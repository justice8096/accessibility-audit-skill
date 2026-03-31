# LLM Compliance & Transparency Report
## accessibility-audit-skill

**Report Date**: 2026-03-31
**Auditor**: LLM Governance & Compliance Team
**Project**: accessibility-audit-skill (Claude-assisted development)
**Framework**: EU AI Act Art. 25, OWASP LLM Top 10 2025, NIST SP 800-218A
**Audit Type**: INITIAL

---

## Executive Summary

**Overall LLM Compliance Score: 76/100 — GOOD**

The accessibility-audit-skill demonstrates strong transparency and consent practices but has gaps in supply chain documentation, bias assessment, and formal incident response procedures. As a markdown-based skill (no executable code), many traditional risk categories are inherently low-risk. The primary compliance concerns are around supply chain governance (no SBOM, no signed commits, no CI/CD) and the absence of formal bias/accuracy measurement for the skill's audit output.

---

## Compliance Dimensions

### Dimension 1: System Transparency — 90/100

The project excels at AI transparency:
- README.md explicitly states this is "a comprehensive WCAG 2.2 Level AA accessibility audit skill for Claude"
- Git history attributes both commits with clear authorship (justice8096 as committer, Claude as generator)
- SKILL.md's report template includes "Auditor: Claude (automated)" in every generated report
- The skill description discloses AI involvement throughout

**Regulatory mapping:** EU AI Act Art. 52 (Transparency) — COMPLIANT. NIST AI RMF MAP 1.1 — COMPLIANT.

**Gap:** No per-file AI attribution comments in the markdown files themselves.

### Dimension 2: Training Data Disclosure — 80/100

The skill references specific standards and frameworks:
- WCAG 2.2 Level AA criteria (all 56 applicable success criteria enumerated)
- WAI-ARIA Authoring Practices Guide patterns
- Angular CDK A11y module documentation
- React Aria, Radix UI, shadcn/ui documentation
- eslint-plugin-jsx-a11y and angular-eslint rule sets

**Regulatory mapping:** EU AI Act Art. 53 — MOSTLY COMPLIANT. NIST AI RMF MEASURE 2.6 — MOSTLY COMPLIANT.

**Gap:** No version dates on referenced frameworks. WCAG 2.2 was finalized Oct 2023 — the skill should note which version it targets and when references were last verified.

### Dimension 3: Risk Classification — 85/100

The skill uses a well-defined 4-tier severity system (CRITICAL/HIGH/MEDIUM/LOW) consistent with industry standards:
- Each finding maps to specific WCAG criterion numbers
- Severity definitions align with user impact (CRITICAL = "cannot access core functionality at all")
- CWE mapping analysis found all 5 identified CWEs correctly classified

**Regulatory mapping:** EU AI Act Art. 25 — COMPLIANT. NIST SP 800-53 RA-3 — COMPLIANT.

**Gap:** No documented false positive/negative rates for the skill's detection heuristics.

### Dimension 4: Supply Chain Security — 45/100

This is the weakest dimension, per the supply chain audit:
- No SBOM (CycloneDX or SPDX)
- No signed commits (GPG signing configured in .gitconfig but not used for this repo)
- No CI/CD pipeline or automated validation
- No release versioning or git tags
- No branch protection or code review policy
- No dependency monitoring for referenced external tools

**Regulatory mapping:** NIST SP 800-218A — NON-COMPLIANT. SLSA v1.0 — Level 1 (achievable L2 with signing + CI). ISO 27001 A.15 — PARTIAL.

**Remediation:** See supply-chain-audit.md for the full 10-item roadmap.

### Dimension 5: Consent & Authorization — 90/100

Excellent user control model:
- The skill is entirely opt-in (Claude invokes it only when the user requests an accessibility audit)
- No destructive operations — the skill analyzes code and generates reports
- User controls what code is shared for audit
- Skill instructions explicitly state it generates markdown reports, not code modifications
- No automatic execution of remediation — fixes are proposed, not applied

**Regulatory mapping:** EU AI Act Art. 14 — COMPLIANT. NIST AI RMF GOVERN 1.2 — COMPLIANT.

### Dimension 6: Sensitive Data Handling — 75/100

The skill handles this reasonably well:
- No secrets or credentials in the repository
- .gitignore excludes audit output files (preventing accidental commit of proprietary audit data)
- CWE mapping identified CWE-200 (Information Exposure) as MEDIUM risk — users may share proprietary source code during audits

**Regulatory mapping:** GDPR Art. 5 — PARTIAL (no explicit data minimization guidance). NIST SP 800-53 SC-28 — PARTIAL.

**Gap:** SKILL.md should include a warning that users may be sharing proprietary code during audits and that audit reports may contain sensitive code snippets.

### Dimension 7: Incident Response — 70/100

The skill has a built-in remediation workflow:
- Every finding includes concrete remediation code
- Severity classification enables triage
- Remediation Roadmap provides prioritized action plan
- The skill supports re-audit to verify fixes

**Regulatory mapping:** NIST SP 800-53 IR-4 — PARTIAL. ISO 27001 A.16 — PARTIAL.

**Gap:** No SECURITY.md or vulnerability disclosure process for the skill itself. No documented procedure for when the skill produces incorrect audit findings.

### Dimension 8: Bias Assessment — 70/100

The skill covers multiple frameworks (Angular, React, vanilla JS) and disability types:
- WCAG 2.2 covers visual, auditory, motor, and cognitive disabilities
- Framework references cover Angular CDK and React Aria equally
- Eval test cases span all three supported frameworks

**Regulatory mapping:** EU AI Act Art. 10 — PARTIAL. NIST AI RMF MEASURE 2.11 — PARTIAL.

**Gap:** No documented false positive/negative rates. No acknowledgment of detection gaps (e.g., the skill can't test color contrast from source code alone, can't verify screen reader behavior, can't assess cognitive load). No coverage metrics for WCAG 2.2 criteria that are inherently manual-judgment.

---

## Score Summary

| Dimension | Score | Status |
|-----------|-------|--------|
| System Transparency | 90 | EXCELLENT |
| Training Data Disclosure | 80 | GOOD |
| Risk Classification | 85 | GOOD |
| Supply Chain Security | 45 | NEEDS IMPROVEMENT |
| Consent & Authorization | 90 | EXCELLENT |
| Sensitive Data Handling | 75 | GOOD |
| Incident Response | 70 | GOOD |
| Bias Assessment | 70 | GOOD |
| **Overall** | **76** | **GOOD** |

---

## Recommendations

1. **Create SBOM and enable commit signing** — immediate action to bring Supply Chain from 45 to 70+ (see supply-chain-audit.md roadmap)
2. **Add SECURITY.md** with vulnerability disclosure process and scope statement
3. **Add data handling warning** to SKILL.md about proprietary code exposure during audits
4. **Document detection limitations** — which WCAG criteria can vs cannot be assessed from code alone
5. **Add version dates** to all framework references (WCAG 2.2, Angular CDK, React Aria versions)

## Next Audit

Recommended after implementing supply chain improvements — target 2 weeks.
