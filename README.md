# Accessibility Audit Skill

A comprehensive WCAG 2.2 Level AA accessibility audit skill for Claude. Generates structured audit reports with severity-based findings, evidence collection, and framework-specific remediation for Angular and React.

## What It Does

When triggered, this skill guides Claude through a 4-phase accessibility audit:

1. **Automated Extraction** — scans source code for missing `alt`, unlabeled inputs, missing landmarks, `div onClick` without keyboard handlers, missing `aria-live` regions
2. **Framework-Specific Checks** — loads Angular or React reference and checks for framework-specific anti-patterns
3. **Manual / Human-Judgment Checks** — evaluates heading hierarchy, meaningful link text, cognitive load, color-only information, motion
4. **Report Generation** — produces a structured markdown report with CRITICAL/HIGH/MEDIUM/LOW findings, full WCAG 2.2 criterion checklist, remediation roadmap, and evidence checklist

## Report Format

The audit report mirrors the evidence-collection approach from the [LLMCompliance pipeline](https://github.com/justice8096/ai-compliance-extractors):

- Metadata block with framework, tools used, scope, conformance target
- Executive summary with findings by severity and conformance by WCAG principle
- Detailed findings — each includes WCAG criterion, element, description, impact, reproduction steps, evidence, concrete remediation code, and effort estimate
- Full WCAG 2.2 criterion checklist (every applicable criterion marked PASS/FAIL/N-A)
- Remediation roadmap prioritized by severity then effort
- Testing methodology checklist (automated, keyboard, screen reader, visual)
- Compliance framework mapping (connects to LLMCompliance templates T02, T03, T09, T10, T13)

## Installation

### As a Claude Code Skill

Copy this directory into your Claude Code skills folder:

```bash
cp -r accessibility-audit-skill/ ~/.claude/skills/accessibility-audit/
```

### As a Cowork Plugin Skill

Place in your plugin's `skills/` directory following the [plugin skill format](https://docs.claude.com).

## File Structure

```
accessibility-audit-skill/
├── SKILL.md                     # Main skill — audit template, process, severity guide
├── references/
│   ├── angular-a11y.md          # Angular CDK A11y, common failures, eslint rules
│   └── react-a11y.md            # React Aria, Radix, shadcn/ui, SPA focus management
├── README.md
├── LICENSE
└── .gitignore
```

## Trigger Phrases

The skill activates when you mention any of the following:

- "accessibility audit", "WCAG audit", "a11y check"
- "is this accessible", "check accessibility"
- "screen reader test", "keyboard navigation check"
- "ADA compliance", "Section 508", "EAA compliance"
- "ARIA audit", "focus management review"
- "contrast check", "target size check"
- "run axe", "check contrast ratios", "test keyboard navigation"
- "audit for disabilities"

## Severity Levels

| Severity | Definition |
|----------|-----------|
| **CRITICAL** | Users with disabilities cannot access core functionality at all |
| **HIGH** | Significant barrier; workaround exists but is burdensome |
| **MEDIUM** | Accessibility degraded but tasks completable with moderate difficulty |
| **LOW** | Minor issue or best practice enhancement |

## Supported Frameworks

- **Vanilla JS / HTML** — baseline checks for all projects
- **Angular** — CDK A11y (FocusTrap, FocusMonitor, LiveAnnouncer), angular-eslint rules, common failure patterns
- **React** — React Aria hooks, Radix UI, shadcn/ui, SPA focus management, eslint-plugin-jsx-a11y, jest-axe integration

## Standards Covered

- WCAG 2.2 Level AA (all 56 applicable success criteria)
- WAI-ARIA Authoring Practices Guide (APG) patterns
- Section 508 (US), European Accessibility Act (EAA), ADA compliance mapping

## License

MIT
