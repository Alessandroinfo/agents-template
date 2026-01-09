# Modules Index

**Complete list of all available instruction modules for AI coding agents.**

---

## How to Read This Index

Each module contains:
- **Purpose**: What the module covers
- **Scope/ApplyTo**: Which files/directories it affects
- **When to Use**: Common scenarios requiring this module
- **How to Fill**: What information you need to provide

**Module Types**:
- **[CORE]** - Recommended for most projects
- **[OPTIONAL]** - Use for specific project types or needs

---

## Quick Selection Guide

**Choose modules by project type**:

| Project Type | Recommended Modules |
|--------------|---------------------|
| **Minimal** | code-style, testing, forbidden-practices |
| **Backend API** | code-style, testing, api, security, tools-commands |
| **Frontend** | code-style, testing, frontend-ui, build-and-test |
| **Full Stack** | All core + frontend-ui + api |
| **Team Setup** | agent-persona, boundaries-permissions, code-style, tools-commands |

---

## Core Modules (16)

| Tag | Module | Path | Scope | When to Use |
|-----|--------|------|-------|-------------|
| [CORE] | **Language Policy** | modules/language-policy.instructions.md | **/* | Multi-language projects, i18n requirements, comment standards |
| [CORE] | **Project Overview** | modules/project-overview.instructions.md | **/* | Project onboarding, context for agents, priority setting |
| [CORE] | **Project-Type Specific** | modules/project-type-specific.instructions.md | src/**/* | Directory structure rules, architecture patterns, module boundaries |
| [CORE] | **Tools & Commands** | modules/tools-commands.instructions.md | **/* | Pre-commit hooks, build/test commands, CLI workflows |
| [CORE] | **Agent Persona** | modules/agent-persona.instructions.md | **/* | Define agent expertise, output style, decision authority |
| [CORE] | **Boundaries & Permissions** | modules/boundaries-permissions.instructions.md | **/* | File permissions, protected resources, safety rules |
| [CORE] | **Agentic Patterns** | modules/agentic-patterns.instructions.md | **/* | Multi-step workflows, reflection, planning, memory |
| [CORE] | **Context Management** | modules/context-management.instructions.md | **/* | Large codebases, token optimization, context strategies |
| [CORE] | **Build & Test** | modules/build-and-test.instructions.md | **/* | Build process, test commands, CI integration |
| [CORE] | **Code Style** | modules/code-style.instructions.md | **/* | Commit messages, linting, formatting, code examples |
| [CORE] | **Testing** | modules/testing.instructions.md | **/*.{spec,test}.* | Test requirements, coverage targets, testing frameworks |
| [CORE] | **Security** | modules/security.instructions.md | **/* | Secret handling, dependency policies, security scans |
| [CORE] | **Versioning & Branching** | modules/versioning-branching.instructions.md | **/* | Git workflow, branch naming, release process |
| [CORE] | **Docs & Maintenance** | modules/docs-maintenance.instructions.md | docs/**/* | Documentation standards, auto-updates, CI enforcement |
| [CORE] | **Roadmap** | modules/roadmap.instructions.md | ROADMAP.md | Feature planning, status tracking, project timeline |
| [CORE] | **Forbidden Practices** | modules/forbidden-practices.instructions.md | **/* | Anti-patterns, prohibited actions, safety rules |

---

## Optional Modules (5)

| Tag | Module | Path | Scope | When to Use |
|-----|--------|------|-------|-------------|
| [OPTIONAL] | **Frontend UI** | modules/frontend-ui.instructions.md | src/**/*.{tsx,jsx,html,css} | React/Vue/Angular projects, UI components, accessibility |
| [OPTIONAL] | **API & Backend** | modules/api.instructions.md | src/**/*.{ts,js,py,go,java} | REST/GraphQL APIs, backend architecture, clean architecture |
| [OPTIONAL] | **Style & Tooling** | modules/style.instructions.md | **/* | Additional style rules beyond code-style module |
| [OPTIONAL] | **Branching (Alias)** | modules/branching.instructions.md | **/* | Alternative to versioning-branching if you need separate file |
| [OPTIONAL] | **Docs (Alias)** | modules/docs.instructions.md | docs/**/* | Alternative to docs-maintenance for simpler projects |

---

## How to Choose Modules

### Start with essentials (3-5 modules):
1. **code-style** - Universal, every project needs this
2. **testing** - If you have tests
3. **tools-commands** - For build/test/deploy automation
4. **forbidden-practices** - Safety rules
5. **agent-persona** - If using autonomous agents

### Add as needed:
- **security** - If handling sensitive data
- **boundaries-permissions** - For team projects with safety requirements
- **frontend-ui** or **api** - Based on project type
- **agentic-patterns** - For complex multi-step agent workflows
- **context-management** - For large codebases (1000+ files)

### Use guided generation if:
- You want all modules configured consistently
- New project with comprehensive requirements
- Team onboarding and alignment

---

## Related Documentation

- **[QUICK-START.md](QUICK-START.md)** - Manual module selection guide
- **[AGENTS-GUIDED-PROMPT.md](AGENTS-GUIDED-PROMPT.md)** - Automated generation with LLM
- **[AGENTS-TEMPLATE.md](AGENTS-TEMPLATE.md)** - Output file structure reference
