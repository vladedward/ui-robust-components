---
component: Combobox / autocomplete
id-prefix: CMB
status: draft
---

# Combobox / autocomplete

> Builds on `dropdown.md`. Also verify the dropdown capabilities that apply (positioning, long text, special characters, form integration, empty state), then the ones below.

## 1. When to use it vs alternatives

- **Combobox**: the user types to find a value, the list is large or remote, or free text is allowed alongside suggestions.
- **Dropdown** (`DD`): a short or medium list the user picks from without typing.
- **Search input** (`SRC`): the result is a results page, not a value for a field.
- **Native input with a suggestion list**: simple suggestions for free text.

## 2. Anatomy and variants

Parts: label, text field, suggestion list, options, optional clear action, optional loading and empty indicators, helper and error text.

Variants that change which capabilities apply:

- List only (value must come from the list) vs free text allowed
- Static options vs options loaded as the user types
- Single vs multiple selection (selected values shown as removable items)
- Minimum characters before suggestions appear vs suggestions on focus

Also covers these variants through the **Applies when** column: **chips and tags** (`CMB-17`, `CMB-18`; selected value display and removal are `CMB-15`) and a **command palette** (`CMB-19`, `CMB-20`). The palette also follows `dialog.md` for the modal surface.

## 3. States

Empty, typing, suggestions open, option highlighted, option selected, loading, no results, loading failed, disabled, read-only, error.

## 4. Behavior and keyboard interaction

Focus stays in the text field while the highlight moves through the list.

| Key | Result |
|---|---|
| Printable characters | Update the text and the suggestions |
| ArrowDown / ArrowUp | Opens the list if closed, moves the highlight |
| Enter | Selects the highlighted option, or commits the text when free text is allowed |
| Escape | Closes the list; pressed again, clears the text where the pattern defines it |
| Tab | Leaves the field; the list closes and the pending text is committed or reverted per the list only or free text rule |
| Home / End | Move the caret in the text field |

## 5. Component-specific accessibility

- The field exposes that it has a popup list and whether it is open.
- The highlighted option is exposed without moving focus out of the field.
- The number of suggestions or the absence of results is announced.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| CMB-01 | Typing shows matching suggestions; the list opens and closes predictably | Always | Required | Usually provided by primitives |
| CMB-02 | Keyboard: highlight moves with arrows while focus stays in the field; Enter selects; Escape closes | Always | Required | Usually provided by primitives |
| CMB-03 | Matching rule is defined and consistent: case, diacritics and word position | Always | Required | Application's job |
| CMB-04 | Asynchronous results are debounced, show loading, ignore outdated responses, and show an error with retry on failure | Async options | If applicable | Application's job |
| CMB-05 | A message is shown when nothing matches | Always | Required | Application's job |
| CMB-06 | List only: text that is not an option is reverted or flagged on leaving the field. Free text: the typed text is kept as the value | Always | Required | Application's job |
| CMB-07 | Selecting an option sets both the text and the value; the value is identified by a stable id, not the label | Always | Required | Application's job |
| CMB-08 | The text and the value can be cleared in one step | Clearable | If applicable | Application's job |
| CMB-09 | The highlighted option and the result count are exposed to assistive technology | Always | Required | Usually provided by primitives |
| CMB-10 | A minimum number of characters is respected, with a hint, and initial suggestions are defined | Minimum characters or suggestions on focus | If applicable | Application's job |
| CMB-11 | An initial value that is not in the loaded results still shows its label | Initial value | Required | Application's job |
| CMB-12 | Composition input (IME), diacritics, emoji and special characters do not trigger searches mid-composition or corrupt the text | Always | Required | Application's job |
| CMB-13 | The list is fully visible: flips, is not clipped, is stacked above content | Always | Required | Application's job |
| CMB-14 | Form value is submitted, reset and retained after a failed submit | Inside a form | Required | Application's job |
| CMB-15 | Selected values appear as removable items that are operable by keyboard, and Backspace behavior is defined | Multiple selection | If applicable | Application's job |
| CMB-16 | Usable on touch devices and small viewports, list not hidden by the on-screen keyboard | Always | Required | Application's job |
| CMB-17 | Tags can be created from typed text with defined separators (Enter, comma, paste split into several), whitespace is trimmed, duplicates and the maximum count are handled, and each is validated | Chips or tags | If applicable | Application's job |
| CMB-18 | Many tags stay manageable: the layout wraps or collapses with a count, and each remove control is named with its tag | Chips or tags | If applicable | Application's job |
| CMB-19 | A command palette opens with a shortcut that does not clash, behaves as a modal surface, groups results, runs the chosen action then closes, and returns focus | Command palette | If applicable | Application's job |
| CMB-20 | Command palette results show recent items and shortcuts, handle no results, and only offer actions the user may run | Command palette | If applicable | Application's job |

## 7. Anti-patterns

- Firing a request on every keystroke and showing the answer to an older query.
- Treating typed text as a valid value in a list-only field.
- Moving focus into the list, so typing stops working.
- Saving the label as the value.
- Starting a search during IME composition.
- An empty list with no message.
- Showing a raw id when the initial value was loaded before its option.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| CMB-01 | Functional | Always | Suggestions | Type a few characters, then delete them | List opens with matches, closes or resets when appropriate | Required | Automatable | Critical |
| CMB-02 | Keyboard | Always | Keyboard model | Use arrows, Enter and Escape while typing | Highlight moves, focus stays in the field, Enter selects, Escape closes | Required | Automatable | Critical |
| CMB-03 | Functional | Always | Matching rule | Type in a different case, without diacritics, with a word from the middle | Matches follow the defined rule | Required | Automatable | Important |
| CMB-04 | Data | Async options | Async results | Type quickly, make an early response arrive late, then fail | Only the latest query shown, loading shown, error with retry | If applicable | Automatable | Critical |
| CMB-05 | Functional | Always | No results | Type text that matches nothing | A "no results" message is shown | Required | Automatable | Critical |
| CMB-06 | Validation | Always | List only vs free text | Type text that is not an option and leave the field | List only: reverted or flagged. Free text: kept | Required | Automatable | Critical |
| CMB-07 | Data | Always | Value identity | Select an option, read the form value, use two options with the same label | The id is submitted, both options are distinct | Required | Automatable | Critical |
| CMB-08 | Functional | Clearable | Clear | Trigger the clear action | Text and value empty, focus in the field | If applicable | Automatable | Important |
| CMB-09 | Accessibility | Always | Exposed state | Use a screen reader while typing and moving the highlight | Highlighted option and result count announced | Required | Manual | Critical |
| CMB-10 | Functional | Minimum characters or suggestions on focus | Minimum characters | Type fewer than the minimum, then enough | Hint shown, no request until enough characters | If applicable | Automatable | Important |
| CMB-11 | Data | Initial value | Initial value | Render with a value whose option is not loaded | Label shown, not the id and not empty | Required | Automatable | Critical |
| CMB-12 | Data | Always | Composition and special characters | Compose text with an IME, type diacritics, emoji and quotes | No search mid-composition, text preserved | Required | Manual | Important |
| CMB-13 | Layout | Always | Positioning | Open near the viewport bottom and inside a clipping container | Fully visible | Required | Automatable | Important |
| CMB-14 | Data | Inside a form | Form integration | Submit, reset, fail validation | Value correct, reset restores, value retained | Required | Automatable | Critical |
| CMB-15 | Keyboard | Multiple selection | Selected items | Select several, remove items by keyboard and with Backspace | Items operable and removable, value updated | If applicable | Automatable | Important |
| CMB-16 | Layout | Always | Touch and small viewports | Use a narrow viewport and a real device with the keyboard shown | List reachable and not covered | Required | Manual | Important |
| CMB-17 | Functional | Chips or tags | Tags can be created from typed text with defined separators (Enter, comma, paste split into several), whitespace is trimmed, duplicates and the maximum count are handled, and each is validated | Type with separators, paste 'a, b, c', add a duplicate, exceed the limit | Tags created as defined, duplicates and limits reported | If applicable | Automatable | Critical |
| CMB-18 | Layout | Chips or tags | Many tags stay manageable: the layout wraps or collapses with a count, and each remove control is named with its tag | Add many long tags and inspect the remove controls | Layout intact, remove controls named per tag | If applicable | Automatable | Important |
| CMB-19 | Keyboard | Command palette | A command palette opens with a shortcut that does not clash, behaves as a modal surface, groups results, runs the chosen action then closes, and returns focus | Open with the shortcut, search, run an action, press Escape | Opens and closes cleanly, action runs once, focus returned | If applicable | Automatable | Critical |
| CMB-20 | Data | Command palette | Command palette results show recent items and shortcuts, handle no results, and only offer actions the user may run | Search with no match, with a restricted action, and reopen | No results shown, restricted actions absent or explained, recents correct | If applicable | Automatable | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
