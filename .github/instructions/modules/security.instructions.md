---
applyTo: "**/*"
---

# Security – Instructions

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
- Secret manager, dependency sources, vulnerability scanning (Dependabot/Snyk).
- SBOM policy, input validation, logging redaction.
- Rules for third-party code and licenses.

