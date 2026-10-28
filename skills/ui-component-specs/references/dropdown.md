---
component: Dropdown / select (single and multiple)
id-prefix: DD
status: draft
---

# Dropdown / select

## 1. When to use it vs alternatives

- **Native select**: default choice for a single value from a short or medium list with plain text options. Best mobile behavior, free keyboard and accessibility.
- **Radio group**: 2 to 5 options where seeing all choices at once helps the decision.
- **Checkbox group**: multiple selection with few options.
- **Custom dropdown**: needed for rich option content, multiple selection with summary, option groups with custom styling, or search inside the list.
- **Combobox / autocomplete** (`CMB`): free text, very large or remote datasets, or results that depend on what the user types. A dropdown with a filter field over a fully loaded list stays a dropdown.

## 2. Anatomy and variants

Parts: trigger (shows the selected value or placeholder), label, option panel, options, optional option groups, optional search field, optional reset action, helper and error text.

Variants that change which capabilities apply:

- Single vs multiple selection
- Short list vs long list (more than about 15 options, or a panel that scrolls)
- Static options vs options loaded asynchronously
- Plain text options vs rich options
- With vs without search or filter
- With vs without option groups

Also covers these variants through the **Applies when** column: an always visible **listbox** (`DD-27`, `DD-28`), **tree select** (`DD-29`, `DD-30`) and **transfer list** (`DD-31`). A tree shown on its own is in `tree-view.md`.

## 3. States

Default (placeholder or selected value), hover, focus, open, option highlighted, option selected, option disabled, disabled, read-only, required, error, loading, empty, loading failed.

## 4. Behavior and keyboard interaction

Open the panel, move through options, select, close. The value shown on the trigger always matches the form value.

| Key | Result |
|---|---|
| Enter, Space, ArrowDown on the trigger | Opens the panel and highlights the selected option, or the first option when none is selected |
| ArrowDown / ArrowUp | Moves the highlight, skipping disabled options |
| Home / End | Highlights the first / last option |
| PageDown / PageUp | Moves the highlight by a page of options |
| Printable character | Highlights the next option starting with those characters (typeahead) |
| Enter (Space when there is no search field) | Selects the highlighted option |
| Escape | Closes the panel, focus returns to the trigger, value unchanged |
| Tab / Shift+Tab | Moves focus out of the control and closes the panel, no selection is made implicitly unless the pattern defines it |

Single selection closes the panel after selecting. Multiple selection keeps it open so several options can be chosen.

## 5. Component-specific accessibility

- Trigger has an accessible name from the visible label and exposes the current value.
- The trigger exposes expanded or collapsed state and what it controls.
- The highlighted option is exposed to assistive technology while focus stays on the trigger (or on the search field).
- Selected options expose selected state. In multiple selection the number of selected values is perceivable.
- Option groups have names.
- General rules (focus visibility, contrast, target size, error association) are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| DD-01 | Open and close with pointer and keyboard | Always | Required | Usually provided by primitives |
| DD-02 | Escape closes the panel and returns focus to the trigger | Always | Required | Usually provided by primitives |
| DD-03 | Interacting outside the panel closes it without changing the value | Always | Required | Usually provided by primitives |
| DD-04 | Selecting an option updates the value; single selection closes the panel, multiple keeps it open | Always | Required | Usually provided by primitives |
| DD-05 | Placeholder or default shown when no value is selected | Always | Required | Application's job |
| DD-06 | Disabled options cannot be selected, are skipped by keyboard navigation and stay perceivable | Options can be disabled | If applicable | Usually provided by primitives |
| DD-07 | Empty state: a message is shown when there are no options | Always | Required | Application's job |
| DD-08 | Very long option text and very long selected value stay usable: no overflow of the panel or layout, full text still available | Always | Required | Application's job |
| DD-09 | Long lists: panel scrolls, the highlighted option stays in view, Home, End, PageUp, PageDown work | Long list | If applicable | Usually provided by primitives |
| DD-10 | Loading state while options load, and an error state with a retry action when loading fails | Async options | If applicable | Application's job |
| DD-11 | A preselected value that is not in the options list is handled explicitly (kept visible and flagged, or cleared with feedback), never silently shown as empty or as another option | Always | Required | Application's job |
| DD-12 | Search or filter narrows the list, shows an empty state for no match, and resets when the panel closes | Search or filter present | If applicable | Application's job |
| DD-13 | Typeahead highlights the matching option | No search field | If applicable | Usually provided by primitives |
| DD-14 | Reset action clears all selections in one step | Multiple selection | If applicable | Application's job |
| DD-15 | Option groups are labeled and navigable as part of one list | Option groups | If applicable | Usually provided by primitives |
| DD-16 | The panel stays fully visible: opens upward when there is no room below, is not clipped by scrolling or overflow containers, is stacked above surrounding content | Always | Required | Application's job |
| DD-17 | Form integration: the value is submitted, restored on reset, and retained after a failed submit | Inside a form | Required | Application's job |
| DD-18 | Required, error, disabled and read-only states; the error message is associated with the control | Always | Required | Application's job |
| DD-19 | Label, role, expanded state, highlighted option and selection changes are exposed to assistive technology | Always | Required | Usually provided by primitives |
| DD-20 | Special characters, diacritics and emoji display correctly in options, selected value and search | Always | Required | Application's job |
| DD-21 | Rapid repeated interaction (double activation, successive selections, quick open and close) leaves a consistent state | Always | Required | Application's job |
| DD-22 | Usable on touch devices and small viewports, panel not hidden behind the on-screen keyboard | Always | Required | Application's job |
| DD-23 | Usable at 200% zoom, in right-to-left layout and in dark mode, with sufficient contrast | Always | Required | Application's job |
| DD-24 | Select all action | Multiple selection | Optional | Application's job |
| DD-25 | The selected values stay readable when many are selected (summary, count or wrapping) | Multiple selection | If applicable | Application's job |
| DD-26 | Options are identified by a stable value, not by label; options with identical labels stay distinguishable | Always | Required | Application's job |
| DD-27 | An always visible list is one tab stop, selection either follows focus or needs an explicit action as defined, and the list scrolls to keep the focused option in view | Listbox | If applicable | Usually provided by primitives |
| DD-28 | Multiple selection by keyboard supports toggling and ranges, and selecting all | Listbox with multiple selection | If applicable | Usually provided by primitives |
| DD-29 | Hierarchy: branches expand and collapse by keyboard, selecting a parent has a defined effect on its children with a mixed state, and the selected value shows its path | Tree select | If applicable | Application's job |
| DD-30 | Search shows matches together with their ancestors, children can load on demand, and deep nesting stays readable | Tree select | If applicable | Application's job |
| DD-31 | Items move between the two lists in both directions, singly and in bulk, with counts announced, both lists keyboard operable, and disabled items respected | Transfer list | If applicable | Application's job |

## 7. Anti-patterns

- Building a custom dropdown where a native select would do.
- Rendering an empty panel when there are no options.
- Silently showing the placeholder (or the first option) when the stored value is not in the list.
- Panel inside an overflow-hidden container, so it is cut off.
- Closing on Escape without returning focus to the trigger.
- Using the label text as the stored value.
- Trusting a library component and skipping the empty, long text, async and form cases.
- Selecting an option just because the highlight passed over it with Tab.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| DD-01 | Functional | Always | Open and close | Open the control with the pointer, close it, repeat with the keyboard | Panel opens and closes both ways, expanded state follows | Required | Automatable | Critical |
| DD-02 | Keyboard | Always | Escape closes and returns focus | Open the panel, move the highlight, close with Escape | Panel closed, value unchanged, focus on the trigger | Required | Automatable | Critical |
| DD-03 | Functional | Always | Outside interaction | Open the panel, interact outside it | Panel closed, value unchanged | Required | Automatable | Important |
| DD-04 | Functional | Always | Selection | Select an option (single), then repeat with several options (multiple) | Value updated and shown on the trigger; single closes, multiple stays open | Required | Automatable | Critical |
| DD-05 | States | Always | Placeholder | Render with no value | Placeholder shown, form value empty | Required | Automatable | Important |
| DD-06 | Keyboard | Options can be disabled | Disabled options | Move through options past a disabled one, try to select it | It is skipped, cannot be selected, remains visible as disabled | If applicable | Automatable | Important |
| DD-07 | Functional | Always | Empty state | Open the control with no options | A "no options" message is shown, not an empty panel | Required | Automatable | Critical |
| DD-08 | Layout | Always | Very long text | Use an option and a selected value with a very long text, including one unbroken string | No horizontal overflow of the page, panel stays within the viewport, full text still available | Required | Automatable | Important |
| DD-09 | Keyboard | Long list | Long lists | Move to the last option with End and with repeated arrows, then PageUp | Highlighted option always visible, navigation reaches both ends | If applicable | Automatable | Important |
| DD-10 | Data | Async options | Loading and error | Open while options are loading, then make loading fail, then trigger the retry action | Loading indicator, then an error message with retry, then options after a successful retry | If applicable | Automatable | Critical |
| DD-11 | Data | Always | Preselected value missing | Provide a stored value that is not among the options | Behavior is explicit and visible, form value is not silently changed to another option | Required | Automatable | Critical |
| DD-12 | Functional | Search or filter present | Search | Type a query that matches some options, then one that matches none, then close and reopen | List narrows, "no match" message shown, query reset on reopen | If applicable | Automatable | Important |
| DD-13 | Keyboard | No search field | Typeahead | Type the first characters of an option, type quickly several characters | The matching option is highlighted, repeated characters cycle matches | If applicable | Automatable | Nice-to-have | 
| DD-14 | Functional | Multiple selection | Clear all selections | With several values selected, trigger the reset action | No value selected, placeholder shown, form value empty, focus stays somewhere logical | If applicable | Automatable | Important |
| DD-15 | Accessibility | Option groups | Option groups | Navigate across groups with the keyboard | Groups have names, navigation passes through all options in order | If applicable | Manual | Nice-to-have |
| DD-16 | Layout | Always | Positioning and clipping | Open near the bottom of the viewport, and inside a container that scrolls or hides overflow | Panel opens upward when needed, fully visible, above surrounding content | Required | Automatable | Critical |
| DD-17 | Data | Inside a form | Form integration | Submit with a value, reset the form, submit a form that fails validation | Submitted value correct, reset restores the initial value, value retained after failed submit | Required | Automatable | Critical |
| DD-18 | Validation | Always | Required, error, disabled, read-only | Submit empty when required, then set each state | Error message shown and associated with the control, disabled cannot be opened, read-only shows the value but cannot be changed | Required | Automatable | Critical |
| DD-19 | Accessibility | Always | Exposed semantics | Inspect the accessibility tree while navigating and selecting; use a screen reader | Name, role, expanded state, highlighted option and selection are exposed and announced | Required | Manual | Critical |
| DD-20 | Data | Always | Special characters | Use options and queries with diacritics, quotes, markup characters and emoji | Text shown literally and correctly, search matches as expected | Required | Automatable | Important |
| DD-21 | Functional | Always | Rapid interaction | Activate the trigger twice quickly, select several options in quick succession, open and close repeatedly | Consistent state, one value, panel open or closed as the last action implies | Required | Automatable | Important |
| DD-22 | Layout | Always | Touch and small viewports | Use a narrow viewport and a real touch device | Panel reachable and not hidden by the on-screen keyboard, targets large enough | Required | Manual | Important |
| DD-23 | Layout | Always | Zoom, RTL, dark mode | Check at 200% zoom, in right-to-left layout, in dark mode | Nothing clipped or overlapping, arrows and alignment mirrored, contrast sufficient | Required | Manual | Important |
| DD-24 | Functional | Multiple selection | Select all | Trigger select all, then trigger it again | All options selected, then none (or defined behavior with disabled options) | Optional | Automatable | Nice-to-have |
| DD-25 | Layout | Multiple selection | Many selected values | Select most options | Trigger stays readable and within its container, count or summary correct | If applicable | Automatable | Important |
| DD-26 | Data | Always | Stable value identity | Provide two options with the same label but different values | Both can be selected independently and the right value is submitted | Required | Automatable | Important |
| DD-27 | Keyboard | Listbox | An always visible list is one tab stop, selection either follows focus or needs an explicit action as defined, and the list scrolls to keep the focused option in view | Tab into the list and move through the options | One tab stop, selection model as defined, focused option visible | If applicable | Automatable | Critical |
| DD-28 | Keyboard | Listbox with multiple selection | Multiple selection by keyboard supports toggling and ranges, and selecting all | Select with Space, extend with Shift and arrows, select all | Selection correct and exposed | If applicable | Automatable | Important |
| DD-29 | Functional | Tree select | Hierarchy: branches expand and collapse by keyboard, selecting a parent has a defined effect on its children with a mixed state, and the selected value shows its path | Expand by keyboard, select a parent, select a child | Parent and child states consistent, path shown | If applicable | Automatable | Critical |
| DD-30 | Data | Tree select | Search shows matches together with their ancestors, children can load on demand, and deep nesting stays readable | Search for a deep node, expand an unloaded branch, use ten levels | Matches in context, loading handled, no overflow | If applicable | Automatable | Important |
| DD-31 | Functional | Transfer list | Items move between the two lists in both directions, singly and in bulk, with counts announced, both lists keyboard operable, and disabled items respected | Move items both ways by keyboard, move all, move a disabled item | Lists and counts correct, announced, disabled stay put | If applicable | Automatable | Critical |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
