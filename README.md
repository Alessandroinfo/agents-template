# Agent Instructions Generator

A **modular system** for creating clear, enforceable instructions for AI coding agents (GitHub Copilot, Claude, Cursor, Gemini, etc.).

Includes best practices for LLM coding agents: agentic workflows, context management, AGENTS.md standard, boundaries & permissions.

---

## Two Ways to Use This System

Choose the method that fits your needs:

| Method | Best For | Time Required | Output |
|--------|----------|---------------|--------|
| **Quick Setup** | Specific needs, small projects, cherry-pick modules | 10-30 minutes | Selected module files |
| **Guided Generation** | Complete setup, new projects, comprehensive instructions | 30-90 minutes | Full AGENTS.md + all modules |

---

## Method 1: Quick Setup (Manual)

**Copy and customize only the modules you need.**

### When to use:
- You need specific guidelines (e.g., only code style + testing)
- Small project with focused requirements
- You want to add modules incrementally
- You prefer manual control

### How to use:
1. Browse available modules in [`instructions/MODULES-INDEX.md`](instructions/MODULES-INDEX.md)
2. Copy the modules you need from [`instructions/modules/`](instructions/modules/)
3. Fill in the "Inputs Required" sections with your project specifics
4. Follow the detailed guide: **[`instructions/QUICK-START.md`](instructions/QUICK-START.md)**

**Example**: Need only code style rules? Copy `code-style.instructions.md` and fill it in.

---

## Method 2: Guided Generation (LLM-Assisted)

**Let an AI agent guide you through creating complete instructions.**

### When to use:
- New project needing comprehensive setup
- You want all modules configured consistently
- You prefer interactive Q&A over manual editing
- Team alignment on standards

### How to use:
1. Open [`instructions/AGENTS-GUIDED-PROMPT.md`](instructions/AGENTS-GUIDED-PROMPT.md)
2. Copy the entire prompt block
3. Paste it into your AI coding agent (Claude, Copilot, Cursor, etc.)
4. Type **`start`** and answer the questions

The agent will:
- Ask about your project specifics for each module
- Generate rules and examples based on your answers
- Assemble a complete `AGENTS.md` file with all modules
- Export everything to `/dist` directory

**Full guide**: [`instructions/AGENTS-GUIDED-PROMPT.md`](instructions/AGENTS-GUIDED-PROMPT.md)

---

## What You'll Get

After using either method, you'll have:

- **`AGENTS.md`**: Master instruction file for your AI agents
- **Module files**: Detailed rules organized by topic (code style, testing, security, etc.)
- **Ready-to-use guidelines**: That your team's AI agents will follow consistently

---

## Project Structure

```
/instructions/
├── QUICK-START.md              # Guide for Method 1 (manual)
├── AGENTS-GUIDED-PROMPT.md     # Guide for Method 2 (LLM-assisted)
├── MODULES-INDEX.md            # Full list of available modules
├── AGENTS-TEMPLATE.md          # Output template reference
└── modules/                    # Individual instruction modules
    ├── agent-persona.instructions.md
    ├── tools-commands.instructions.md
    ├── code-style.instructions.md
    └── ... (16 core modules + 5 optional)
```

---

## Available Modules

**Core Modules** (16):
- Language Policy, Project Overview, Project-Type Specific
- Tools & Commands, Agent Persona, Boundaries & Permissions
- Agentic Patterns, Context Management
- Build & Test, Code Style, Testing, Security
- Versioning & Branching, Docs & Maintenance
- Roadmap, Forbidden Practices

**Optional Modules** (5):
- Frontend UI, API & Backend, Style & Tooling
- Branching (alias), Docs (alias)

See [`instructions/MODULES-INDEX.md`](instructions/MODULES-INDEX.md) for details.

---

## Getting Started

1. **Choose your method** (Quick Setup vs Guided Generation)
2. **Follow the appropriate guide**:
   - Quick: [`instructions/QUICK-START.md`](instructions/QUICK-START.md)
   - Guided: [`instructions/AGENTS-GUIDED-PROMPT.md`](instructions/AGENTS-GUIDED-PROMPT.md)
3. **Customize** the generated instructions for your project
4. **Use** the `AGENTS.md` file with your AI coding agents

---

## Questions?

- **How do I know which modules I need?** → See module use cases in [`MODULES-INDEX.md`](instructions/MODULES-INDEX.md)
- **Can I mix both methods?** → Yes! Start with Quick Setup, use Guided for remaining modules
- **How do I maintain these over time?** → Update module files when project rules change, keep AGENTS.md in sync

---

## License

MIT License - See LICENSE file for details
