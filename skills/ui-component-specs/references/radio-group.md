---
component: Radio group
id-prefix: RAD
status: draft
---

# Radio group

## 1. When to use it vs alternatives

- **Radio group**: exactly one choice from 2 to about 7 options, when seeing all options helps the decision.
- **Dropdown** (`DD`): more options, or space is limited.
- **Checkbox group** (`CHK`): more than one choice allowed.
- **Switch** (`SWT`) or single checkbox: a single yes or no.
- **Segmented control** (`SEG`): compact, immediate choice among a few views or modes.

## 2. Anatomy and variants

Parts: group label, options (each with label and optional description), optional helper text, optional error text.

Variants that change which capabilities apply:

- With a preselected option vs no initial selection
- Required vs optional
- Plain labels vs options with descriptions or rich content
- With conditional content revealed by an option
- Static vs dynamic options
- Vertical vs horizontal layout

Also covers the **segmented control** variant through the **Applies when** column (`RAD-17`, `RAD-18`). If a segmented control switches panels, it is tabs: use `tabs.md`.

## 3. States

Unselected, selected, hover, focus, disabled option, disabled group, read-only, error.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Tab / Shift+Tab | Enters the group on the selected option (or the first when none is selected), and leaves it in one step |
| ArrowDown / ArrowRight | Moves to the next option and selects it, wraps at the end |
| ArrowUp / ArrowLeft | Moves to the previous option and selects it, wraps at the start |
| Space | Selects the focused option if it is not selected |

In right-to-left layout the horizontal arrows are mirrored.

## 5. Component-specific accessibility

- The group has an accessible name and each option has its own.
- Selected state and position in the group are exposed.
- Required, helper and error text are associated with the group.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| RAD-01 | Exactly one option is selected at a time | Always | Required | Usually provided by primitives |
| RAD-02 | The group has a name | Always | Required | Application's job |
| RAD-03 | Arrow keys move and select; the group is a single tab stop | Always | Required | Usually provided by primitives |
| RAD-04 | The initial selection is a deliberate choice; a way to return to no selection exists when the choice is optional | Always | Required | Application's job |
| RAD-05 | Required validation with an associated error message | Required | If applicable | Application's job |
| RAD-06 | Disabled options are skipped by arrow keys and cannot be selected | Can be disabled | If applicable | Usually provided by primitives |
| RAD-07 | The label is part of the activation target | Always | Required | Application's job |
| RAD-08 | Form value: the selected option is submitted; reset restores the initial state | Inside a form | Required | Application's job |
| RAD-09 | The selection is retained after a failed submit | Inside a form | Required | Application's job |
| RAD-10 | A long option list is reconsidered: switch to a dropdown or keep the group usable | More than about 7 options | If applicable | Application's job |
| RAD-11 | Conditional content appears with the selected option and handles entered data on change | Conditional content | If applicable | Application's job |
| RAD-12 | Focus is visible, state is not shown by color alone, contrast and target size are sufficient | Always | Required | Application's job |
| RAD-13 | Options with descriptions stay associated with their option | Rich options | If applicable | Application's job |
| RAD-14 | When options change, a selected option that disappears is handled explicitly | Dynamic options | If applicable | Application's job |
| RAD-15 | Arrow key direction is correct in right-to-left layout | Always | Required | Usually provided by primitives |
| RAD-16 | Long labels wrap and stay aligned | Always | Required | Application's job |
| RAD-17 | A segmented control exposes the right meaning: a single choice of a value, or a switch between views, each with the right semantics and keyboard behavior | Segmented control | If applicable | Application's job |
| RAD-18 | Segments fit or reflow on small viewports, icon-only segments are named, the selected one is not shown by color alone, and one is always selected | Segmented control | If applicable | Application's job |

## 7. Anti-patterns

- Preselecting an option that hides a default the user may not notice, for consequential choices.
- Radios with no way to deselect when the choice is optional.
- Every radio being its own tab stop.
- Only the small circle being activatable.
- Radio group used for a list of 15 options.
- Different groups sharing one name by accident.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| RAD-01 | Functional | Always | Exclusive selection | Select one option, then another | Only the latest is selected | Required | Automatable | Critical |
| RAD-02 | Accessibility | Always | Group name | Inspect the group with a screen reader | Name announced when entering the group | Required | Manual | Critical |
| RAD-03 | Keyboard | Always | Arrow navigation | Tab into the group, use each arrow key, tab out | One tab stop, arrows move and select, wraps at ends | Required | Automatable | Critical |
| RAD-04 | States | Always | Initial selection | Render with and without an initial selection; try to return to none | Behavior matches the decision, no hidden selection | Required | Automatable | Important |
| RAD-05 | Validation | Required | Required validation | Submit with no selection | Error shown and associated with the group | If applicable | Automatable | Critical |
| RAD-06 | Keyboard | Can be disabled | Disabled options | Move through options past a disabled one, try to select it | Skipped, not selectable, visibly disabled | If applicable | Automatable | Important |
| RAD-07 | Functional | Always | Label target | Activate the label text | Option selected | Required | Automatable | Important |
| RAD-08 | Data | Inside a form | Form value | Submit, reset the form | Selected value submitted, reset restores the initial state | Required | Automatable | Critical |
| RAD-09 | Data | Inside a form | Retained selection | Fail validation on submit | Selection unchanged | Required | Automatable | Important |
| RAD-10 | Layout | More than about 7 options | Long option lists | Render with many options on a small viewport | Still usable, or replaced by a dropdown | If applicable | Manual | Nice-to-have |
| RAD-11 | Functional | Conditional content | Conditional content | Select an option with revealed content, enter data, change option, return | Content shown for the selected option, data handling defined and consistent | If applicable | Automatable | Important |
| RAD-12 | Accessibility | Always | Focus, contrast, target | Tab through, view in grayscale, use a touch device | Focus visible, state readable without color, target large enough | Required | Manual | Important |
| RAD-13 | Accessibility | Rich options | Descriptions | Focus an option with a description using a screen reader | Description is read with the option | If applicable | Manual | Important |
| RAD-14 | Data | Dynamic options | Disappearing selection | Remove the selected option from the list | Selection cleared or flagged explicitly, form value consistent | If applicable | Automatable | Important |
| RAD-15 | Keyboard | Always | Right-to-left | Switch to right-to-left layout and use the horizontal arrows | Direction mirrored | Required | Automatable | Important |
| RAD-16 | Layout | Always | Long labels | Use very long labels | Wrap, alignment intact | Required | Automatable | Nice-to-have |
| RAD-17 | Accessibility | Segmented control | A segmented control exposes the right meaning: a single choice of a value, or a switch between views, each with the right semantics and keyboard behavior | Inspect and operate by keyboard and with a screen reader | Semantics match the purpose, arrow keys move and select | If applicable | Manual | Critical |
| RAD-18 | Layout | Segmented control | Segments fit or reflow on small viewports, icon-only segments are named, the selected one is not shown by color alone, and one is always selected | Narrow the viewport, view in grayscale, inspect icon-only segments | Fits, named, selected state clear | If applicable | Automatable | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
