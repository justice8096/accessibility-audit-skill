# Security Policy

## Scope

This repository contains a Claude skill (markdown instruction files and reference documentation) for running WCAG 2.2 accessibility audits. It does **not** contain executable code, runtime dependencies, or server components.

The skill analyzes user-provided source code and generates markdown audit reports. It never executes, compiles, or runs the code it audits.

## Supported Versions

| Version | Supported |
|---------|-----------|
| 1.0.x   | Yes       |

## Reporting a Vulnerability

If you discover a security issue in this skill (e.g., instructions that could lead to unsafe operations, information disclosure, or prompt injection vectors), please report it responsibly:

1. **Email:** justice8096@gmail.com
2. **Subject line:** `[SECURITY] accessibility-audit-skill: <brief description>`
3. **Include:** Description of the issue, reproduction steps, and potential impact

**Response timeline:**
- Acknowledgment within 48 hours
- Assessment and fix within 7 days for confirmed issues
- Public disclosure after fix is released

## Security Considerations

### Data Handling

This skill may process proprietary source code during audits. Users should be aware that:
- Code snippets shared for audit may appear in generated audit reports
- Audit reports may contain sensitive architectural details
- Users should review audit reports before sharing or committing them to public repositories
- The `.gitignore` excludes generated audit reports (`Accessibility-Audit-Report-*.md`) by default to prevent accidental commits

### No Code Execution

This skill operates entirely through static analysis of source code provided by the user. It:
- Never executes, compiles, or runs audited code
- Never makes network requests or accesses external APIs
- Never modifies the audited codebase (remediation code is suggested, not applied)
- Never accesses the filesystem beyond reading files the user explicitly shares

### Eval Test Cases

The `evals/evals.json` file contains test prompts with embedded code snippets. These are for testing the skill's audit capabilities and are not executed. The code snippets are intentionally accessibility-noncompliant for testing purposes.
