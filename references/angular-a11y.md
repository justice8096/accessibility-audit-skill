# Angular Accessibility Reference

## Angular CDK A11y Module (`@angular/cdk/a11y`)

### FocusTrap
Trap focus within modals and dialogs — required for WCAG 2.4.3 Focus Order.
```html
<div cdkTrapFocus [cdkTrapFocusAutoCapture]="true">
  <!-- Dialog content — Tab cycles only within this container -->
</div>
```
**Audit check:** Every `<dialog>`, modal overlay, and slide-out panel must use `cdkTrapFocus`.

### FocusMonitor
Track how an element received focus (keyboard, mouse, touch, programmatic).
```typescript
constructor(private focusMonitor: FocusMonitor) {}

ngAfterViewInit() {
  this.focusMonitor.monitor(this.elementRef, true)
    .subscribe(origin => {
      // origin: 'keyboard' | 'mouse' | 'touch' | 'program' | null
      // Show focus ring only for keyboard origin
    });
}
```
**Audit check:** Custom components should show focus indicators for keyboard users but may suppress them for mouse clicks.

### LiveAnnouncer
Announce dynamic content changes to screen readers — required for WCAG 4.1.3 Status Messages.
```typescript
constructor(private liveAnnouncer: LiveAnnouncer) {}

onFormSubmit() {
  this.liveAnnouncer.announce('Form submitted successfully', 'polite');
}

onError() {
  this.liveAnnouncer.announce('Error: email is required', 'assertive');
}
```
**Audit check:** Every toast notification, form submission result, loading state change, and dynamic content update should use `LiveAnnouncer`.

### InteractivityChecker
Determine if elements are focusable, tabbable, or visible.
```typescript
if (this.interactivityChecker.isFocusable(element)) {
  // safe to programmatically focus
}
```

### HighContrastModeDetector
Detect OS high contrast mode for adaptive styling.
**Audit check:** Components should remain functional and readable in high contrast mode.

## Angular Aria (17+)

Headless accessible directives implementing WAI-ARIA APG patterns:
- Handles keyboard interactions per APG spec
- Manages ARIA attributes automatically
- Handles focus management
- Screen reader support without imposing visual styling

## Common Angular A11y Failures

| Issue | Detection | Fix |
|-------|-----------|-----|
| `routerLink` without `aria-current` | Grep for `routerLinkActive` without `aria-current` | Add `[attr.aria-current]="isActive ? 'page' : null"` |
| Missing page title on route change | Check if `Title` service is used in route guards/resolvers | Use `Title.setTitle()` on every route change |
| `(click)` on non-interactive elements | Grep for `(click)` on `<div>`, `<span>`, `<li>` | Use `<button>` or add `role="button" tabindex="0" (keydown.enter)` |
| Template-driven forms without labels | Grep for `<input>` without adjacent `<label>` or `aria-label` | Add `<label [for]="inputId">` or `aria-label` |
| `*ngIf` removing content without announcement | Review dynamic content toggled by `*ngIf` | Add `aria-live="polite"` container around dynamic regions |
| Missing `role` on custom components | Check component selectors that render interactive elements | Add `host: { role: 'button' }` in `@Component` decorator |
| `mat-dialog` without `cdkTrapFocus` | Review all dialog usages | Angular Material dialogs include this by default; custom dialogs need it |

## Angular Testing

```bash
# Install angular-eslint with a11y rules
ng add @angular-eslint/schematics

# Run accessibility linting
ng lint
```

Key eslint rules to enable:
- `@angular-eslint/template/accessibility-alt-text`
- `@angular-eslint/template/accessibility-elements-content`
- `@angular-eslint/template/accessibility-label-for`
- `@angular-eslint/template/accessibility-table-scope`
- `@angular-eslint/template/accessibility-valid-aria`
- `@angular-eslint/template/click-events-have-key-events`
- `@angular-eslint/template/no-autofocus`
- `@angular-eslint/template/no-positive-tabindex`
