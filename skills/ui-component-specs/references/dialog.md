---
component: Dialog / modal
id-prefix: DLG
status: draft
---

# Dialog / modal

## 1. When to use it vs alternatives

- **Modal dialog**: a short task or decision that must be completed or dismissed before the user continues (confirmation, small form).
- **Non-modal dialog or popover** (`POP`): supplementary content that must not block the page.
- **Drawer / sheet** (`DRW`): longer tasks that keep page context visible.
- **Inline content or a separate page**: long forms, multi-step flows, anything that needs its own URL.
- **Toast** (`TST`): feedback that needs no decision.

## 2. Anatomy and variants

Parts: backdrop, dialog container, title, optional description, body, actions, close action.

Variants that change which capabilities apply:

- Modal vs non-modal
- Informational, confirmation, destructive confirmation, form
- Short vs long content
- Opened by a user action vs opened programmatically
- Single vs nested dialogs
- With async submit

## 3. States

Closed, open, opening and closing (animated), submitting, error inside the dialog, disabled actions. Hover and focus on its controls.

## 4. Behavior and keyboard interaction

Opening moves focus inside, closing returns it. The page behind cannot be interacted with while a modal dialog is open.

| Key | Result |
|---|---|
| Tab / Shift+Tab | Cycles through focusable elements inside the dialog only |
| Escape | Closes the dialog, or asks for confirmation when closing would lose data |
| Enter | Activates the focused control; submits a form dialog |

## 5. Component-specific accessibility

- The dialog has a role, an accessible name from its title, and a description where useful.
- A modal dialog makes the content behind it unreachable for assistive technology as well.
- Destructive confirmations use the alert dialog semantics.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| DLG-01 | On open, focus moves into the dialog to a deliberate element | Always | Required | Usually provided by primitives |
| DLG-02 | Focus stays inside a modal dialog | Modal | Required | Usually provided by primitives |
| DLG-03 | Escape closes the dialog | Always | Required | Usually provided by primitives |
| DLG-04 | On close, focus returns to the element that opened it, or a logical fallback when it no longer exists | Always | Required | Usually provided by primitives |
| DLG-05 | The page behind is inert and does not scroll; no layout shift when the scrollbar disappears | Modal | Required | Usually provided by primitives |
| DLG-06 | Role, accessible name, description and modal state are exposed | Always | Required | Usually provided by primitives |
| DLG-07 | Interacting with the backdrop has a deliberate, consistent behavior, and never closes a dialog holding unsaved input without protection | Modal | Required | Application's job |
| DLG-08 | A visible close action exists | Always | Required | Application's job |
| DLG-09 | Long content scrolls inside the dialog, title and actions stay reachable, fits small viewports and 200% zoom | Always | Required | Application's job |
| DLG-10 | Destructive confirmation: specific action labels, safest action as the initial focus | Destructive action | If applicable | Application's job |
| DLG-11 | Unsaved changes are protected on close | Form dialog | If applicable | Application's job |
| DLG-12 | Nested dialogs stack correctly: Escape closes only the top one, focus returns down the chain | Nested dialogs | If applicable | Usually provided by primitives |
| DLG-13 | Async submit shows progress, prevents double submit, keeps the dialog open with an error on failure | Async submit | If applicable | Application's job |
| DLG-14 | Usable on mobile: fits the viewport, not hidden by the on-screen keyboard or safe areas | Always | Required | Application's job |
| DLG-15 | Opened programmatically without a trigger, focus and return are still sensible | Opened programmatically | If applicable | Application's job |
| DLG-16 | The dialog is stacked above sticky headers, other overlays and notifications as intended | Always | Required | Application's job |
| DLG-17 | The dialog closes or stays consistent on route change and the browser back action | Navigation possible while open | If applicable | Application's job |
| DLG-18 | Opening and closing animation respects reduced motion | Animated | Optional | Application's job |
| DLG-19 | Non-modal dialogs keep the page usable and have their own dismissal and focus rules | Non-modal | If applicable | Application's job |

## 7. Anti-patterns

- Focus stays on the trigger behind the backdrop.
- No focus return, so keyboard users restart from the top of the page.
- Backdrop click discards a half-filled form.
- Dialog taller than the viewport with no internal scroll.
- Generic "OK" and "Cancel" on a destructive confirmation.
- Page behind still scrolls or is reachable with Tab.
- Dialog used for long multi-step flows.
- Dialog rendered inside a container that clips it or puts it under another layer.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| DLG-01 | Keyboard | Always | Initial focus | Open the dialog | Focus is on a deliberate element inside it | Required | Automatable | Critical |
| DLG-02 | Keyboard | Modal | Focus containment | Press Tab and Shift+Tab repeatedly | Focus cycles inside the dialog, never reaches the page behind | Required | Automatable | Critical |
| DLG-03 | Keyboard | Always | Escape | Press Escape | Dialog closes (or asks to confirm when data would be lost) | Required | Automatable | Critical |
| DLG-04 | Keyboard | Always | Focus return | Close the dialog by each available means, including when the trigger was removed | Focus returns to the trigger, or a logical fallback | Required | Automatable | Critical |
| DLG-05 | Layout | Modal | Inert page and scroll lock | Try to scroll and interact with the page behind | No interaction, no scrolling, no layout shift | Required | Automatable | Important |
| DLG-06 | Accessibility | Always | Exposed semantics | Inspect the accessibility tree, use a screen reader | Role, name and description exposed, background hidden from assistive technology | Required | Manual | Critical |
| DLG-07 | Functional | Modal | Backdrop behavior | Interact with the backdrop with and without entered data | Behavior is the deliberate one, no data lost silently | Required | Automatable | Important |
| DLG-08 | Functional | Always | Close action | Look for and use the close action | Present, reachable, closes the dialog | Required | Automatable | Important |
| DLG-09 | Layout | Always | Long content | Fill the dialog with content taller than a small viewport, zoom to 200% | Body scrolls, title and actions stay reachable | Required | Automatable | Critical |
| DLG-10 | Functional | Destructive action | Destructive confirmation | Open a destructive confirmation | Action labels are specific, safest action focused first | If applicable | Automatable | Critical |
| DLG-11 | Functional | Form dialog | Unsaved changes | Enter data, then close by each means | The user is asked to confirm before data is discarded | If applicable | Automatable | Important |
| DLG-12 | Keyboard | Nested dialogs | Nested dialogs | Open a dialog from a dialog, press Escape, close the second | Only the top dialog closes each time, focus returns to the right element | If applicable | Automatable | Important |
| DLG-13 | Functional | Async submit | Async submit | Submit slowly, submit twice, make it fail | Progress shown, one submission, dialog stays open with an error on failure | If applicable | Automatable | Critical |
| DLG-14 | Layout | Always | Mobile | Open on a small viewport and a real device with the keyboard shown | Fits, actions reachable, nothing hidden | Required | Manual | Important |
| DLG-15 | Keyboard | Opened programmatically | Programmatic open | Open without a user action, then close | Focus lands inside, and on close goes to a logical element | If applicable | Automatable | Important |
| DLG-16 | Layout | Always | Stacking | Open with sticky headers and notifications present | Dialog above them as intended | Required | Automatable | Important |
| DLG-17 | Functional | Navigation possible while open | Navigation | Trigger route change and the back action while open | Dialog state consistent with the decision, no orphaned scroll lock | If applicable | Automatable | Important |
| DLG-18 | Accessibility | Animated | Reduced motion | Enable the reduced motion preference | Animation reduced or removed | Optional | Manual | Nice-to-have |
| DLG-19 | Functional | Non-modal | Non-modal behavior | Interact with the page while the dialog is open | Page stays usable, dismissal and focus rules hold | If applicable | Automatable | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
