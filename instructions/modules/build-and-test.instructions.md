---
applyTo: "**/*"
---

# Build & Test – Instructions

## Purpose
_What belongs here:_ A one-paragraph description of what this module governs and why it matters.

## Inputs Required
_How to fill:_ List each input you need from maintainers. For each, specify:
- **Name** (what):  
- **Format** (how to write it):  
- **Example** (one realistic sample):  

## Rules
_How to draft rules:_ Convert inputs into clear, enforceable bullets. Prefer **must/should/never** language.
- Keep each rule testable by a human reviewer or by CI.
- When relevant, reference files, folders, commands, or globs.

## Examples
_How to provide examples:_ Add minimal snippets (naming, files, code, commit messages) that show the rule in practice.

## Validation
_How to validate:_ Describe CI/lint/test checks that prove rules are followed.
- Mention tools, scripts, or workflows.
- Define pass/fail criteria.

## Source of Truth
_How to reference:_ Link canonical docs in `/docs/*` (ADR, architecture, API schemas, i18n guides).


### Fill-in tips (specific)
- List exact commands for build/test/lint/ci; tag them as **mandatory** or **if required**.
- Note platform constraints (Node version, Go version, etc.).
- Reference CI entrypoints (workflows, Make targets, npm scripts).
- **Tool calling integration**: Define which commands agent must run automatically (pre-commit hooks).
- Specify **command sequencing**: Order matters (lint → test → build vs build → test).
- Link to `tools-commands.instructions.md` for detailed tool use patterns.
- Include **verification commands** (how to check if build/test succeeded).

