---
component: Checkbox
id-prefix: CHK
status: draft
---

# Checkbox

## 1. When to use it vs alternatives

- **Single checkbox**: a yes or no choice submitted with a form (consent, "remember me").
- **Checkbox group**: zero or more choices from a short list.
- **Switch** (`SWT`): an on or off setting that takes effect immediately.
- **Radio group**: exactly one choice.
- **Multi-select dropdown**: the list is long.

## 2. Anatomy and variants

Parts: box, label, optional helper text, optional group label, optional error text.

Variants that change which capabilities apply:

- Single vs group
- Group with a parent option (select all) vs without
- Required single (consent) vs at least one required in a group
- With conditional content revealed by a choice

## 3. States

Unchecked, checked, indeterminate (mixed), hover, focus, disabled, read-only, error.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Space | Toggles the focused checkbox |
| Tab / Shift+Tab | Moves between checkboxes, each one is a tab stop |

Activating the box or its label gives the same result.

## 5. Component-specific accessibility

- Each checkbox has an accessible name; a group has a name for the whole group.
- Checked, unchecked and mixed states are exposed.
- Required, error and helper text are associated with the checkbox or group.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| CHK-01 | Toggle by pointer and by keyboard | Always | Required | Usually provided by primitives |
| CHK-02 | The label is associated and is part of the activation target | Always | Required | Application's job |
| CHK-03 | Checked, unchecked and mixed states are exposed programmatically | Always | Required | Usually provided by primitives |
| CHK-04 | A parent option shows a mixed state when only some children are checked, and activating it resolves to a defined state | Parent option present | If applicable | Application's job |
| CHK-05 | A group has a name for the whole group | Group | If applicable | Application's job |
| CHK-06 | Select all and clear all actions | Group | Optional | Application's job |
| CHK-07 | Required validation: single consent or at least one in a group, with an associated error message | Required | If applicable | Application's job |
| CHK-08 | Disabled state for one option and for the whole group | Can be disabled | Required | Usually provided by primitives |
| CHK-09 | Form value: only checked options are submitted, with the right value; reset restores the initial state | Inside a form | Required | Application's job |
| CHK-10 | Initial state is retained after a failed submit | Inside a form | Required | Application's job |
| CHK-11 | Long labels wrap and stay aligned with the box | Always | Required | Application's job |
| CHK-12 | Focus is visible, state is not shown by color alone, contrast is sufficient | Always | Required | Application's job |
| CHK-13 | Target size is large enough | Always | Required | Application's job |
| CHK-14 | Rapid toggling and externally controlled state never desynchronize the display and the value | Always | Required | Application's job |
| CHK-15 | Conditional content appears and disappears with the choice, without losing entered data unexpectedly | Conditional content | If applicable | Application's job |

## 7. Anti-patterns

- Custom checkbox built from a generic element without state exposure.
- Only the small box is activatable, the label is not.
- Using checkboxes for mutually exclusive choices.
- Parent option that cannot show a mixed state.
- Consent checkbox pre-checked.
- Immediate side effects with no feedback.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| CHK-01 | Keyboard | Always | Toggle | Toggle with the pointer, then with Space | State flips each time | Required | Automatable | Critical |
| CHK-02 | Functional | Always | Label target | Activate the label text | State flips | Required | Automatable | Important |
| CHK-03 | Accessibility | Always | Exposed state | Inspect the state in each of the three states | Checked, unchecked and mixed are exposed | Required | Automatable | Critical |
| CHK-04 | States | Parent option present | Mixed state | Check some children only, then activate the parent, twice | Parent shows mixed, then resolves to all checked, then to none (or defined behavior) | If applicable | Automatable | Important |
| CHK-05 | Accessibility | Group | Group name | Inspect the group with a screen reader | Group name announced when entering the group | If applicable | Manual | Important |
| CHK-06 | Functional | Group | Select all | Trigger select all and clear all | All checked, then none, disabled options handled as defined | Optional | Automatable | Nice-to-have |
| CHK-07 | Validation | Required | Required validation | Submit unchecked | Error shown, associated with the checkbox or group, focus handling defined | If applicable | Automatable | Critical |
| CHK-08 | States | Can be disabled | Disabled | Tab and try to toggle disabled options and a disabled group | Not changeable, not submitted, visibly disabled | Required | Automatable | Important |
| CHK-09 | Data | Inside a form | Form value | Submit with some checked, then reset | Only checked values submitted, reset restores the initial state | Required | Automatable | Critical |
| CHK-10 | Data | Inside a form | Retained state | Fail validation on submit | Choices unchanged | Required | Automatable | Important |
| CHK-11 | Layout | Always | Long labels | Use a very long label | Wraps, box stays aligned with the first line | Required | Automatable | Nice-to-have |
| CHK-12 | Accessibility | Always | Focus and contrast | Tab through, check each state in grayscale | Focus visible, state readable without color | Required | Manual | Important |
| CHK-13 | Layout | Always | Target size | Measure the target, use a touch device | Large enough to hit reliably | Required | Manual | Important |
| CHK-14 | Functional | Always | Consistency | Toggle rapidly, then change the state from outside the component | Display and form value always agree | Required | Automatable | Important |
| CHK-15 | Functional | Conditional content | Conditional content | Check, enter data in the revealed content, uncheck, check again | Content appears and hides, data handling defined and consistent | If applicable | Automatable | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
