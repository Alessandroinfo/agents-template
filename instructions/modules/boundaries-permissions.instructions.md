---
applyTo: "**/*"
---

# Boundaries & Permissions – Instructions

## Purpose
_What belongs here:_ Defines explicit boundaries for what the agent can read, write, modify, and must never touch. This module establishes file system permissions, protected resources, and three-tier rules (Always do / Ask first / Never do). Critical for preventing accidental damage and maintaining code safety with autonomous agents.

## Inputs Required
_How to fill:_ List each input you need from maintainers. For each, specify:

- **Name**: Readable directories
  **Format**: Glob patterns or directory paths
  **Example**: `src/**, tests/**, docs/**, *.md`

- **Name**: Writable directories
  **Format**: Glob patterns or directory paths
  **Example**: `src/**, tests/**, docs/**, dist/**`

- **Name**: Protected/read-only resources
  **Format**: Glob patterns or file paths that should never be modified
  **Example**: `.env, .env.*, credentials.json, config/production.yaml, vendor/**, node_modules/**`

- **Name**: Always do (autonomous actions)
  **Format**: List of actions agent can perform without asking
  **Example**: "Add unit tests, refactor within files, fix linting issues, update documentation"

- **Name**: Ask first (approval required)
  **Format**: List of actions requiring user confirmation
  **Example**: "Add dependencies, modify database schemas, change API contracts, delete files"

- **Name**: Never do (forbidden actions)
  **Format**: List of actions strictly prohibited
  **Example**: "Commit secrets, modify production configs, delete entire directories, force-push to main"

- **Name**: Dangerous patterns to avoid
  **Format**: Specific code or file patterns that should trigger warnings
  **Example**: "API keys in code, hardcoded passwords, `rm -rf`, database drop commands"

- **Name**: Commit restrictions
  **Format**: Rules about what can/cannot be committed
  **Example**: "Never commit .env files, node_modules, build artifacts, IDE settings"

## Rules
_How to draft rules:_ Convert inputs into clear, enforceable bullets. Prefer **must/should/never** language.

- Agent **must** only read files within readable directories; all other locations are off-limits.
- Agent **must** only write/modify files within writable directories.
- Agent **never** modifies protected/read-only resources under any circumstances.
- Agent **must** perform "Always do" actions autonomously without requesting approval.
- Agent **must** request explicit approval before performing "Ask first" actions.
- Agent **never** performs "Never do" actions, even if explicitly requested by user.
- Agent **must** scan for dangerous patterns before committing and refuse to commit if found.
- Agent **never** commits files matching commit restriction patterns.
- Agent **should** warn user when approaching boundary limits (e.g., about to modify sensitive file).
- Agent **must** validate file paths against permission rules before any write operation.

## Examples
_How to provide examples:_ Add minimal snippets (naming, files, code, commit messages) that show the rule in practice.

**Example 1: Directory permissions**
```yaml
permissions:
  read:
    - "src/**"
    - "tests/**"
    - "docs/**"
    - "*.md"
    - "package.json"
    - "tsconfig.json"

  write:
    - "src/**"
    - "tests/**"
    - "docs/**"
    - "README.md"

  protected:
    - ".env*"
    - "config/production.*"
    - "node_modules/**"
    - "dist/**"
    - ".git/**"
    - "credentials.*"
```

**Example 2: Three-tier action rules**
```markdown
✅ ALWAYS DO (autonomous):
- Add/modify unit tests in tests/**
- Refactor code within existing files
- Fix ESLint errors
- Update function documentation
- Format code with prettier
- Add type annotations

⚠️ ASK FIRST (requires approval):
- Install new npm packages
- Modify database schema files
- Change API endpoint signatures
- Delete unused files
- Modify build configuration
- Update dependency versions

🚫 NEVER DO (strictly forbidden):
- Commit .env or .env.* files
- Delete entire directories
- Modify files in vendor/
- Hard-code secrets or API keys
- Force-push to protected branches
- Execute rm -rf or destructive commands
- Disable security checks
```

**Example 3: Pre-commit validation**
```javascript
// Agent validates before commit:
const forbiddenPatterns = [
  /\.env$/,
  /credentials\.json$/,
  /api[_-]?key\s*=\s*['"][^'"]+['"]/i,
  /password\s*=\s*['"][^'"]+['"]/i,
  /secret[_-]?key\s*=\s*['"][^'"]+['"]/i
];

// If any pattern matches:
// ❌ Refuse to commit
// ⚠️ Show warning with matched pattern
// 💡 Suggest moving to environment variables
```

**Example 4: Boundary warnings**
```
User: "Update the production config file"
Agent: "⚠️ Warning: config/production.yaml is protected. I cannot modify this file.
        Please update it manually or adjust boundaries in boundaries-permissions.instructions.md"

User: "Add the axios library"
Agent: "⚠️ This requires approval (adding dependency). Proceed? [y/n]"

User: "Delete the old api folder"
Agent: "⚠️ This requires approval (deleting directory). Proceed? [y/n]"
```

## Validation
_How to validate:_ Describe CI/lint/test checks that prove rules are followed.

- **Pre-commit hooks**: Scan staged files against forbidden patterns; block commit if match found.
- **Git ignore validation**: Ensure `.gitignore` includes all protected patterns.
- **Secret scanning**: Use tools like `gitleaks`, `truffleHog`, or `detect-secrets` in CI.
- **Permission tests**: Automated tests that verify agent cannot write to protected paths.
- **Audit logs**: Track all agent write operations and validate against permission rules.
- **CI checks**: Fail pipeline if any protected file is modified or forbidden pattern detected.
- **Pass criteria**: No secrets committed, no protected files modified, all write operations within boundaries.

## Source of Truth
_How to reference:_ Link canonical docs in `/docs/*` (ADR, architecture, API schemas, i18n guides).

- `/docs/security/boundaries.md` → Complete boundary and permission documentation
- `/docs/security/secrets-management.md` → How to handle secrets properly
- `.gitignore` → Canonical list of files never to commit
- `/docs/development/protected-resources.md` → Explanation of why resources are protected
- `/docs/agent/permission-matrix.md` → Detailed permission breakdown by directory
- `CODEOWNERS` → File ownership and required reviewers for sensitive files

### Fill-in tips (specific)
- Use **glob patterns** for flexibility (`src/**/*.ts` instead of listing every file).
- Be **explicit about exceptions** (e.g., "all of src/** except src/generated/**").
- Consider **temporary files** (logs, caches) - usually writable but not committable.
- Document **environment-specific** boundaries (dev vs staging vs production).
- Include **IDE-specific** files in protected list (.vscode/, .idea/).
- Define **audit requirements** (some changes require logging, not just permission).
- Specify **recovery procedures** if agent violates boundary (rollback, alert, etc.).
- List **sensitive data patterns** beyond just file names (regex patterns for secrets).
