---
component: Date picker
id-prefix: DTP
status: draft
---

# Date picker

## 1. When to use it vs alternatives

- **Typed date fields**: dates the user knows by heart (birth date). Typing is faster than navigating a calendar.
- **Date picker (field with calendar)**: dates near today, or where weekday and surroundings matter (booking, scheduling).
- **Native date input**: simplest option with built-in mobile pickers, when its look and locale handling are acceptable.
- **Date range** (`DTR`), **time picker** (`TMP`), **calendar** (`CAL`): separate patterns.

## 2. Anatomy and variants

Parts: label, text field, format hint, calendar trigger, calendar panel with month and year navigation and a day grid, helper and error text, optional today and clear actions.

Variants that change which capabilities apply:

- Typed only, picked only, or both
- With minimum, maximum or disabled dates
- Availability data loaded asynchronously
- Date only vs date with time
- Native vs custom calendar

Also covers these variants through the **Applies when** column: **date range** (`DTP-21` to `DTP-23`), **time picker** (`DTP-24`, `DTP-25`) and an **always visible calendar** (`DTP-26`). The single date rows apply to each end of a range.

## 3. States

Empty, filled, focus, calendar open, day highlighted, day selected, day today, day disabled, disabled, read-only, error, loading availability.

## 4. Behavior and keyboard interaction

The text field and the calendar represent the same value. Typing updates the calendar, picking updates the text.

| Key | Result |
|---|---|
| Enter or Space on the calendar trigger | Opens the calendar, focus moves to the selected day, or today when none is selected |
| ArrowLeft / ArrowRight | Previous / next day |
| ArrowUp / ArrowDown | Same day in the previous / next week |
| Home / End | First / last day of the week |
| PageUp / PageDown | Previous / next month |
| Shift+PageUp / Shift+PageDown | Previous / next year |
| Enter / Space | Selects the focused day and closes the calendar |
| Escape | Closes the calendar without changing the value, focus returns to the trigger or field |

In right-to-left layout the horizontal arrows are mirrored.

## 5. Component-specific accessibility

- The day grid exposes its structure, the focused day and the selected day; the month and year are announced when they change.
- The expected format is stated in text, not only as a placeholder.
- The calendar trigger has an accessible name.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| DTP-01 | The date can be typed, and picked from the calendar, and both stay in sync | Typed and picked | Required | Application's job |
| DTP-02 | The expected format is shown in text and matches the locale and the displayed value | Always | Required | Application's job |
| DTP-03 | Invalid dates are rejected with a specific message: nonexistent dates, partial input, wrong separators, ambiguous two-digit years | Typed input | Required | Application's job |
| DTP-04 | Minimum and maximum are enforced in the calendar and in typed input | Limits | If applicable | Application's job |
| DTP-05 | Disabled dates cannot be selected, are perceivable as unavailable, and the reason is available where useful | Disabled dates | If applicable | Application's job |
| DTP-06 | The calendar grid is fully keyboard operable | Calendar present | Required | Usually provided by primitives |
| DTP-07 | Opening the calendar moves focus into it; closing returns focus to the trigger or field | Calendar present | Required | Usually provided by primitives |
| DTP-08 | Month and year navigation reaches distant dates quickly and respects the limits | Calendar present | Required | Application's job |
| DTP-09 | Today and the selected day are indicated, and the calendar opens on the selected date, or a sensible default month | Calendar present | Required | Application's job |
| DTP-10 | Locale is respected: first day of the week, month and day names, format, numerals, right-to-left layout | Always | Required | Application's job |
| DTP-11 | A date without a time never shifts across time zones and daylight saving changes; month ends and leap days are correct | Always | Required | Application's job |
| DTP-12 | The submitted value is in an unambiguous format, reset restores the initial value, and the value is retained after a failed submit | Inside a form | Required | Application's job |
| DTP-13 | Clearing the value is possible, and empty is distinct from invalid | Optional field | If applicable | Application's job |
| DTP-14 | Required, error, disabled and read-only states, with the error associated to the field | Always | Required | Application's job |
| DTP-15 | Name, grid semantics, focused and selected day, and month changes are exposed to assistive technology | Calendar present | Required | Usually provided by primitives |
| DTP-16 | Usable on touch devices and small viewports, with a native picker or a touch-friendly calendar | Always | Required | Application's job |
| DTP-17 | The calendar panel is fully visible: not clipped by containers, flips when needed, stacked above content | Calendar present | Required | Application's job |
| DTP-18 | Pasted dates in common formats are accepted or rejected with clear feedback | Typed input | Required | Application's job |
| DTP-19 | Availability loaded asynchronously shows a loading state and handles failure | Async availability | If applicable | Application's job |
| DTP-20 | Selected, disabled and today days are distinguishable without color alone, with sufficient contrast, at 200% zoom and in dark mode | Always | Required | Application's job |
| DTP-21 | Choosing a range: start then end, an end before the start is swapped or rejected as defined, the partial range is visible, and a range can be cleared or restarted | Date range | If applicable | Application's job |
| DTP-22 | Range rules: minimum and maximum length, disabled dates inside the range, and a preview of the range while choosing | Date range | If applicable | Application's job |
| DTP-23 | Each end can be typed, is labeled, stays in sync with the calendar, and both values are submitted | Date range | If applicable | Application's job |
| DTP-24 | Time entry follows the locale (12 or 24 hours, unambiguous AM and PM), supports the step, partial typing, midnight and noon, and times that do not exist at daylight saving changes | Time picker | If applicable | Application's job |
| DTP-25 | The time list or spinner is keyboard operable, invalid and out-of-range times are rejected, and minimum and maximum times are enforced | Time picker | If applicable | Application's job |
| DTP-26 | A calendar that is always visible is one tab stop for the grid, month changes do not move focus unexpectedly, and indicators on days are available in text | Always visible calendar | If applicable | Application's job |

## 7. Anti-patterns

- Calendar only, for a date that is far away (birth date by month-by-month navigation).
- Format shown only as a placeholder that disappears on typing.
- Accepting "31/02/2026" or silently correcting it.
- Converting a calendar date to a timestamp and reading it back a day earlier.
- Ambiguous order (day or month first) with no hint.
- Disabled dates that look the same as available ones.
- Calendar that cannot be operated with a keyboard, or traps focus.
- Calendar clipped by a dialog or table container.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| DTP-01 | Functional | Typed and picked | Sync | Type a date and open the calendar, pick a date and read the field | Both always show the same date | Required | Automatable | Critical |
| DTP-02 | Accessibility | Always | Format hint | Inspect the field with and without a value | Expected format stated in text | Required | Automatable | Important |
| DTP-03 | Validation | Typed input | Invalid dates | Enter a nonexistent date, a partial date, a wrong separator, a two-digit year | Specific error, value not silently changed | Required | Automatable | Critical |
| DTP-04 | Validation | Limits | Min and max | Type and pick dates before the minimum and after the maximum | Rejected in both ways, limits visible in the calendar | If applicable | Automatable | Critical |
| DTP-05 | Functional | Disabled dates | Disabled dates | Navigate to and try to select a disabled date | Not selectable, visibly unavailable | If applicable | Automatable | Important |
| DTP-06 | Keyboard | Calendar present | Grid keyboard | Use every key in the keyboard table | Focus moves as specified across week, month and year boundaries | Required | Automatable | Critical |
| DTP-07 | Keyboard | Calendar present | Focus on open and close | Open, then close by selecting and by Escape | Focus moves in on open and returns on close, value unchanged on Escape | Required | Automatable | Critical |
| DTP-08 | Functional | Calendar present | Month and year navigation | Jump far forward and back, navigate at the limits | Reaches distant dates quickly, stops at the limits | Required | Automatable | Important |
| DTP-09 | Functional | Calendar present | Today and selected | Open with and without a value | Today and selected day marked, correct month shown | Required | Automatable | Important |
| DTP-10 | Layout | Always | Locale | Switch to locales with a different first day of the week, format and direction | Layout, names and format follow the locale | Required | Automatable | Important |
| DTP-11 | Data | Always | Time zones | Select the last day of a month, February 29, and a date around a daylight saving change, in different time zones | Date never shifts, value identical | Required | Automatable | Critical |
| DTP-12 | Data | Inside a form | Form value | Submit, reset, fail validation | Unambiguous value submitted, reset restores the initial value, value retained after failed submit | Required | Automatable | Critical |
| DTP-13 | Functional | Optional field | Clearing | Clear a selected value, leave the field empty and invalid | Empty accepted, invalid distinct | If applicable | Automatable | Important |
| DTP-14 | Validation | Always | States | Submit empty when required, set disabled and read-only | Error associated to the field, disabled cannot be changed, read-only shows the value | Required | Automatable | Critical |
| DTP-15 | Accessibility | Calendar present | Exposed semantics | Navigate the calendar with a screen reader | Grid, focused and selected day, and month change announced | Required | Manual | Critical |
| DTP-16 | Layout | Always | Touch and small viewports | Use a narrow viewport and a real touch device | Picker usable, targets large enough | Required | Manual | Important |
| DTP-17 | Layout | Calendar present | Positioning | Open near the viewport edge and inside a clipping container | Fully visible, flips when needed | Required | Automatable | Important |
| DTP-18 | Data | Typed input | Paste | Paste dates in several formats | Accepted or rejected with clear feedback | Required | Automatable | Important |
| DTP-19 | Data | Async availability | Async availability | Load availability slowly, then fail | Loading shown, failure handled, no wrong dates selectable meanwhile | If applicable | Automatable | Important |
| DTP-20 | Accessibility | Always | Visual distinction | View in grayscale, at 200% zoom, in dark mode | Selected, disabled and today are distinct, contrast sufficient | Required | Manual | Important |
| DTP-21 | Functional | Date range | Choosing a range: start then end, an end before the start is swapped or rejected as defined, the partial range is visible, and a range can be cleared or restarted | Pick the start, then an earlier end, then the same day, then restart | Behavior as defined, partial state visible | If applicable | Automatable | Critical |
| DTP-22 | Validation | Date range | Range rules: minimum and maximum length, disabled dates inside the range, and a preview of the range while choosing | Select ranges that are too short, too long, or cross a disabled date | Rejected or adjusted as defined, preview matches the result | If applicable | Automatable | Critical |
| DTP-23 | Data | Date range | Each end can be typed, is labeled, stays in sync with the calendar, and both values are submitted | Type each end and pick in the calendar, submit | Always in sync, both values submitted | If applicable | Automatable | Important |
| DTP-24 | Data | Time picker | Time entry follows the locale (12 or 24 hours, unambiguous AM and PM), supports the step, partial typing, midnight and noon, and times that do not exist at daylight saving changes | Enter times in both clock styles, at midnight, and in a skipped hour | Unambiguous, correct, skipped times handled | If applicable | Automatable | Critical |
| DTP-25 | Keyboard | Time picker | The time list or spinner is keyboard operable, invalid and out-of-range times are rejected, and minimum and maximum times are enforced | Operate by keyboard, enter times beyond the limits | Operable, limits enforced with a message | If applicable | Automatable | Important |
| DTP-26 | Keyboard | Always visible calendar | A calendar that is always visible is one tab stop for the grid, month changes do not move focus unexpectedly, and indicators on days are available in text | Tab to the calendar, change month, inspect day indicators | One stop, focus stable, indicators in text | If applicable | Automatable | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
