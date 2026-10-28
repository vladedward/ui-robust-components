---
component: Button
id-prefix: BTN
status: draft
---

# Button

## 1. When to use it vs alternatives

- **Button**: performs an action on the current page (submit, open a dialog, toggle, delete).
- **Link**: navigates to another page or location. If it navigates, it is a link, even when styled like a button.
- **Toggle / switch**: a persistent on or off state.
- **Menu**: several related actions behind one control.

## 2. Anatomy and variants

Parts: label, optional icon, optional loading indicator.

Variants that change which capabilities apply:

- Text, icon with text, icon-only
- Primary, secondary, tertiary, destructive
- Submit, reset or neutral inside a form, vs outside a form
- Action with immediate side effects (async) vs purely local action
- Toggle button (exposes pressed state)

Also covers these variants through the **Applies when** column: **icon-only buttons** (`BTN-16`; sizing and name rules also in `BTN-02` and `BTN-11`) and **split buttons** (`BTN-17`, `BTN-18`). The alternatives list follows `menu.md`.

## 3. States

Default, hover, focus, active (pressed), disabled, loading, pressed (toggle). Read-only does not apply.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Enter | Activates the button on key down |
| Space | Activates the button on key up |
| Tab / Shift+Tab | Moves focus to and from the button |

Activation by pointer and by keyboard give the same result.

## 5. Component-specific accessibility

- Every button has an accessible name, including icon-only buttons.
- State changes (loading, pressed, expanded) are exposed, not only shown visually.
- A disabled button is a deliberate choice: decide whether it stays discoverable and explain why it is unavailable when the reason is not obvious.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| BTN-01 | Activation by pointer, Enter and Space | Always | Required | Usually provided by primitives |
| BTN-02 | Accessible name for every variant, including icon-only | Always | Required | Application's job |
| BTN-03 | Distinct visible states: hover, focus, pressed, disabled | Always | Required | Application's job |
| BTN-04 | A disabled button cannot be activated and is visibly disabled; the reason is available when not obvious | Can be disabled | If applicable | Application's job |
| BTN-05 | Loading state shows progress, blocks repeated activation, keeps its size and name | Async action | If applicable | Application's job |
| BTN-06 | An action with side effects runs once per intent, however fast it is activated | Action has side effects | Required | Application's job |
| BTN-07 | Destructive actions need confirmation or are undoable | Destructive action | If applicable | Application's job |
| BTN-08 | Long and localized labels wrap or grow without breaking the layout | Always | Required | Application's job |
| BTN-09 | Navigation is a link, an action is a button | Always | Required | Application's job |
| BTN-10 | Inside a form the button type is explicit and never submits by accident | Inside a form | Required | Application's job |
| BTN-11 | Target size is large enough for touch and pointer | Always | Required | Application's job |
| BTN-12 | Focus is handled after the action when the button disappears or changes | Action changes the button | If applicable | Application's job |
| BTN-13 | Toggle buttons expose their pressed state | Toggle button | If applicable | Usually provided by primitives |
| BTN-14 | States and meaning do not rely on color alone; contrast is sufficient | Always | Required | Application's job |
| BTN-15 | Loading animation respects reduced motion | Animated indicator | Optional | Application's job |
| BTN-16 | An icon-only button is named by its action, not by the icon, the name stays the same when a toggle changes state, and a tooltip is a supplement, not the name | Icon-only button | Required | Application's job |
| BTN-17 | A split button has a default action and a separate control for the alternatives, each named, with the default action usable without opening the menu | Split button | If applicable | Application's job |
| BTN-18 | The alternatives of a split button open and are chosen by keyboard, a chosen alternative changes the default only if that is defined, and a disabled part is handled | Split button | If applicable | Application's job |

## 7. Anti-patterns

- A non-button element with a click handler and no keyboard support.
- Link styled as a button for an action, or button used for navigation.
- Icon-only button with no accessible name.
- Disabling the button after click only visually while the action can still be fired.
- Loading state that changes the button width and shifts the layout.
- Removing the focused button from the page and leaving focus lost.
- Submit by default for buttons inside a form.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| BTN-01 | Keyboard | Always | Activation | Activate with the pointer, then with Enter, then with Space | Same action runs each time, exactly once | Required | Automatable | Critical |
| BTN-02 | Accessibility | Always | Accessible name | Inspect the name of each variant, including icon-only | Every button has a meaningful name | Required | Automatable | Critical |
| BTN-03 | States | Always | Visible states | Hover, focus with the keyboard, press, disable | Each state is visually distinct from default | Required | Manual | Important |
| BTN-04 | States | Can be disabled | Disabled | Try to activate a disabled button with pointer and keyboard | Nothing happens, state visible, reason available if defined | If applicable | Automatable | Important |
| BTN-05 | States | Async action | Loading | Activate and keep the action pending | Progress shown, further activation ignored, size and name unchanged, busy state exposed | If applicable | Automatable | Critical |
| BTN-06 | Functional | Action has side effects | Single execution | Activate twice quickly, and hold Enter | The action runs once | Required | Automatable | Critical |
| BTN-07 | Functional | Destructive action | Confirmation or undo | Trigger the destructive action | Confirmation requested or undo offered before the change is final | If applicable | Automatable | Critical |
| BTN-08 | Layout | Always | Long labels | Use a very long label and a label 40% longer than the original language | Layout intact, label fully readable | Required | Automatable | Important |
| BTN-09 | Accessibility | Always | Link vs button | Review each control that navigates and each that acts | Navigation uses links, actions use buttons | Required | Manual | Important |
| BTN-10 | Functional | Inside a form | Form type | Activate a neutral button inside a form | Form is not submitted unless it is the submit button | Required | Automatable | Critical |
| BTN-11 | Layout | Always | Target size | Measure the interactive area, use a touch device | Large enough to activate reliably | Required | Manual | Important |
| BTN-12 | Keyboard | Action changes the button | Focus after action | Activate an action that removes or replaces the button | Focus moves to a logical element, not lost | If applicable | Automatable | Important |
| BTN-13 | Accessibility | Toggle button | Pressed state | Toggle several times | Pressed state exposed and updated | If applicable | Automatable | Important |
| BTN-14 | Accessibility | Always | Contrast and color | Check contrast for every state, view in grayscale | Meaning preserved, contrast sufficient | Required | Manual | Important |
| BTN-15 | Accessibility | Animated indicator | Reduced motion | Enable the reduced motion preference | Animation reduced or removed | Optional | Manual | Nice-to-have |
| BTN-16 | Accessibility | Icon-only button | An icon-only button is named by its action, not by the icon, the name stays the same when a toggle changes state, and a tooltip is a supplement, not the name | Inspect the name of each icon-only button, including a toggle in both states | Name describes the action, constant across states, present without a tooltip | Required | Automatable | Critical |
| BTN-17 | Functional | Split button | A split button has a default action and a separate control for the alternatives, each named, with the default action usable without opening the menu | Activate the default action, then open the alternatives | Default runs directly, alternatives open separately, both named | If applicable | Automatable | Critical |
| BTN-18 | Keyboard | Split button | The alternatives of a split button open and are chosen by keyboard, a chosen alternative changes the default only if that is defined, and a disabled part is handled | Open by keyboard, choose an alternative, disable one part | Keyboard operable, default behavior as defined | If applicable | Automatable | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
