# Run Accessibility Audit

Execute a comprehensive WCAG 2.2 Level AA accessibility audit using the 4-phase process.

## Parameters

- **target** (required): Path to the file, component, or URL to audit
- **framework** (optional): Frontend framework — vanilla, angular, or react (default: vanilla)
- **severity_threshold** (optional): Minimum severity — CRITICAL, HIGH, MEDIUM, LOW (default: LOW)
- **include_checklist** (optional): Include full WCAG 2.2 checklist (default: true)

## Process

1. **Automated Extraction** — Scan source for semantic HTML, ARIA attributes, color contrast, focus management
2. **Framework-Specific Checks** — Apply Angular CDK A11y or React Aria patterns if framework specified
3. **Manual/Human-Judgment Checks** — Flag items requiring human review (alt text quality, reading order, cognitive load)
4. **Report Generation** — Produce structured markdown report with findings grouped by severity

## Output

Structured markdown report containing:
- Executive summary with conformance level
- Findings grouped by severity (CRITICAL → LOW) with CWE references
- Full WCAG 2.2 criterion checklist (if enabled)
- Remediation roadmap with effort estimates
- Evidence checklist for compliance documentation
