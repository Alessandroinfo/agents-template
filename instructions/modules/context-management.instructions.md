---
applyTo: "**/*"
---

# Context Management – Instructions

## Purpose
_What belongs here:_ Defines how to optimize LLM context usage for maximum efficiency and accuracy. This module addresses token budget management, high-signal information prioritization, context compaction strategies, and techniques to prevent "context rot" (degraded performance with large contexts). Critical for maintaining agent performance on large codebases.

## Inputs Required
_How to fill:_ List each input you need from maintainers. For each, specify:

- **Name**: Token budget limits
  **Format**: Maximum tokens per interaction or cumulative
  **Example**: "Max 8K tokens per request, 100K tokens per session"

- **Name**: High-signal information priorities
  **Format**: Ordered list of what information matters most
  **Example**: "1. Current task files, 2. Related tests, 3. Type definitions, 4. Documentation, 5. Examples"

- **Name**: Context compaction strategies
  **Format**: Methods to reduce context while preserving meaning
  **Example**: "Summarize long files, extract only relevant functions, use references instead of full code"

- **Name**: File size thresholds
  **Format**: When to truncate or summarize files
  **Example**: "Files >500 lines: show structure only; files >1000 lines: require specific line ranges"

- **Name**: Context refresh triggers
  **Format**: When to clear and rebuild context
  **Example**: "After 10 interactions, after switching tasks, after 50K tokens accumulated"

- **Name**: Information retrieval strategy
  **Format**: How to fetch relevant context dynamically
  **Example**: "Use RAG pattern: search → retrieve top 3 matches → read only relevant sections"

- **Name**: Caching policy
  **Format**: What to cache for reuse
  **Example**: "Cache: project structure, common imports, type definitions, frequently accessed files"

## Rules
_How to draft rules:_ Convert inputs into clear, enforceable bullets. Prefer **must/should/never** language.

- Agent **must** stay within token budget limits; truncate or summarize if necessary.
- Agent **must** prioritize high-signal information (relevant code > tangential files).
- Agent **should** use context compaction: summaries over full text when possible.
- Agent **must** apply file size thresholds; never load entire large files into context.
- Agent **should** trigger context refresh when hitting refresh thresholds.
- Agent **must** use RAG patterns for information retrieval: search → filter → load minimal relevant content.
- Agent **should** leverage caching for frequently accessed, static information.
- Agent **never** loads entire directories into context; use targeted file reads.
- Agent **must** prefer specific line ranges over full file reads for large files.
- Agent **should** monitor cumulative token usage and optimize proactively.

## Examples
_How to provide examples:_ Add minimal snippets (naming, files, code, commit messages) that show the rule in practice.

**Example 1: Prioritized context loading**
```markdown
Task: "Fix bug in user authentication"

Context priority:
1. 🔥 HIGH: src/auth/login.service.ts (relevant file)
2. 🔥 HIGH: tests/auth/login.test.ts (tests for context)
3. 🟡 MED: src/auth/types.ts (type definitions)
4. 🟡 MED: docs/auth/flow.md (documentation)
5. ⚪ LOW: package.json (dependencies - reference only)
6. ⚪ LOW: Other auth files (load only if needed)

Load HIGH first, MED if space allows, LOW only on demand.
```

**Example 2: File size threshold handling**
```markdown
File: src/legacy/monolith.service.ts (2500 lines)

❌ BAD: Load entire file
```typescript
// Read 2500 lines → wastes 15K tokens
```

✅ GOOD: Load structure + relevant section
```typescript
// Read file structure → 500 tokens
// Classes: MonolithService, DataProcessor, CacheManager
// Methods: 47 total

// User asks about caching
// Read only CacheManager class (lines 1200-1450) → 2K tokens
```

**Example 3: Context compaction with summarization**
```markdown
Full documentation (5000 words / 6K tokens):
"The authentication system uses JWT tokens with RS256 signing.
It includes refresh tokens, token rotation, and automatic expiration.
Middleware validates tokens on protected routes... [continues for pages]"

Compacted summary (200 words / 300 tokens):
"Auth: JWT RS256, refresh tokens, auto-expiration, middleware validation.
Config: src/auth/config.ts. Key functions: generateToken(), validateToken(), refreshToken()."

Use summary until detailed info needed.
```

**Example 4: RAG-based retrieval**
```markdown
Task: "How do we handle database transactions?"

❌ INEFFICIENT: Load all DB-related files
- Load src/database/** (50 files, 30K tokens)
- Scan manually
- Most files irrelevant

✅ EFFICIENT: RAG pattern
1. Search: grep "transaction" → 5 matches
2. Filter: Most relevant: database/transaction-manager.ts
3. Load: Only that file (200 lines, 1.5K tokens)
4. Extract: Relevant functions only (50 lines, 400 tokens)

Saved 29.6K tokens, got exact answer.
```

**Example 5: Context refresh**
```markdown
Session tracking:
- Interactions: 12
- Tokens used: 85K / 100K budget
- Current task: Different from initial task

→ Trigger: Context refresh

Actions:
1. Summarize previous decisions: 500 tokens
2. Clear detailed code context
3. Keep: Project structure, user preferences, current task
4. Reset counter: 0 interactions, 10K tokens

Continue with fresh, focused context.
```

**Example 6: Caching strategy**
```markdown
Frequently accessed (cache these):
✓ Project structure (directories, key files)
✓ package.json / tsconfig.json (configs)
✓ Common type definitions
✓ API route list
✓ Database schema overview

Cache once, reference many times → save tokens.

Dynamic content (don't cache):
✗ Individual function implementations
✗ Test details (change frequently)
✗ Current work-in-progress files
✗ Temporary outputs
```

## Validation
_How to validate:_ Describe CI/lint/test checks that prove rules are followed.

- **Token monitoring**: Log token usage per interaction; alert if approaching limits.
- **Context audit**: Review agent logs to ensure proper prioritization (high-signal first).
- **Compaction effectiveness**: Measure token savings from summaries vs full loads.
- **Retrieval efficiency**: Track search → load ratio (should be high specificity).
- **Cache hit rate**: Monitor how often cached data is reused.
- **Performance metrics**: Measure response quality vs context size (optimize ratio).
- **Pass criteria**: Stay within budget, maintain quality, no context rot symptoms (repetition, confusion).

## Source of Truth
_How to reference:_ Link canonical docs in `/docs/*` (ADR, architecture, API schemas, i18n guides).

- `/docs/agent/context-policy.md` → Complete context management documentation
- `/docs/agent/token-budgets.md` → Token limits and allocation strategies
- `/docs/agent/rag-patterns.md` → Retrieval-augmented generation workflows
- `/docs/agent/caching-strategy.md` → What and how to cache
- `/docs/performance/context-optimization.md` → Performance tuning for context
- `/docs/architecture/file-structure.md` → Project structure for quick reference

### Fill-in tips (specific)
- Specify **token limits** for your LLM model (GPT-4: 8K/32K, Claude: 100K/200K, etc.).
- Define **priority tiers** (critical/high/medium/low) for different file types.
- Set **size thresholds** based on your typical file sizes (adjust 500/1000 line limits).
- Document **compaction techniques** (AST summaries, signature extraction, docstring only).
- Create **retrieval patterns** for common queries (how to find config, locate feature, etc.).
- List **cacheable items** specific to your project (schema, constants, types).
- Define **refresh indicators** (task switches, time elapsed, token accumulation).
- Include **emergency strategies** if context limit hit (what to drop first).
- Consider **multi-repository** scenarios (monorepo vs multiple projects).
