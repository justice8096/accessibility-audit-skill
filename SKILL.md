---
name: accessibility-audit
description: "Run a comprehensive WCAG 2.2 accessibility audit on a web application, component library, or design system. Generates a structured audit report with severity-based findings (CRITICAL/HIGH/MEDIUM/LOW), evidence collection, remediation guidance, and framework-specific fixes for Angular and React. Use this skill whenever the user mentions: 'accessibility audit', 'WCAG audit', 'a11y check', 'is this accessible', 'check accessibility', 'screen reader test', 'keyboard navigation check', 'ADA compliance', 'Section 508', 'EAA compliance', 'ARIA audit', 'focus management review', 'contrast check', 'target size check', or any request to evaluate a UI, component, page, or application for accessibility compliance. Also trigger when the user asks to 'run axe', 'check contrast ratios', 'test keyboard navigation', or 'audit for disabilities'. This skill should run proactively when the user shares a URL, screenshot, or component code that involves user-facing UI."
---

# Accessibility Audit Skill

A comprehensive WCAG 2.2 accessibility audit tool that mirrors the evidence-collection approach from the LLMCompliance pipeline: structured templates, severity-based validation, auto-extraction where possible, and human judgment for the rest.

## Audit Philosophy

This audit follows the same principles as the AI Compliance Evidence Collection Kit:

1. **Extract before asking** — run automated tools first (axe-core, Lighthouse, contrast checkers), then ask for human judgment only on what automation can't catch
2. **Severity-based findings** — not all issues are equal. CRITICAL blocks users entirely; LOW is a polish item
3. **Evidence-based** — every finding includes the specific WCAG criterion, the element/component affected, and reproduction steps
4. **Remediation-ready** — every finding includes a concrete fix, not just a description of the problem

## Audit Report Structure

ALWAYS generate the audit report using this exact template structure. Save as a markdown file.

```markdown
# Accessibility Audit Report

> **Project:** [name]
> **Audit Date:** [YYYY-MM-DD]
> **Auditor:** Claude (automated) + [human reviewer if applicable]
> **Standard:** WCAG 2.2 Level AA
> **Scope:** [what was audited — pages, components, flows]

## Metadata
- **Framework:** [Angular/React/Vanilla/etc.]
- **Testing Tools Used:** [axe-core, Lighthouse, manual keyboard, screen reader, etc.]
- **Pages/Components Audited:** [count and list]
- **Conformance Target:** WCAG 2.2 Level AA

---

## Executive Summary

[2-3 sentences: overall conformance posture, number of findings by severity, most critical blockers]

### Findings Summary

| Severity | Count | Auto-Detected | Manual-Found |
|----------|-------|---------------|--------------|
| CRITICAL | X     | X             | X            |
| HIGH     | X     | X             | X            |
| MEDIUM   | X     | X             | X            |
| LOW      | X     | X             | X            |
| **Total**| **X** | **X**         | **X**        |

### Conformance by Principle

| Principle | Pass | Fail | N/A |
|-----------|------|------|-----|
| Perceivable (1.x) | X | X | X |
| Operable (2.x) | X | X | X |
| Understandable (3.x) | X | X | X |
| Robust (4.x) | X | X | X |

---

## Findings

### CRITICAL Findings

> CRITICAL = Users with disabilities cannot access core functionality at all.

#### F-001: [Short title]
- **WCAG Criterion:** [number and name, e.g., 2.1.1 Keyboard]
- **Severity:** CRITICAL
- **Category:** [Perceivable | Operable | Understandable | Robust]
- **Element/Component:** [specific selector, component name, or page area]
- **Description:** [what the problem is]
- **Impact:** [who is affected and how — e.g., "Screen reader users cannot navigate the main menu"]
- **Reproduction Steps:**
  1. [step]
  2. [step]
- **Evidence:** [screenshot ref, axe-core rule ID, Lighthouse audit ID, or manual test result]
- **Remediation:**
  ```[language]
  // concrete code fix
  ```
- **Effort Estimate:** [S/M/L]
- **Affects Templates:** [if applicable — maps to compliance templates like the LLMCompliance system]

[Repeat for each CRITICAL finding]

### HIGH Findings
> HIGH = Significant barrier for users with disabilities; workaround may exist but is burdensome.

[Same structure as CRITICAL]

### MEDIUM Findings
> MEDIUM = Accessibility degraded but users can still complete tasks with moderate difficulty.

[Same structure as CRITICAL]

### LOW Findings
> LOW = Minor issue; best practice violation or enhancement opportunity.

[Same structure as CRITICAL but Reproduction Steps and Evidence can be abbreviated]

---

## WCAG 2.2 Criterion Checklist

Evaluate every applicable criterion. Use this checklist format:

### 1. Perceivable

| # | Criterion | Level | Status | Finding Ref |
|---|-----------|-------|--------|-------------|
| 1.1.1 | Non-text Content | A | PASS/FAIL/N-A | F-XXX |
| 1.3.1 | Info and Relationships | A | PASS/FAIL/N-A | |
| 1.3.2 | Meaningful Sequence | A | PASS/FAIL/N-A | |
| 1.3.3 | Sensory Characteristics | A | PASS/FAIL/N-A | |
| 1.3.4 | Orientation | AA | PASS/FAIL/N-A | |
| 1.3.5 | Identify Input Purpose | AA | PASS/FAIL/N-A | |
| 1.4.1 | Use of Color | A | PASS/FAIL/N-A | |
| 1.4.2 | Audio Control | A | PASS/FAIL/N-A | |
| 1.4.3 | Contrast (Minimum) | AA | PASS/FAIL/N-A | |
| 1.4.4 | Resize Text | AA | PASS/FAIL/N-A | |
| 1.4.5 | Images of Text | AA | PASS/FAIL/N-A | |
| 1.4.10 | Reflow | AA | PASS/FAIL/N-A | |
| 1.4.11 | Non-text Contrast | AA | PASS/FAIL/N-A | |
| 1.4.12 | Text Spacing | AA | PASS/FAIL/N-A | |
| 1.4.13 | Content on Hover or Focus | AA | PASS/FAIL/N-A | |

### 2. Operable

| # | Criterion | Level | Status | Finding Ref |
|---|-----------|-------|--------|-------------|
| 2.1.1 | Keyboard | A | PASS/FAIL/N-A | |
| 2.1.2 | No Keyboard Trap | A | PASS/FAIL/N-A | |
| 2.1.4 | Character Key Shortcuts | A | PASS/FAIL/N-A | |
| 2.2.1 | Timing Adjustable | A | PASS/FAIL/N-A | |
| 2.2.2 | Pause, Stop, Hide | A | PASS/FAIL/N-A | |
| 2.3.1 | Three Flashes | A | PASS/FAIL/N-A | |
| 2.4.1 | Bypass Blocks | A | PASS/FAIL/N-A | |
| 2.4.2 | Page Titled | A | PASS/FAIL/N-A | |
| 2.4.3 | Focus Order | A | PASS/FAIL/N-A | |
| 2.4.4 | Link Purpose (In Context) | A | PASS/FAIL/N-A | |
| 2.4.5 | Multiple Ways | AA | PASS/FAIL/N-A | |
| 2.4.6 | Headings and Labels | AA | PASS/FAIL/N-A | |
| 2.4.7 | Focus Visible | AA | PASS/FAIL/N-A | |
| 2.4.11 | Focus Not Obscured (Min) | AA | PASS/FAIL/N-A | |
| 2.5.1 | Pointer Gestures | A | PASS/FAIL/N-A | |
| 2.5.2 | Pointer Cancellation | A | PASS/FAIL/N-A | |
| 2.5.3 | Label in Name | A | PASS/FAIL/N-A | |
| 2.5.4 | Motion Actuation | A | PASS/FAIL/N-A | |
| 2.5.7 | Dragging Movements | AA | PASS/FAIL/N-A | |
| 2.5.8 | Target Size (Minimum) | AA | PASS/FAIL/N-A | |

### 3. Understandable

| # | Criterion | Level | Status | Finding Ref |
|---|-----------|-------|--------|-------------|
| 3.1.1 | Language of Page | A | PASS/FAIL/N-A | |
| 3.1.2 | Language of Parts | AA | PASS/FAIL/N-A | |
| 3.2.1 | On Focus | A | PASS/FAIL/N-A | |
| 3.2.2 | On Input | A | PASS/FAIL/N-A | |
| 3.2.3 | Consistent Navigation | AA | PASS/FAIL/N-A | |
| 3.2.4 | Consistent Identification | AA | PASS/FAIL/N-A | |
| 3.2.6 | Consistent Help | A | PASS/FAIL/N-A | |
| 3.3.1 | Error Identification | A | PASS/FAIL/N-A | |
| 3.3.2 | Labels or Instructions | A | PASS/FAIL/N-A | |
| 3.3.3 | Error Suggestion | AA | PASS/FAIL/N-A | |
| 3.3.4 | Error Prevention (Legal) | AA | PASS/FAIL/N-A | |
| 3.3.7 | Redundant Entry | A | PASS/FAIL/N-A | |
| 3.3.8 | Accessible Authentication | AA | PASS/FAIL/N-A | |

### 4. Robust

| # | Criterion | Level | Status | Finding Ref |
|---|-----------|-------|--------|-------------|
| 4.1.2 | Name, Role, Value | A | PASS/FAIL/N-A | |
| 4.1.3 | Status Messages | AA | PASS/FAIL/N-A | |

---

## Remediation Roadmap

| Priority | Finding | Effort | Sprint Target |
|----------|---------|--------|---------------|
| 1 | F-001: [title] | S/M/L | Sprint N |
| 2 | F-002: [title] | S/M/L | Sprint N |

---

## Testing Methodology

### Automated Testing
- [ ] axe-core scan (via browser extension or CI integration)
- [ ] Lighthouse accessibility audit
- [ ] Color contrast analyzer

### Keyboard Testing
- [ ] Tab through all interactive elements
- [ ] Verify visible focus indicators on all focused elements
- [ ] Verify no keyboard traps
- [ ] Verify all functionality operable via keyboard alone
- [ ] Test Enter/Space activation on buttons and links
- [ ] Test arrow key navigation in menus, tabs, radio groups

### Screen Reader Testing
- [ ] NVDA (Windows) / VoiceOver (macOS) walkthrough
- [ ] Verify all images have appropriate alt text
- [ ] Verify form labels announced correctly
- [ ] Verify dynamic content changes announced via aria-live
- [ ] Verify landmarks navigable

### Visual Testing
- [ ] Zoom to 400% — no horizontal scrolling
- [ ] High contrast mode — all elements visible
- [ ] prefers-reduced-motion respected

---

## Evidence Checklist

- [ ] Automated scan results attached (axe-core JSON or Lighthouse report)
- [ ] All CRITICAL findings have reproduction steps
- [ ] All findings have WCAG criterion references
- [ ] All findings have concrete remediation code
- [ ] Keyboard navigation test completed
- [ ] Screen reader test completed (at least one reader)
- [ ] Color contrast verified for all text
- [ ] Zoom test completed (200% and 400%)
- [ ] Legal compliance mapping noted (ADA, EAA, Section 508)

---

## Version History

| Date | Version | Author | Changes |
|------|---------|--------|---------|
| [date] | 1.0 | [author] | Initial audit |
```

## Audit Execution Process

Follow this sequence when running an audit:

### Phase 1: Automated Extraction
Run automated tools first — they catch ~30-40% of issues instantly.

1. If you have access to the live page via browser tools, run axe-core or Lighthouse
2. If auditing source code, inspect for:
   - Missing `alt` attributes on `<img>` elements
   - Missing `<label>` associations on form inputs
   - Missing landmark roles (`<main>`, `<nav>`, `<header>`, `<footer>`)
   - Missing `lang` attribute on `<html>`
   - Hardcoded color values without sufficient contrast
   - Missing `aria-label`/`aria-labelledby` on interactive custom components
   - Click handlers on non-interactive elements (`<div onClick>`)
   - Missing keyboard event handlers alongside mouse handlers
   - Missing `aria-live` regions for dynamic content

### Phase 2: Framework-Specific Checks
Read the appropriate reference file based on the project's framework:
- For Angular projects: read `references/angular-a11y.md`
- For React projects: read `references/react-a11y.md`

### Phase 3: Manual / Human-Judgment Checks
These cannot be automated and require actually experiencing the interface:
- Logical reading order and heading hierarchy
- Meaningful link text in context
- Appropriate use of ARIA (not over-ARIA'd)
- Cognitive load and plain language
- Error message helpfulness
- Color-only information conveyance
- Animation and motion appropriateness
- Touch target adequacy on mobile

### Phase 4: Report Generation
1. Compile all findings into the report template above
2. Assign severity: CRITICAL > HIGH > MEDIUM > LOW
3. Fill the WCAG criterion checklist
4. Generate the remediation roadmap ordered by severity then effort
5. Save the report as `Accessibility-Audit-Report-[project]-[date].md`

## Severity Classification Guide

| Severity | Definition | Examples |
|----------|-----------|---------|
| **CRITICAL** | Users with disabilities cannot access core functionality at all | No keyboard access to primary navigation; form submits with no error feedback to screen readers; entire page section invisible to assistive tech |
| **HIGH** | Significant barrier; workaround exists but is burdensome | Focus not visible on important controls; images of text with no alternative; complex widget missing ARIA roles |
| **LOW** | Minor issue or best practice enhancement | Redundant ARIA on native HTML elements; slightly below-ideal (but passing) contrast; missing `autocomplete` attributes |
| **MEDIUM** | Accessibility degraded but tasks completable with moderate difficulty | Heading hierarchy skips levels; inconsistent focus styles; missing skip link; status messages not announced |

## Mapping to Compliance Frameworks

When the audit is for a project that also uses the LLMCompliance evidence collection system, map findings to the relevant compliance templates:

| Accessibility Area | Compliance Template | Connection |
|-------------------|-------------------|------------|
| User-facing disclosures | T02 User-Facing Disclosure | Disclosures must be accessible to users with disabilities |
| Consent mechanisms | T10 Consent Records | Consent UX must meet WCAG for valid informed consent |
| Human oversight interfaces | T09 Human Oversight | Override controls must be keyboard-operable |
| Incident reporting UI | T13 Incident Management | Reporting interfaces must be accessible |
| Content labeling | T03 Content Labeling | AI content labels must be perceivable by assistive tech |
| Risk dashboards | T06 Impact/Risk Assessment | Assessment tools used by compliance teams must be accessible |

## Important: Data Handling

When running an audit, be aware that:
- Users may share **proprietary source code** — audit reports will contain code snippets from the audited project
- Generated reports may reveal **architectural patterns and security-sensitive implementation details**
- Advise users to **review audit reports before sharing** them publicly or committing to open repositories
- This skill **analyzes code but never executes it** — all assessment is static analysis and pattern matching against known accessibility anti-patterns

## Detection Limitations

This skill cannot fully assess all WCAG 2.2 criteria from source code alone. The following require live testing or human judgment that static analysis cannot replace:

| What This Skill CAN Detect | What Requires Live/Manual Testing |
|---------------------------|----------------------------------|
| Missing `alt` attributes | Whether `alt` text is *meaningful* (not just present) |
| Missing `aria-label`/`aria-labelledby` | Whether labels make sense in context |
| Missing landmark roles | Whether landmark structure is *logical* |
| `outline: none` without replacement | Actual contrast ratios of focus indicators |
| Missing `lang` attribute | Correct language identification for multilingual content |
| Click handlers without keyboard handlers | Actual keyboard navigation flow and tab order |
| Missing `aria-live` regions | Whether live region announcements are *useful* and not noisy |
| Heading level skips | Whether heading hierarchy makes semantic sense |
| Missing `autocomplete` attributes | N/A — fully detectable from code |
| Color values in CSS | Precise contrast ratio calculation (needs computed styles) |
| Missing `prefers-reduced-motion` | Whether animations are actually distracting |
| Double-click / hover-only interactions | Touch target sizes on actual rendered layout |

**Always recommend live testing** (keyboard walkthrough, screen reader testing with NVDA/VoiceOver, contrast analyzer, zoom testing) alongside this code-level audit. The Testing Methodology checklist in the report template covers these manual checks.

## Standards Versions

This skill targets the following standard versions (last verified 2026-03-31):

| Standard | Version | Date |
|----------|---------|------|
| WCAG | 2.2 | W3C Recommendation, Oct 2023 |
| WAI-ARIA APG | 1.2 | W3C Note, ongoing updates |
| Angular CDK A11y | 17+ | Angular v17-v19 compatible |
| React Aria | 3.x | Adobe, React 18+ compatible |
| Radix UI | 1.x | Radix Primitives |
| eslint-plugin-jsx-a11y | 6.x | npm |
| @angular-eslint | 17+ | npm |
| axe-core | 4.x | Deque Systems |
| Section 508 | Revised 2018 | US Access Board |
| European Accessibility Act | Directive 2019/882 | Enforcement from June 2025 |
