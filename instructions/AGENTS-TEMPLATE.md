# Agents (Master Template)

> **What is this file?**
> This is the **output template** - a reference showing what your final `AGENTS.md` should look like.
>
> **Do not fill this in manually.** Instead:
> - **Quick Setup**: Use filled modules and reference them here with links
> - **Guided Generation**: The LLM agent will generate this automatically
>
> This template shows the structure and provides guidance for each section.

---

> **How to use this template**
> 1) Read the short guidance under each heading
> 2) Open the corresponding module in `/modules/*.instructions.md`
> 3) Fill inputs in the module first; then paste/condense the final rules back here (or just link to the module)

**Note**  
_What to write here:_ Any global warnings or constraints (e.g., “Do NOT use Babel. Use SWC only”).  
- Keep it short and non-ambiguous.
- If this affects CI, reference the pipeline step.

**Language Policy (summary)**  
_What to write here:_ One paragraph summary of rules from `modules/language-policy.instructions.md`.  
- Link the module for full details.
- Include the default locale and fallback locale in one line.

---

## Project Overview
_How to fill:_ Describe purpose, scope, and priorities.  
- One short paragraph + 3 bullets (business goals, main components, key constraints).  
- Full details live in `modules/project-overview.instructions.md`.

---

## Project-Type Specific Instructions
_How to fill:_ Summarize directory layout, naming, architecture, module boundaries, UI i18n tool.
- Include 4–6 bullet points.
- Full details: `modules/project-type-specific.instructions.md`.

---

## Tools & Commands
_How to fill:_ List all executable commands (build, test, lint, format), tool calling patterns, mandatory pre-commit hooks.
- Include exact CLI commands with examples.
- Specify command sequencing (e.g., lint → test → build).
- Full details: `modules/tools-commands.instructions.md`.

---

## Agent Persona
_How to fill:_ Define agent role, expertise areas, output style preferences, decision-making authority.
- Include role title and primary/secondary skills.
- Specify what agent can decide autonomously vs. what requires approval.
- Full details: `modules/agent-persona.instructions.md`.

---

## Boundaries & Permissions
_How to fill:_ Define read/write permissions, protected resources, Always/Ask/Never action rules.
- List readable and writable directories (glob patterns).
- Specify protected files and forbidden actions.
- Full details: `modules/boundaries-permissions.instructions.md`.

---

## Agentic Patterns
_How to fill:_ Define Reflection, Planning, Tool Use, and Memory patterns for multi-step autonomous workflows.
- Include reflection checkpoints and planning approaches.
- Specify tool selection strategies and iteration limits.
- Full details: `modules/agentic-patterns.instructions.md`.

---

## Context Management
_How to fill:_ Define token budgets, high-signal prioritization, context compaction strategies, RAG patterns.
- Include token limits and file size thresholds.
- Specify context refresh triggers and caching policies.
- Full details: `modules/context-management.instructions.md`.

---

## Build and Test Commands
_How to fill:_ List build/test commands and whether they’re mandatory or “if required”.  
- Example block with commands.  
- Full details: `modules/build-and-test.instructions.md`.

---

## Code Style Guidelines
_How to fill:_ Conventional Commits, lint/format tools, docs expectations, review rules.  
- Provide 2 commit examples.  
- Full details: `modules/code-style.instructions.md`.

---

## Testing Instructions
_How to fill:_ Unit/integration/e2e requirements, coverage, tooling.  
- State CI pass criteria.  
- Full details: `modules/testing.instructions.md`.

---

## Security Considerations
_How to fill:_ Secrets handling, dependency policy, scans.  
- Mention secret manager and scanning tools.  
- Full details: `modules/security.instructions.md`.

---

## Versioning & Branching Rules
_How to fill:_ Branch model, protected branches, naming conventions, bugfix branching.  
- Include 3–4 example branch names.  
- Full details: `modules/versioning-branching.instructions.md`.

---

## Documentation Structure & Maintenance
_How to fill:_ Docs layout, auto-update rule, CI enforcement.  
- Link `/docs` entry points.  
- Full details: `modules/docs-maintenance.instructions.md`.

---

## Feature Roadmap (Optional)
_How to fill:_ Link to ROADMAP.md and describe status markers.  
- Full details: `modules/roadmap.instructions.md`.

---

## Forbidden Practices
_How to fill:_ 5–7 “never do this” bullets.  
- Full details: `modules/forbidden-practices.instructions.md`.

---

# Modular System Usage
- The **source of truth** for each topic sits under `/modules`.  
- Update module files first; keep this master as the concise index.  
- Use `AGENTS-GUIDED-PROMPT.md` to be guided section-by-section.

