# Framework Accessibility Check

Run targeted accessibility checks using framework-specific patterns and best practices.

## Parameters

- **target** (required): Path to the component or module to check
- **framework** (required): Framework to check — angular or react

## Angular Checks

- Angular CDK A11y module usage (FocusMonitor, FocusTrap, LiveAnnouncer)
- angular-eslint a11y rules compliance
- Material component ARIA attribute usage
- Template-driven form label associations

## React Checks

- React Aria hooks usage (useButton, useFocusRing, useListBox)
- Radix UI / shadcn/ui accessible primitive usage
- SPA focus management on route changes (react-router-dom)
- jest-axe test coverage for component accessibility

## Output

Framework-specific findings with before/after code examples and library recommendations.
