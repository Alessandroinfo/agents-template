---
applyTo: "**/*"
---

# Agentic Patterns – Instructions

## Purpose
_What belongs here:_ Defines how the agent should think, plan, and execute complex multi-step tasks. This module implements agentic workflow patterns: Reflection (self-evaluation), Planning (task decomposition), Tool Use (intelligent tool selection), and Memory (context retention). These patterns enable autonomous problem-solving and iterative refinement.

## Inputs Required
_How to fill:_ List each input you need from maintainers. For each, specify:

- **Name**: Reflection requirements
  **Format**: When and how agent should self-evaluate
  **Example**: "After each code change, verify: tests pass, no lint errors, logic is correct; if any fail, iterate"

- **Name**: Planning approach
  **Format**: How to break down complex tasks
  **Example**: "For features: 1) analyze requirements, 2) design solution, 3) implement incrementally, 4) test, 5) document"

- **Name**: Tool selection strategy
  **Format**: Rules for choosing which tools to use
  **Example**: "Search before read, read before write, test after write, verify before commit"

- **Name**: Memory retention policy
  **Format**: What information to remember across interactions
  **Example**: "Remember: user preferences, previous decisions, code patterns used, failed approaches"

- **Name**: Iteration limits
  **Format**: Maximum attempts before escalating to user
  **Example**: "Max 3 attempts to fix failing tests; if still failing, ask user for guidance"

- **Name**: Multi-step workflow patterns
  **Format**: Standard sequences for common tasks
  **Example**: "Bug fix workflow: reproduce → locate → fix → test → verify no regression"

- **Name**: Contextual adaptation rules
  **Format**: How to adjust behavior based on context
  **Example**: "In tests/, prioritize correctness over performance; in src/, balance both"

## Rules
_How to draft rules:_ Convert inputs into clear, enforceable bullets. Prefer **must/should/never** language.

- Agent **must** follow the Reflection pattern: after each significant action, evaluate success and iterate if needed.
- Agent **must** use Planning pattern for complex tasks: decompose into steps, execute sequentially, verify each step.
- Agent **must** follow Tool Use pattern: select appropriate tools based on current need (search → read → understand → act).
- Agent **should** maintain Memory: reference previous decisions and avoid repeating failed approaches.
- Agent **must** respect iteration limits; escalate to user after maximum attempts.
- Agent **should** adapt behavior based on context (test files vs source files, dev vs prod).
- Agent **never** proceeds with later steps if earlier steps failed; fix or escalate first.
- Agent **must** use multi-step workflows for standard tasks (bug fixes, features, refactoring).
- Agent **should** explain its reasoning when making significant decisions (transparency).
- Agent **must** cache successful patterns and reuse them for similar tasks (learning).

## Examples
_How to provide examples:_ Add minimal snippets (naming, files, code, commit messages) that show the rule in practice.

**Example 1: Reflection Pattern**
```markdown
Task: "Implement user authentication"

Agent workflow with reflection:
1. Plan: Break down into subtasks
   Self-check: Are all requirements covered?

2. Implement login endpoint
   Self-check: Does it follow API conventions?
   Failed: Missing input validation
   Iterate: Add validation

3. Add tests
   Self-check: Coverage >80%? Pass?
   All checks pass

4. Final reflection:
   Tests pass
   Lint clean
   Follows architecture
   Documented
   Ready for review
```

**Example 2: Planning Pattern**
```markdown
User: "Add export to CSV feature"

Agent planning:
┌─ Phase 1: Understand
│  ├─ Read existing export code
│  ├─ Identify data structures
│  └─ Check available libraries
│
┌─ Phase 2: Design
│  ├─ Design CSV format
│  ├─ Plan file structure
│  └─ Consider edge cases
│
┌─ Phase 3: Implement
│  ├─ Create CSVExporter class
│  ├─ Add export endpoint
│  └─ Handle errors
│
┌─ Phase 4: Test
│  ├─ Unit tests for CSVExporter
│  ├─ Integration test for endpoint
│  └─ Test edge cases
│
└─ Phase 5: Finalize
   ├─ Update documentation
   ├─ Add usage example
   └─ Verify all checks pass
```

**Example 3: Tool Use Pattern**
```markdown
Task: "Fix bug in payment processing"

Intelligent tool selection:
1. Grep: Search for "payment" → find relevant files
2. Read: Read payment.service.ts → understand logic
3. Read: Read payment.test.ts → understand expected behavior
4. Grep: Search for error message → locate bug source
5. Read: Read transaction.model.ts → understand data flow
6. Edit: Fix bug in payment.service.ts
7. Run: npm test → verify fix
8. Read: Review test output → ensure no regression
9. Commit: Bug fixed and verified

Right tool for right task, in logical sequence.
```

**Example 4: Memory Pattern**
```markdown
Session 1:
User: "Use functional components, not classes"
Agent: Stored preference: React → functional components

Session 2:
User: "Add a new component"
Agent: [Remembers preference] → creates functional component automatically

Session 3:
User: "Why did you use a functional component?"
Agent: "Based on your Session 1 preference for functional over class components"

Memory enables consistency across interactions.
```

**Example 5: Iteration with Limits**
```markdown
Attempt 1: Fix test - Still failing (wrong approach)
Attempt 2: Different fix - Still failing (edge case missed)
Attempt 3: Refactor approach - Still failing (underlying issue)
Limit reached (3 attempts)

Agent: "I've tried 3 different approaches but tests still fail:
1. Adjusted timeout → didn't help
2. Fixed mock data → didn't help
3. Refactored async logic → didn't help

The issue may be in database setup or environment config.
Please review: tests/integration/payment.test.ts:45"

Escalate instead of infinite loops.
```

## Validation
_How to validate:_ Describe CI/lint/test checks that prove rules are followed.

- **Planning compliance**: Review agent logs to ensure multi-step tasks were decomposed before execution.
- **Reflection verification**: Check that agent re-ran tests/lint after each significant change.
- **Tool use efficiency**: Audit tool call sequences to ensure logical progression (search→read→write).
- **Memory consistency**: Verify agent applied previous decisions to new similar tasks.
- **Iteration tracking**: Ensure agent escalated after hitting iteration limits (no infinite loops).
- **Workflow adherence**: Validate standard workflows (bug fix, feature) followed defined patterns.
- **Pass criteria**: Agent completes tasks using patterns, reflects on results, doesn't exceed iteration limits.

## Source of Truth
_How to reference:_ Link canonical docs in `/docs/*` (ADR, architecture, API schemas, i18n guides).

- `/docs/agent/patterns.md` → Complete agentic patterns documentation
- `/docs/agent/workflows.md` → Standard workflow definitions
- `/docs/agent/reflection-checklist.md` → Self-evaluation criteria
- `/docs/agent/tool-selection.md` → Tool selection decision tree
- `/docs/agent/memory-policy.md` → What to remember and for how long
- `/docs/development/iteration-limits.md` → When to escalate vs retry

### Fill-in tips (specific)
- Define **reflection checkpoints** (after each commit, after tests, after deployment).
- Create **workflow templates** for common tasks (feature, bugfix, refactor, optimization).
- Specify **tool sequences** explicitly (e.g., "always grep before read for efficiency").
- Set **iteration thresholds** (how many retries before asking for help).
- Document **memory scope** (session-only, project-wide, user-wide).
- Include **decision trees** for when to use which pattern.
- Define **success criteria** for each workflow step.
- Add **failure handling** strategies (retry, adapt, escalate).
- Consider **parallel vs sequential** execution where applicable.
