---
component: Drawer / sheet
id-prefix: DRW
status: draft
---

# Drawer / sheet

> Same behavior family as `dialog.md`. Where the drawer is modal, also verify the dialog capabilities that apply (initial focus, containment, focus return, unsaved changes, async submit, nesting). The cases below add what is specific to a drawer.

## 1. When to use it vs alternatives

- **Drawer or sheet**: a longer task or detail view opened from an edge, where the page context stays partly visible (edit details, filters, a cart).
- **Dialog** (`DLG`): a short decision or form in the center.
- **Popover** (`POP`): small anchored content.
- **Sidebar** (`SID`): persistent navigation.
- **A separate page**: content that needs its own URL or is a full flow.

## 2. Anatomy and variants

Parts: panel, optional backdrop, header with title and close action, body, optional footer with actions, optional handle.

Variants that change which capabilities apply:

- Modal vs non-modal (page remains usable)
- Edge: start, end, top, bottom
- Overlay vs one that pushes the page content
- Touch gestures (swipe, drag handle) vs none
- Fixed width vs resizable

## 3. States

Closed, opening, open, closing, loading content, submitting, error, dragging (touch).

## 4. Behavior and keyboard interaction

As a dialog: Escape closes, Tab cycles inside a modal drawer, focus returns on close.

## 5. Component-specific accessibility

- Role, name and modal state are exposed.
- A modal drawer makes the page behind inert for assistive technology.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| DRW-01 | On open focus moves inside, Escape closes, and focus returns to what opened it | Always | Required | Usually provided by primitives |
| DRW-02 | A modal drawer makes the page inert and stops page scrolling, a non-modal one keeps the page usable | Always | Required | Usually provided by primitives |
| DRW-03 | A visible close action exists, and backdrop behavior is deliberate and protects unsaved input | Always | Required | Application's job |
| DRW-04 | Touch gestures to dismiss have an equivalent without gestures | Swipe or drag | If applicable | Application's job |
| DRW-05 | Size and position suit the viewport: width limits, full width on small viewports, safe areas | Always | Required | Application's job |
| DRW-06 | Long content scrolls inside the body while the header and footer stay reachable | Always | Required | Application's job |
| DRW-07 | Unsaved changes are protected on close | Form content | If applicable | Application's job |
| DRW-08 | A dialog or drawer opened from a drawer stacks correctly and closes in order | Nested overlays | If applicable | Usually provided by primitives |
| DRW-09 | A drawer that pushes content re-lays out the page without overlap or lost scroll | Push drawer | If applicable | Application's job |
| DRW-10 | Role, name and modal state are exposed | Always | Required | Usually provided by primitives |
| DRW-11 | Opening and closing animation respects reduced motion, and an interrupted animation leaves a consistent state | Always | Required | Application's job |
| DRW-12 | The edge and gestures are mirrored in right-to-left layout | Always | Required | Application's job |
| DRW-13 | Asynchronous content shows loading and failure with retry | Async content | If applicable | Application's job |
| DRW-14 | The drawer is stacked correctly relative to headers, notifications and other overlays | Always | Required | Application's job |

## 7. Anti-patterns

- A drawer that cannot be closed without a gesture.
- A modal drawer where the page behind can still be tabbed to.
- A full-height drawer that hides its own footer actions on a small viewport.
- A swipe that closes a drawer holding unsaved input.
- Opening and closing rapidly leaving the page scroll locked.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| DRW-01 | Keyboard | Always | Focus and Escape | Open, press Escape | Focus moved in, then closed and returned | Required | Automatable | Critical |
| DRW-02 | Functional | Always | Modal vs non-modal | Interact with the page behind in each mode | Inert and locked when modal, usable otherwise | Required | Automatable | Critical |
| DRW-03 | Functional | Always | Close and backdrop | Use each way to close, with entered data | Deliberate behavior, no silent data loss | Required | Automatable | Important |
| DRW-04 | Functional | Swipe or drag | Gesture alternative | Close without gestures, then with | Both work | If applicable | Manual | Important |
| DRW-05 | Layout | Always | Size and position | Use small and large viewports, with safe areas | Fits, actions reachable | Required | Manual | Important |
| DRW-06 | Layout | Always | Long content | Use long content on a short viewport, zoom to 200% | Body scrolls, header and footer reachable | Required | Automatable | Critical |
| DRW-07 | Functional | Form content | Unsaved changes | Enter data, then close | Confirmation asked | If applicable | Automatable | Important |
| DRW-08 | Keyboard | Nested overlays | Nesting | Open an overlay from the drawer, press Escape | Only the top overlay closes | If applicable | Automatable | Important |
| DRW-09 | Layout | Push drawer | Pushing | Open and close with page content and scroll position | No overlap, scroll kept | If applicable | Automatable | Important |
| DRW-10 | Accessibility | Always | Exposed semantics | Inspect and use a screen reader | Role, name, modal state exposed | Required | Manual | Critical |
| DRW-11 | Functional | Always | Animation | Enable reduced motion, open and close rapidly | Reduced, consistent final state | Required | Automatable | Important |
| DRW-12 | Layout | Always | Right-to-left | Switch to right-to-left layout | Edge and gestures mirrored | Required | Manual | Important |
| DRW-13 | Data | Async content | Async content | Load slowly and with a failure | Loading and retry shown | If applicable | Automatable | Important |
| DRW-14 | Layout | Always | Stacking | Open with sticky headers and notifications | Correct layering | Required | Automatable | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
