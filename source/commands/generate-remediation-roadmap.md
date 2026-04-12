# Generate Remediation Roadmap

Create a prioritized remediation plan from accessibility audit findings.

## Parameters

- **findings_path** (required): Path to the audit findings file or report
- **sprint_capacity** (optional): Developer hours per sprint (default: 40)
- **compliance_target** (optional): Target standard — WCAG-AA, Section-508, EAA (default: WCAG-AA)

## Process

1. Parse findings and classify by severity and WCAG principle
2. Identify quick wins (high impact, low effort)
3. Group related fixes into sprint-sized work packages
4. Map fixes to compliance requirements
5. Estimate effort and assign sprint targets

## Output

Markdown roadmap with:
- Quick wins list (fixes completable in under 2 hours)
- Sprint-by-sprint remediation plan with effort estimates
- Compliance coverage progress tracker
- Dependency graph for fixes that must be sequenced
