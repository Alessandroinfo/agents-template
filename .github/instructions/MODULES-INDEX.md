# Modular Instructions – Index (with guidance)

> **How to use this index:**  
> 1) Pick a module, open its file in `/modules`, fill "Inputs Required".  
> 2) Convert inputs into enforceable "Rules" and add tiny "Examples".  
> 3) Define "Validation" (CI, lint, tests).  
> 4) Link to any canonical "Source of Truth" in `/docs`.

## Core Modules
| Module | Path | Scope / applyTo | How to Fill |
|-------|------|------------------|-------------|
| Language Policy | modules/language-policy.instructions.md | **/* | Set language & casing for comments/identifiers; UI/i18n policy; locales & fallback |
| Project Overview | modules/project-overview.instructions.md | **/* | Purpose, scope, priorities; stability vs speed |
| Project-Type Specific | modules/project-type-specific.instructions.md | src/**/* | Directory layout, patterns, architecture, state, i18n |
| Build & Test | modules/build-and-test.instructions.md | **/* | Build/test/CI commands; mandatory vs optional |
| Code Style | modules/code-style.instructions.md | **/* | Conventional Commits; lint/format; docs; reviews |
| Testing | modules/testing.instructions.md | **/*.{spec,test}.{ts,tsx,js,jsx} | Test levels, coverage, tools, CI artifacts |
| Security | modules/security.instructions.md | **/* | Secrets, dep policy, scans, SBOM |
| Versioning & Branching | modules/versioning-branching.instructions.md | **/* | Branch model + naming; bugfix branches |
| Docs & Maintenance | modules/docs-maintenance.instructions.md | docs/**/* | Docs layout; auto-update; CI gating |
| Roadmap | modules/roadmap.instructions.md | ROADMAP.md | Feature list & status markers |
| Forbidden Practices | modules/forbidden-practices.instructions.md | **/* | “Never do this” rules |

## Optional / Alias Modules
| Module | Path | Scope / applyTo | Notes / How to Fill |
|-------|------|------------------|---------------------|
| Frontend UI | modules/frontend-ui.instructions.md | src/**/*.{tsx,jsx,ts,js,html,css,scss} | UI/i18n/accessibility details; components/testing patterns |
| API & Backend | modules/api.instructions.md | src/**/*.{ts,js,py,go,java,kt,rb} | Clean/Hex rules; contracts; error/logging format |
| Style & Tooling | modules/style.instructions.md | **/* | Extra lint/format/commit rules |
| Branching (Alias) | modules/branching.instructions.md | **/* | Alias of versioning—use if you split files |
| Docs (Alias/Generic) | modules/docs.instructions.md | docs/**/* | Authoring style; headings; references |

> Use `AGENTS-GUIDED-PROMPT.md` to be asked whether to include optional modules.
