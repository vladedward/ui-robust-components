---
component: Popover
id-prefix: POP
status: draft
---

# Popover

> Shares dismissal, focus return and positioning behavior with `dialog.md` and `dropdown.md`. Also verify those where the popover blocks the page or holds a list.

## 1. When to use it vs alternatives

- **Popover**: supplementary content or controls anchored to a trigger, opened on activation, that does not block the page (filters, details, a small form, a color picker).
- **Tooltip** (`TIP`): a short, non-interactive hint on hover and focus.
- **Menu** (`MNU`): a list of actions.
- **Dialog** (`DLG`): content that must be dealt with before continuing.
- **Inline expansion**: content that is better always visible.

## 2. Anatomy and variants

Parts: trigger, popover container, content, optional arrow, optional close action.

Variants that change which capabilities apply:

- Informational (no interactive content) vs interactive content
- Non-modal vs modal-like (traps focus and blocks the page)
- Opened by activation only vs also by hover
- One at a time vs several open

## 3. States

Closed, open, positioning (opening), hover and focus on trigger, content loading.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Enter / Space on the trigger | Opens or closes the popover |
| Tab | Continues in a logical order; leaving the popover closes it unless it is modal-like |
| Escape | Closes the popover, focus returns to the trigger |

## 5. Component-specific accessibility

- The trigger exposes expanded state and what it controls.
- The popover has a name and a role that match its content.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| POP-01 | Open and close by activating the trigger, with the expanded state exposed | Always | Required | Usually provided by primitives |
| POP-02 | Escape closes the popover and returns focus to the trigger | Always | Required | Usually provided by primitives |
| POP-03 | Interacting outside closes the popover without side effects | Non-modal | Required | Usually provided by primitives |
| POP-04 | Focus moves into interactive content on open; informational content keeps focus on the trigger; Tab order stays logical | Always | Required | Usually provided by primitives |
| POP-05 | Role, name and relationship with the trigger are exposed | Always | Required | Usually provided by primitives |
| POP-06 | The popover is fully visible: flips and shifts near edges, is not clipped, follows the trigger on scroll and resize | Always | Required | Application's job |
| POP-07 | All interactive content is keyboard reachable, and a hover-opened popover is also operable by keyboard | Interactive content or hover | Required | Application's job |
| POP-08 | Only one popover is open at a time, and nested ones dismiss from the innermost outward | Several popovers | If applicable | Usually provided by primitives |
| POP-09 | It closes when the trigger is removed, or the page changes, and is handled on scroll | Always | Required | Application's job |
| POP-10 | Content that changes size repositions the popover, and tall content scrolls inside it | Dynamic content | Required | Application's job |
| POP-11 | On small viewports it fits the screen or becomes an equivalent surface | Always | Required | Application's job |
| POP-12 | It is stacked correctly, including above or inside a dialog | Always | Required | Application's job |
| POP-13 | A modal-like popover traps focus and makes the page inert | Modal-like | If applicable | Usually provided by primitives |
| POP-14 | Rapid open and close leaves a consistent state | Always | Required | Application's job |

## 7. Anti-patterns

- A hover-only popover with interactive content.
- Focus left behind on the trigger while the user fills a form inside the popover.
- A popover that stays open after the trigger is removed.
- A popover cut off by an overflow container.
- Essential information that is only reachable inside a popover opened by hover.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| POP-01 | Functional | Always | Open and close | Activate the trigger twice, by pointer and keyboard | Opens then closes, expanded state follows | Required | Automatable | Critical |
| POP-02 | Keyboard | Always | Escape | Open, press Escape | Closed, focus on the trigger | Required | Automatable | Critical |
| POP-03 | Functional | Non-modal | Outside interaction | Interact outside | Closed, no side effects | Required | Automatable | Important |
| POP-04 | Keyboard | Always | Focus on open | Open with interactive and informational content, press Tab | Focus enters interactive content, tab order logical | Required | Automatable | Critical |
| POP-05 | Accessibility | Always | Exposed semantics | Inspect and use a screen reader | Name, role and relationship exposed | Required | Manual | Important |
| POP-06 | Layout | Always | Positioning | Open at each viewport edge, inside a clipping container, while scrolling and resizing | Fully visible, follows the trigger | Required | Automatable | Critical |
| POP-07 | Keyboard | Interactive content or hover | Keyboard access | Reach and use every control without a pointer | Fully operable | Required | Automatable | Critical |
| POP-08 | Functional | Several popovers | Single and nested | Open a second popover, open a nested one, press Escape | Only one open, nested closes first | If applicable | Automatable | Important |
| POP-09 | Functional | Always | Cleanup | Remove the trigger, change the page, scroll while open | Closes or follows as decided, nothing orphaned | Required | Automatable | Important |
| POP-10 | Layout | Dynamic content | Size changes | Add content while open, use tall content | Repositions, scrolls inside | Required | Automatable | Important |
| POP-11 | Layout | Always | Small viewports | Use a narrow viewport and a real device | Fits the screen, usable | Required | Manual | Important |
| POP-12 | Layout | Always | Stacking | Open above content and inside a dialog | Above the right layers | Required | Automatable | Important |
| POP-13 | Keyboard | Modal-like | Modal behavior | Tab through and interact outside | Focus trapped, page inert | If applicable | Automatable | Important |
| POP-14 | Functional | Always | Rapid toggling | Open and close repeatedly | Consistent state | Required | Automatable | Nice-to-have |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
