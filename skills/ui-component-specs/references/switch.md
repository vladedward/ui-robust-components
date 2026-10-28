---
component: Switch / toggle
id-prefix: SWT
status: draft
---

# Switch / toggle

## 1. When to use it vs alternatives

- **Switch**: an on or off setting that takes effect immediately, like a light switch.
- **Checkbox** (`CHK`): a yes or no choice submitted later with a form, or part of a list of choices.
- **Toggle button**: a button whose pressed state changes what is shown (see `button.md`).
- **Radio group** (`RAD`): more than two states.
- Never use a switch to trigger an action or to collect consent.

## 2. Anatomy and variants

Parts: track and thumb, label, optional on and off text, optional helper text.

Variants that change which capabilities apply:

- Immediate effect vs applied on form submit
- Local state vs state saved on a server (asynchronous)
- With or without visible on and off text

## 3. States

Off, on, hover, focus, disabled, read-only, pending (saving), error (save failed).

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Space | Toggles the switch |
| Enter | Toggles the switch where the pattern allows it |
| Tab | Moves focus in and out |

## 5. Component-specific accessibility

- The switch exposes a switch role, its name and its on or off state.
- The label names the setting, never the state.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| SWT-01 | Toggle by pointer and keyboard | Always | Required | Usually provided by primitives |
| SWT-02 | Role, name and state are exposed | Always | Required | Usually provided by primitives |
| SWT-03 | The label is associated and part of the activation target | Always | Required | Application's job |
| SWT-04 | The effect model is clear: an immediate change is confirmed to the user, a deferred change is clearly part of a form | Always | Required | Application's job |
| SWT-05 | On and off are distinguishable without color alone and with sufficient contrast | Always | Required | Application's job |
| SWT-06 | Disabled and read-only states | Can be disabled | Required | Usually provided by primitives |
| SWT-07 | While a change is being saved, the pending state is shown, further toggling is handled, and a failure restores the previous state with an error | Async save | If applicable | Application's job |
| SWT-08 | The initial state reflects the stored value, and reset restores it | Always | Required | Application's job |
| SWT-09 | Rapid toggling leaves the display, the value and the stored setting consistent | Always | Required | Application's job |
| SWT-10 | The label describes the setting, and does not read ambiguously with the state | Always | Required | Application's job |
| SWT-11 | Right-to-left layout and reduced motion are respected | Always | Required | Application's job |
| SWT-12 | Target size is large enough | Always | Required | Application's job |

## 7. Anti-patterns

- A switch that needs a "Save" button but looks immediate.
- A switch whose label changes with the state ("Enable" when off).
- Showing the new state before the save succeeds and never reverting.
- On and off shown only by color.
- A switch used to run an action or give legal consent.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| SWT-01 | Keyboard | Always | Toggle | Toggle with the pointer and with Space | State flips each time | Required | Automatable | Critical |
| SWT-02 | Accessibility | Always | Exposed semantics | Inspect with a screen reader | Role, name and state announced | Required | Manual | Critical |
| SWT-03 | Functional | Always | Label target | Activate the label | State flips | Required | Automatable | Important |
| SWT-04 | Functional | Always | Effect model | Toggle and observe the feedback, and the form submission | Immediate change confirmed, or deferred change submitted with the form | Required | Automatable | Critical |
| SWT-05 | Accessibility | Always | Visual states | View in grayscale and check contrast | On and off distinct without color | Required | Manual | Important |
| SWT-06 | States | Can be disabled | Disabled and read-only | Try to toggle in each state | Unchanged, state visible | Required | Automatable | Important |
| SWT-07 | Data | Async save | Async save | Toggle with a slow save, then a failing one | Pending shown, failure reverts with an error | If applicable | Automatable | Critical |
| SWT-08 | Data | Always | Initial state | Render with each stored value and reset | Displays the stored value, reset restores it | Required | Automatable | Important |
| SWT-09 | Functional | Always | Rapid toggling | Toggle many times quickly | Display, value and stored setting agree | Required | Automatable | Important |
| SWT-10 | Accessibility | Always | Label wording | Review the label with the state read aloud | Unambiguous | Required | Manual | Important |
| SWT-11 | Layout | Always | Direction and motion | Right-to-left layout, reduced motion | Thumb direction mirrored, animation reduced | Required | Manual | Nice-to-have |
| SWT-12 | Layout | Always | Target size | Use a touch device | Easy to hit | Required | Manual | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
