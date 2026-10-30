---
component: Text input
id-prefix: TXT
status: draft
---

# Text input

## 1. When to use it vs alternatives

- **Text input**: short single-line free text (name, email, search term).
- **Textarea** (`TXA`): multi-line or long text.
- **Dropdown, radio group**: when the answers come from a known list.
- **Specialized inputs** (number, date, password, masked, OTP): when the format is constrained. Prefer them over a plain input with custom validation.

## 2. Anatomy and variants

Parts: label, input, optional helper text, optional error text, optional prefix and suffix, optional clear action, optional character counter.

Variants that change which capabilities apply:

- Required vs optional
- With vs without maximum length
- Free text vs constrained format (email, phone, URL)
- Validated on the client only vs also validated asynchronously
- Editable, read-only, disabled

Also covers these variants through the **Applies when** column: **password** (reveal, strength, paste), **email, phone and URL**, **masked input** (card, IBAN, phone) and **one-time code (OTP)**. Their rows are `TXT-20` to `TXT-26`.

## 3. States

Default, hover, focus, filled, disabled, read-only, error, loading (async validation), success (only when useful).

## 4. Behavior and keyboard interaction

Typing, pasting and autofill all update the value the same way. Validation runs at a predictable moment. Enter inside a form follows the form's submit behavior.

| Key | Result |
|---|---|
| Tab / Shift+Tab | Moves focus in and out |
| Enter | Submits the form when inside one |
| Escape | Clears or reverts only if the component defines it, never silently |

## 5. Component-specific accessibility

- A visible, persistent label is programmatically associated with the input.
- Helper and error text are associated with the input and available when it receives focus.
- Required state is exposed, not only shown with a symbol.
- Error appears as text, not only as color or icon, and is announced when it appears.
- The input purpose is identified so browsers and assistive tools can autofill.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| TXT-01 | Visible persistent label associated with the input | Always | Required | Application's job |
| TXT-02 | Helper text associated with the input | Helper text present | If applicable | Application's job |
| TXT-03 | Required state shown and exposed | Required field | If applicable | Application's job |
| TXT-04 | Validation timing: not on first focus, after leaving the field or on submit, then re-validated while correcting | Always | Required | Application's job |
| TXT-05 | Error message is specific, adjacent, associated, announced and not color-only | Always | Required | Application's job |
| TXT-06 | Input type, input mode and autofill purpose match the data | Always | Required | Application's job |
| TXT-07 | Browser autofill and password managers work and the field validates the filled value | Always | Required | Application's job |
| TXT-08 | Paste works for short, long and formatted text, with defined handling of surrounding whitespace | Always | Required | Application's job |
| TXT-09 | Maximum length is enforced or counted, with feedback, including on paste | Maximum length | If applicable | Application's job |
| TXT-10 | Empty vs whitespace-only values are treated consistently | Always | Required | Application's job |
| TXT-11 | Composition input (IME), diacritics, emoji, right-to-left text and special characters work | Always | Required | Application's job |
| TXT-12 | Read-only stays focusable and submitted; disabled is neither | Can be read-only or disabled | Required | Usually provided by primitives |
| TXT-13 | Placeholder is a hint only, never the label, and has sufficient contrast | Placeholder present | If applicable | Application's job |
| TXT-14 | A value longer than the field stays usable and inspectable | Always | Required | Application's job |
| TXT-15 | Value is retained after a failed submit and after navigating back | Inside a form | Required | Application's job |
| TXT-16 | Prefix, suffix and clear action do not break labeling, focus or the value | Adornments present | If applicable | Application's job |
| TXT-17 | Asynchronous validation shows progress, handles failure and outdated responses | Async validation | If applicable | Application's job |
| TXT-18 | Usable at 200% zoom, in right-to-left layout and on touch devices | Always | Required | Application's job |
| TXT-19 | Sensitive values are not exposed by autofill suggestions, logs or visible echo unless intended | Sensitive data | If applicable | Application's job |
| TXT-20 | A password reveal control is named, exposes its state, keeps the value and caret, and hides the value again when appropriate | Password | If applicable | Application's job |
| TXT-21 | Pasting and password managers are allowed, long passwords are not truncated, and rules and strength feedback are shown before and while typing and are not color-only | Password | If applicable | Application's job |
| TXT-22 | Email, phone and URL checks are lenient and correct: surrounding spaces, plus signs, international formats and internationalized domains are accepted, and the right keyboard is offered | Email, phone or URL | If applicable | Application's job |
| TXT-23 | The mask is applied while typing and on paste, the caret stays correct when editing in the middle or deleting across separators, and the displayed and the submitted values are defined | Masked input | If applicable | Application's job |
| TXT-24 | Masked values are checked for completeness and for check digits where they exist, with a distinct incomplete state | Masked input | If applicable | Application's job |
| TXT-25 | A one-time code works as one logical field: typing advances, deleting moves back, pasting a full code fills every position, the code can come from automatic fill, and only allowed characters are accepted | One-time code | If applicable | Application's job |
| TXT-26 | Code errors are handled: wrong code, expired code, resend with a cooldown that is announced, attempt limits, and a single accessible name that states the position | One-time code | If applicable | Application's job |

## 7. Anti-patterns

- Placeholder used instead of a label.
- Validating on the first keystroke or on first focus.
- Error shown only as a red border.
- Blocking paste.
- Trimming or changing what the user typed without telling them.
- Blocking characters with key handlers (breaks IME and paste).
- Clearing the field after a failed submit.
- Disabling a field that the user needs to read or copy (use read-only).

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| TXT-01 | Accessibility | Always | Label | Inspect the name of the input, activate the label | Name equals the visible label, focus moves to the input | Required | Automatable | Critical |
| TXT-02 | Accessibility | Helper text present | Helper text | Focus the input with a screen reader | Helper text is read with the label | If applicable | Manual | Important |
| TXT-03 | Validation | Required field | Required | Submit empty | Required state exposed, error shown and associated | If applicable | Automatable | Critical |
| TXT-04 | Validation | Always | Timing | Focus and leave empty, type an invalid value then leave, then correct it | No error on first focus, error after leaving, error clears as soon as the value is valid | Required | Automatable | Critical |
| TXT-05 | Validation | Always | Error message | Trigger an error | Specific text next to the field, associated with it, announced, visible without color | Required | Automatable | Critical |
| TXT-06 | Functional | Always | Type and autofill purpose | Inspect the input type and mode on a mobile device | Appropriate keyboard and autofill suggestions | Required | Manual | Important |
| TXT-07 | Functional | Always | Autofill | Fill with browser autofill | Value is accepted and validated like typed input | Required | Manual | Important |
| TXT-08 | Functional | Always | Paste | Paste short text, very long text and text with leading and trailing spaces | Value updated, handling of whitespace as defined, validation runs | Required | Automatable | Important |
| TXT-09 | Validation | Maximum length | Maximum length | Type and paste beyond the limit | Limit enforced or counted, user told, nothing lost silently | If applicable | Automatable | Important |
| TXT-10 | Validation | Always | Whitespace-only | Enter only spaces | Treated as empty where the field is required | Required | Automatable | Important |
| TXT-11 | Data | Always | Special characters | Enter diacritics, emoji, quotes, markup characters, right-to-left text, use IME composition | Value preserved exactly, no corruption, composition not interrupted | Required | Automatable | Important |
| TXT-12 | States | Can be read-only or disabled | Read-only vs disabled | Tab through and submit with each state | Read-only receives focus and is submitted, disabled is skipped and not submitted | Required | Automatable | Important |
| TXT-13 | Accessibility | Placeholder present | Placeholder | Remove the placeholder and check contrast | Field still fully labeled, hint readable | If applicable | Manual | Nice-to-have |
| TXT-14 | Layout | Always | Long value | Enter a value much longer than the field | Layout intact, content reachable | Required | Automatable | Important |
| TXT-15 | Data | Inside a form | Persistence | Fail a submit, then navigate back and forward | Entered value still there | Required | Automatable | Critical |
| TXT-16 | Functional | Adornments present | Adornments | Use the clear action and type next to the prefix and suffix | Value correct, focus stays in the field, label unchanged | If applicable | Automatable | Nice-to-have |
| TXT-17 | Data | Async validation | Async validation | Type quickly, make the response slow, then fail | Progress shown, only the latest response applies, failure handled | If applicable | Automatable | Important |
| TXT-18 | Layout | Always | Zoom, RTL, touch | Check at 200% zoom, in right-to-left layout and on a touch device | Nothing clipped, target usable | Required | Manual | Important |
| TXT-19 | Data | Sensitive data | Sensitive values | Review autofill, history and echo | No unintended exposure | If applicable | Manual | Important |
| TXT-20 | Functional | Password | A password reveal control is named, exposes its state, keeps the value and caret, and hides the value again when appropriate | Reveal and hide the value repeatedly while typing | Value and caret preserved, control named with state, value hidden by default | If applicable | Automatable | Critical |
| TXT-21 | Functional | Password | Pasting and password managers are allowed, long passwords are not truncated, and rules and strength feedback are shown before and while typing and are not color-only | Paste a long password, use a password manager, type a weak then a strong one | Accepted in full, rules visible up front, strength given in text without a flood of announcements | If applicable | Automatable | Critical |
| TXT-22 | Validation | Email, phone or URL | Email, phone and URL checks are lenient and correct: surrounding spaces, plus signs, international formats and internationalized domains are accepted, and the right keyboard is offered | Enter 'a+b@example.com', ' a@b.co ', an international phone number, a URL without a scheme | Valid forms accepted, obvious mistakes reported specifically | If applicable | Automatable | Important |
| TXT-23 | Functional | Masked input | The mask is applied while typing and on paste, the caret stays correct when editing in the middle or deleting across separators, and the displayed and the submitted values are defined | Type, paste, edit in the middle, delete across a separator, select all and replace | Formatting correct, caret not jumping, submitted value as defined | If applicable | Automatable | Critical |
| TXT-24 | Validation | Masked input | Masked values are checked for completeness and for check digits where they exist, with a distinct incomplete state | Enter incomplete, wrong check digit and valid values | Incomplete and invalid reported differently | If applicable | Automatable | Important |
| TXT-25 | Functional | One-time code | A one-time code works as one logical field: typing advances, deleting moves back, pasting a full code fills every position, the code can come from automatic fill, and only allowed characters are accepted | Type, delete, paste a full code, paste with spaces, use automatic fill from a message | Positions filled correctly, no stuck focus, code complete | If applicable | Automatable | Critical |
| TXT-26 | Validation | One-time code | Code errors are handled: wrong code, expired code, resend with a cooldown that is announced, attempt limits, and a single accessible name that states the position | Enter a wrong code, wait for expiry, request a new code repeatedly | Specific messages, cooldown shown and announced, limit explained | If applicable | Automatable | Critical |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
