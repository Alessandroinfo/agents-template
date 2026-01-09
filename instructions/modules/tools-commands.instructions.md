---
applyTo: "**/*"
---

# Tools & Commands – Instructions

## Purpose
_What belongs here:_ Defines all executable commands (build, test, lint, format), tool calling patterns for agentic workflows, and mandatory CLI operations. This module ensures agents know exactly which tools to use, when to use them, and what commands must run before commits or deployments.

## Inputs Required
_How to fill:_ List each input you need from maintainers. For each, specify:

- **Name**: Build command
  **Format**: Exact CLI command with parameters
  **Example**: `npm run build` or `make build`

- **Name**: Test command
  **Format**: Exact CLI command with parameters
  **Example**: `npm test` or `pytest tests/`

- **Name**: Lint command
  **Format**: Exact CLI command with parameters
  **Example**: `npm run lint` or `eslint . --fix`

- **Name**: Format command
  **Format**: Exact CLI command with parameters
  **Example**: `npm run format` or `prettier --write .`

- **Name**: Pre-commit commands (mandatory)
  **Format**: Ordered list of commands that MUST run before any commit
  **Example**: `1. npm run lint 2. npm test 3. npm run build`

- **Name**: Development server command
  **Format**: Exact CLI command to start dev environment
  **Example**: `npm run dev` or `docker-compose up`

- **Name**: Tool calling patterns
  **Format**: Description of when agent should use which tools
  **Example**: "Use search tool before making changes, use read tool to understand context"

- **Name**: CI/CD integration commands
  **Format**: Commands used in CI pipeline
  **Example**: `npm ci && npm run test:ci && npm run build`

## Rules
_How to draft rules:_ Convert inputs into clear, enforceable bullets. Prefer **must/should/never** language.

- Agents **must** run pre-commit commands in the specified order before any git commit.
- Agents **must** verify build success before proposing code changes as complete.
- Agents **should** run tests after any code modification that affects functionality.
- Agents **must** use linting tools and fix all auto-fixable issues before manual review.
- Agents **never** commit code that fails build, test, or lint checks.
- Agents **must** use the development server command when asked to preview or test locally.
- Tool calling **must** follow the reflection pattern: search → read → understand → act → verify.
- Agents **should** use format command after any code generation or modification.
- CI/CD commands **must** match local validation commands to ensure consistency.

## Examples
_How to provide examples:_ Add minimal snippets (naming, files, code, commit messages) that show the rule in practice.

**Example 1: Pre-commit workflow**
```bash
# Before committing changes:
npm run lint          # Fix style issues
npm test             # Ensure tests pass
npm run build        # Verify build works
git add .
git commit -m "feat: add user authentication"
```

**Example 2: Tool calling pattern**
```
User asks: "Fix the login bug"
Agent workflow:
1. grep "login" → find relevant files
2. Read identified files → understand implementation
3. Identify issue → plan fix
4. Apply changes → edit files
5. npm test → verify fix works
6. npm run lint → ensure style compliance
```

**Example 3: Development workflow**
```bash
# Starting work on feature
npm run dev          # Start development server
# Make changes...
npm run lint         # Check style
npm test            # Run tests
npm run build       # Verify production build
```

## Validation
_How to validate:_ Describe CI/lint/test checks that prove rules are followed.

- **Pre-commit hooks**: Use `husky` or `pre-commit` framework to enforce mandatory commands.
- **CI pipeline**: GitHub Actions/GitLab CI must run identical commands as local pre-commit.
- **Build verification**: CI must fail if `build` command exits with non-zero code.
- **Test coverage**: CI must enforce minimum coverage thresholds (specify in testing.instructions.md).
- **Lint enforcement**: CI must fail on any lint errors (warnings optional based on project policy).
- **Pass criteria**: All commands must exit with code 0; any failure blocks merge.

## Source of Truth
_How to reference:_ Link canonical docs in `/docs/*` (ADR, architecture, API schemas, i18n guides).

- `/docs/development/commands.md` → Complete command reference
- `/docs/ci-cd/pipeline.md` → CI/CD configuration and validation rules
- `/docs/development/tool-patterns.md` → Agentic tool calling patterns and workflows
- `package.json` or `Makefile` → Source of truth for script definitions
- `.github/workflows/` or `.gitlab-ci.yml` → CI command definitions

### Fill-in tips (specific)
- List **all** commands an agent might need (install, clean, deploy, etc.).
- Specify **versions** of tools if critical (Node 18+, Python 3.11+).
- Mark commands as **mandatory**, **recommended**, or **optional**.
- Include **error handling**: what to do if a command fails.
- Document **platform differences** (Windows vs Unix commands).
- Reference **Make targets**, **npm scripts**, or **shell scripts** as appropriate.
- Include **environment variables** required for commands to work.
