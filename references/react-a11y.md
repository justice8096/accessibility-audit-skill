# React Accessibility Reference

## JSX ARIA Support

React supports all ARIA attributes natively in JSX. Unlike most React DOM properties which are camelCase, ARIA attributes use hyphen-case exactly as in HTML:

```jsx
<button aria-label="Close dialog" aria-expanded={isOpen}>
  <Icon name="x" />
</button>
```

## React Aria (Adobe) — Headless Accessible Hooks

The gold standard for accessible React components. Provides hooks implementing WAI-ARIA APG patterns with zero visual styling.

```bash
npm install react-aria react-stately
```

Key hooks:
- `useButton` — keyboard, focus, press handling
- `useDialog` — focus trap, escape dismiss, ARIA roles
- `useComboBox` — autocomplete with keyboard nav
- `useListBox` — single/multi select with type-ahead
- `useMenu` / `useMenuTrigger` — APG menu pattern
- `useSlider` — range input with ARIA value announcements
- `useTabs` — tab panel pattern with arrow key nav
- `useTooltip` — hover/focus tooltip with proper ARIA
- `useFocusRing` — visible focus indicator management

**Audit check:** If the project uses React Aria, most APG patterns are handled correctly. Audit the *usage* — are the hooks being called with correct props?

## Radix UI — Accessible Primitives

Unstyled, composable accessible components:
```jsx
import * as Dialog from '@radix-ui/react-dialog';

<Dialog.Root>
  <Dialog.Trigger>Open</Dialog.Trigger>
  <Dialog.Portal>
    <Dialog.Overlay />
    <Dialog.Content>
      <Dialog.Title>Edit Profile</Dialog.Title>
      <Dialog.Description>Make changes here.</Dialog.Description>
      <Dialog.Close>Save</Dialog.Close>
    </Dialog.Content>
  </Dialog.Portal>
</Dialog.Root>
```

**Audit check:** Verify `Dialog.Title` and `Dialog.Description` are always present — they provide the accessible name and description.

## shadcn/ui

Built on Radix + Tailwind. Accessibility comes from Radix; Tailwind adds styling. Audit points:
- Focus ring styles use `focus-visible:` variant (keyboard-only focus indicators)
- Color contrast of Tailwind theme values must meet WCAG thresholds
- Custom variants may override Radix's built-in ARIA handling

## Common React A11y Failures

| Issue | Detection | Fix |
|-------|-----------|-----|
| `<div onClick>` without keyboard | Grep for `onClick` on non-interactive elements | Use `<button>` or add `role="button" tabIndex={0} onKeyDown` |
| Missing route change announcements | Check if SPA route changes are announced | Add a visually-hidden live region that announces page title on route change |
| Missing `useId()` for ARIA relationships | Check `aria-labelledby`/`aria-describedby` with hardcoded IDs | Use `React.useId()` (React 18+) for unique IDs |
| `autoFocus` on mount | Grep for `autoFocus` prop | Remove — manage focus programmatically with `useEffect` + `ref.current.focus()` |
| Missing `<label>` on form inputs | Grep for `<input>` without `<label>` or `aria-label` | Add `<label htmlFor={id}>` or `aria-label` |
| `aria-hidden="true"` on focusable elements | Check for focusable children inside `aria-hidden` containers | Remove from tab order or restructure DOM |
| Images without `alt` | Grep for `<img` without `alt` | Add descriptive `alt` or `alt=""` for decorative |
| Lists rendered without `<ul>`/`<ol>` | Check mapped arrays rendering `<div>` lists | Use semantic `<ul>` with `<li>` children |
| Error messages not associated | Check form validation errors | Use `aria-describedby` pointing to error element ID |
| Dynamic content not announced | Check toast/notification systems | Wrap in `aria-live="polite"` region or use `role="alert"` |

## Focus Management in SPAs

React SPAs don't get browser-native focus management on navigation. This is the #1 accessibility failure in React apps.

```jsx
// Route change focus management
import { useEffect, useRef } from 'react';
import { useLocation } from 'react-router-dom';

function useFocusOnRouteChange() {
  const location = useLocation();
  const mainRef = useRef<HTMLElement>(null);

  useEffect(() => {
    // Focus the main content area on route change
    mainRef.current?.focus();

    // Announce the new page to screen readers
    const title = document.title;
    const announcer = document.getElementById('route-announcer');
    if (announcer) announcer.textContent = title;
  }, [location.pathname]);

  return mainRef;
}

// In layout:
<main ref={mainRef} tabIndex={-1} style={{ outline: 'none' }}>
  {children}
</main>
<div id="route-announcer" role="status" aria-live="polite" className="sr-only" />
```

**Audit check:** Every React SPA must have a focus management strategy for route changes.

## React Testing for Accessibility

```bash
# Install eslint plugin
npm install eslint-plugin-jsx-a11y --save-dev

# Install testing library with a11y queries
npm install @testing-library/jest-dom @testing-library/react --save-dev

# Install axe-core for integration tests
npm install @axe-core/react --save-dev  # dev overlay
npm install jest-axe --save-dev          # jest integration
```

### eslint-plugin-jsx-a11y Rules (enable all)

Critical rules:
- `jsx-a11y/alt-text` — images must have alt
- `jsx-a11y/anchor-has-content` — links must have text
- `jsx-a11y/aria-props` — valid ARIA attributes
- `jsx-a11y/aria-role` — valid ARIA roles
- `jsx-a11y/click-events-have-key-events` — onClick needs onKeyDown
- `jsx-a11y/heading-has-content` — headings must have text
- `jsx-a11y/interactive-supports-focus` — interactive elements must be focusable
- `jsx-a11y/label-has-associated-control` — labels must be associated
- `jsx-a11y/no-noninteractive-element-interactions` — no click on div/span
- `jsx-a11y/no-static-element-interactions` — no handlers on static elements
- `jsx-a11y/role-has-required-aria-props` — roles must have required ARIA

### jest-axe Integration Test

```jsx
import { render } from '@testing-library/react';
import { axe, toHaveNoViolations } from 'jest-axe';

expect.extend(toHaveNoViolations);

test('MyComponent has no accessibility violations', async () => {
  const { container } = render(<MyComponent />);
  const results = await axe(container);
  expect(results).toHaveNoViolations();
});
```

**Audit check:** Does the project have jest-axe tests? If not, flag as HIGH — automated a11y testing in CI prevents regressions.
