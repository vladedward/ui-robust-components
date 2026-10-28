---
component: Accordion / collapsible
id-prefix: ACC
status: draft
---

# Accordion / collapsible

## 1. When to use it vs alternatives

- **Accordion**: several sections of content where users usually need only one or two, such as FAQs or settings groups.
- **Collapsible (single)**: one optional section of detail.
- **Tabs** (`TAB`): peer views where one is always shown.
- **Plain headings and text**: when most users need all the content.

## 2. Anatomy and variants

Parts: header (a control inside a heading), panel, optional icon, optional group.

Variants that change which capabilities apply:

- Only one section open at a time vs several open
- Initially all closed vs some open
- Static vs lazy loaded or dynamic content
- With sections that can be disabled
- Opened from a link to content inside it

## 3. States

Collapsed, expanded, hover, focus, disabled, loading content.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Tab / Shift+Tab | Moves between headers and focusable content in open panels |
| Enter / Space | Expands or collapses the focused section |
| ArrowDown / ArrowUp, Home / End | Optionally move between headers |

## 5. Component-specific accessibility

- Each header is a control inside a heading of the right level and exposes expanded state.
- A collapsed panel is hidden from assistive technology and the tab order.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| ACC-01 | The header expands and collapses its panel by pointer and keyboard, with the expanded state exposed | Always | Required | Usually provided by primitives |
| ACC-02 | The header is a control inside a heading at the right level | Always | Required | Application's job |
| ACC-03 | The open rule is defined: one at a time closes the other, or several can be open | Always | Required | Usually provided by primitives |
| ACC-04 | Arrow, Home and End navigation between headers | Several headers | Optional | Usually provided by primitives |
| ACC-05 | A collapsed panel is not reachable by keyboard or assistive technology | Always | Required | Usually provided by primitives |
| ACC-06 | The initial open sections are defined, and a link or search hit to inner content opens its panel | Initial state or deep linking | If applicable | Application's job |
| ACC-07 | Disabled sections cannot be toggled and are perceivable | Can be disabled | If applicable | Usually provided by primitives |
| ACC-08 | Lazy or dynamic content shows loading and failure, and the panel height adapts | Dynamic content | If applicable | Application's job |
| ACC-09 | Collapsing a panel that contains focus moves focus to its header | Always | Required | Application's job |
| ACC-10 | Animation respects reduced motion | Animated | Required | Application's job |
| ACC-11 | Long titles wrap, and the state is not shown by an icon alone | Always | Required | Application's job |
| ACC-12 | Data entered in a collapsed panel is kept | Panels hold inputs | Required | Application's job |

## 7. Anti-patterns

- A header that is a clickable block with no keyboard support.
- Collapsed panels still in the tab order.
- Everything hidden in an accordion although users need it all.
- Focus lost when the panel that contains it collapses.
- Clearing form data when a panel collapses.
- An expand icon that does not reflect the state.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| ACC-01 | Keyboard | Always | Toggle | Toggle with pointer, Enter and Space | Panel opens and closes, expanded state follows | Required | Automatable | Critical |
| ACC-02 | Accessibility | Always | Heading and control | Inspect the accessibility tree | Control inside a heading at the right level | Required | Automatable | Important |
| ACC-03 | Functional | Always | Open rule | Open several sections in turn | As defined: one closes the other, or several stay open | Required | Automatable | Critical |
| ACC-04 | Keyboard | Several headers | Header navigation | Use arrows, Home and End | Focus moves between headers | Optional | Automatable | Nice-to-have |
| ACC-05 | Accessibility | Always | Hidden content | Tab through and inspect with a screen reader when collapsed | Collapsed content skipped and hidden | Required | Automatable | Critical |
| ACC-06 | Functional | Initial state or deep linking | Initial state and links | Load with and without a link to inner content | Right sections open, the target is visible | If applicable | Automatable | Important |
| ACC-07 | States | Can be disabled | Disabled sections | Try to toggle a disabled section | Unchanged, visibly disabled | If applicable | Automatable | Important |
| ACC-08 | Data | Dynamic content | Dynamic content | Open a slowly loading and a failing panel | Loading, error and correct height | If applicable | Automatable | Important |
| ACC-09 | Keyboard | Always | Focus on collapse | Focus a control in a panel and collapse it | Focus moves to the header, not lost | Required | Automatable | Important |
| ACC-10 | Accessibility | Animated | Reduced motion | Enable the reduced motion preference | Animation reduced or removed | Required | Manual | Nice-to-have |
| ACC-11 | Layout | Always | Long titles and indicator | Use a very long title, view in grayscale | Wraps, state clear without an icon alone | Required | Automatable | Nice-to-have |
| ACC-12 | Data | Panels hold inputs | Kept data | Enter data, collapse, expand, submit | Data kept | Required | Automatable | Critical |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
