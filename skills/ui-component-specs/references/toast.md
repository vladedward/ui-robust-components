---
component: Toast / snackbar
id-prefix: TST
status: draft
---

# Toast / snackbar

## 1. When to use it vs alternatives

- **Toast**: brief, non-blocking feedback about something that just happened (saved, copied, sent).
- **Inline message or alert** (`ALR`): feedback tied to a place on the page, or anything that must stay until acted on.
- **Dialog** (`DLG`): when the user must decide.
- **Validation message** (`VAL`): errors next to the field.

Information the user must act on or cannot lose is never toast-only.

## 2. Anatomy and variants

Parts: container region, message, optional icon, optional action, optional dismiss action.

Variants that change which capabilities apply:

- Severity: info, success, warning, error
- With or without an action (for example undo)
- Auto-dismissing vs persistent
- Single vs stacked

## 3. States

Entering, visible, paused (hover or focus), dismissing, removed. Queued when over the limit.

## 4. Behavior and keyboard interaction

The toast appears without taking focus, is announced, auto-dismisses after enough time unless paused, and can be dismissed.

| Key | Result |
|---|---|
| Tab | Reaches the action and dismiss controls of a visible toast in a logical order |
| Escape | Dismisses the focused toast, where the pattern defines it |

## 5. Component-specific accessibility

- Messages are announced through a live region without moving focus. Errors are more assertive than confirmations.
- The time to read and act is sufficient (WCAG 2.2.1), and timing can be paused.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| TST-01 | A toast appears without moving focus | Always | Required | Usually provided by primitives |
| TST-02 | The message is announced to assistive technology, with urgency matching severity | Always | Required | Usually provided by primitives |
| TST-03 | Auto-dismiss time is long enough for the message length and any action | Auto-dismissing | Required | Application's job |
| TST-04 | The timer pauses while hovered or focused and resumes afterward | Auto-dismissing | Required | Usually provided by primitives |
| TST-05 | It can be dismissed manually by pointer and keyboard | Always | Required | Application's job |
| TST-06 | An action in a toast is keyboard reachable and still available long enough | Toast with action | If applicable | Application's job |
| TST-07 | Several toasts stack in a defined order with a limit, a queue and removal of duplicates | Several toasts | Required | Application's job |
| TST-08 | Toasts behave deliberately across navigation (persist or clear) | Navigation possible | If applicable | Application's job |
| TST-09 | Severity is conveyed by text or icon with a name, not by color alone | Always | Required | Application's job |
| TST-10 | Long messages wrap within a maximum width | Always | Required | Application's job |
| TST-11 | Toasts do not cover essential controls, and respect safe areas and open dialogs | Always | Required | Application's job |
| TST-12 | A keyboard shortcut or region lets keyboard users reach toasts that contain actions | Toast with action | If applicable | Application's job |
| TST-13 | Reduced motion is respected | Animated | If applicable | Application's job |
| TST-14 | Errors that need action also exist in a persistent place | Error toast | Required | Application's job |
| TST-15 | A burst of toasts does not flood the screen or lose announcements | Many events | If applicable | Application's job |
| TST-16 | The timer does not run out while the page is hidden | Auto-dismissing | Optional | Application's job |
| TST-17 | Usable at 200% zoom and in right-to-left layout | Always | Required | Application's job |

## 7. Anti-patterns

- Disappearing after a fixed two seconds regardless of content.
- Moving focus to the toast.
- Error or required information only in a toast.
- Undo action that vanishes before it can be reached with the keyboard.
- Toast timer that keeps running while the user is reading or hovering.
- Unlimited stacking.
- Announcing the same message twice or not at all.
- Toast covering the primary action of the page.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| TST-01 | Keyboard | Always | No focus change | Trigger a toast while focus is on a control | Focus does not move | Required | Automatable | Critical |
| TST-02 | Accessibility | Always | Announcement | Trigger an info and an error toast with a screen reader | Message announced, error more urgent | Required | Manual | Critical |
| TST-03 | Functional | Auto-dismissing | Duration | Show a short and a long message, one with an action | Time scales with content and action | Required | Automatable | Important |
| TST-04 | Functional | Auto-dismissing | Pause | Hover, then focus a toast near its end | Timer paused, resumes afterward | Required | Automatable | Critical |
| TST-05 | Keyboard | Always | Manual dismissal | Dismiss with the pointer and with the keyboard | Toast removed, focus remains logical | Required | Automatable | Important |
| TST-06 | Keyboard | Toast with action | Action | Reach the action with the keyboard before it dismisses | Action works, toast still available | If applicable | Automatable | Critical |
| TST-07 | Functional | Several toasts | Stacking | Trigger more toasts than the limit, and the same one repeatedly | Order defined, limit held, queue works, duplicates handled | Required | Automatable | Important |
| TST-08 | Functional | Navigation possible | Navigation | Trigger a toast, change page | Behavior matches the decision | If applicable | Automatable | Important |
| TST-09 | Accessibility | Always | Severity cues | View each severity in grayscale | Severity clear without color | Required | Manual | Important |
| TST-10 | Layout | Always | Long messages | Use a very long message and an unbroken string | Wraps within the maximum width | Required | Automatable | Nice-to-have |
| TST-11 | Layout | Always | Placement | Show toasts with essential controls, on small viewports and with a dialog open | Nothing essential covered, visible above the dialog if intended | Required | Manual | Important |
| TST-12 | Keyboard | Toast with action | Keyboard access | Use the defined way to reach toasts | Toast reachable without the pointer | If applicable | Automatable | Important |
| TST-13 | Accessibility | Animated | Reduced motion | Enable the reduced motion preference | Animation reduced or removed | If applicable | Manual | Nice-to-have |
| TST-14 | Data | Error toast | Persistent error | Trigger an error that needs action | The information also exists somewhere persistent | Required | Manual | Critical |
| TST-15 | Functional | Many events | Burst | Trigger many events at once | Screen not flooded, announcements not lost | If applicable | Automatable | Nice-to-have |
| TST-16 | Functional | Auto-dismissing | Hidden page | Hide the page while a toast is shown and return | Toast still there when the user returns | Optional | Manual | Nice-to-have |
| TST-17 | Layout | Always | Zoom and direction | Check at 200% zoom and in right-to-left layout | Nothing clipped, placement mirrored | Required | Manual | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
