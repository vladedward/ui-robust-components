---
component: Inline validation and error messages
id-prefix: VAL
status: draft
---

# Inline validation and error messages

> Cross-cutting behavior used by every form field. Field references link here for timing and message rules. The form-level flow is in `form.md`.

## 1. When to use it vs alternatives

- **Inline validation**: telling the user next to a field what is wrong and how to fix it.
- **Error summary**: a list of all errors at the top of a form after a failed submit, in addition to inline messages.
- **Alert** (`ALR`) or **toast** (`TST`): problems that are not tied to a field.
- **Constraints in the control itself** (input type, limits): preferred over reporting an error where the control can prevent the mistake.

## 2. Anatomy and variants

Parts: field, error message (with an icon), optional helper text, optional error summary with links, optional success indication.

Variants that change which capabilities apply:

- Single field rules vs rules across several fields
- Client-only vs also asynchronous or server checks
- Forms with one field vs many fields
- Required vs optional fields

## 3. States

Untouched, valid, invalid, validating (pending), error shown, error summary shown.

## 4. Behavior and keyboard interaction

- Validation does not run before the user has had a chance to enter a value.
- After leaving a field or on submit, its error appears. While the user corrects it, the error updates as they type.
- On a failed submit, focus moves to the error summary or the first invalid field.

## 5. Component-specific accessibility

- The error text is associated with its field and exposed as invalid.
- Error appearance is announced once, not repeatedly.
- Errors are text, not only color or an icon.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| VAL-01 | Timing: no error before interaction, error after leaving the field or on submit, updated while correcting | Always | Required | Application's job |
| VAL-02 | The message is specific and tells the user how to fix it | Always | Required | Application's job |
| VAL-03 | The message is associated with the field, the field is exposed as invalid, and the message is announced | Always | Required | Application's job |
| VAL-04 | An error summary lists every error with links to the fields, and receives focus on a failed submit | Several fields | If applicable | Application's job |
| VAL-05 | Errors are not conveyed by color alone | Always | Required | Application's job |
| VAL-06 | An error clears as soon as the value becomes valid, and the summary updates | Always | Required | Application's job |
| VAL-07 | Server errors map to the right field, with a general message as a fallback, and the entered data is kept | Server validation | Required | Application's job |
| VAL-08 | Rules across fields are reported on the right field (end before start, confirmation does not match) | Cross-field rules | If applicable | Application's job |
| VAL-09 | Asynchronous checks show a pending state, ignore outdated responses, and treat a failed check as unknown, not invalid | Async checks | If applicable | Application's job |
| VAL-10 | Required and optional fields are marked consistently | Always | Required | Application's job |
| VAL-11 | Messages are translated and a longer message does not break the layout | Always | Required | Application's job |
| VAL-12 | Success is shown only when it helps, and never before the value is fully checked | Success indication | Optional | Application's job |
| VAL-13 | One error is announced once, not by several live regions | Always | Required | Application's job |
| VAL-14 | The submit action is not disabled as a way of reporting invalid input | Always | Required | Application's job |
| VAL-15 | The entered value is kept after an error | Always | Required | Application's job |

## 7. Anti-patterns

- Validating on the first keystroke or on focus.
- "Invalid input" with no explanation.
- A disabled submit button with no explanation of why.
- Red border only.
- Clearing the field when it is invalid.
- Error text far from the field, or not linked to it.
- Treating a network failure of an availability check as "name taken".

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| VAL-01 | Validation | Always | Timing | Focus and leave an empty field, enter invalid then correct it | No early error, error after leaving, updates while correcting | Required | Automatable | Critical |
| VAL-02 | Validation | Always | Message quality | Trigger each rule | Each message says what to change | Required | Manual | Important |
| VAL-03 | Accessibility | Always | Association | Trigger an error with a screen reader | Message read with the field, invalid state exposed | Required | Automatable | Critical |
| VAL-04 | Keyboard | Several fields | Error summary | Submit with several errors | Summary shown with working links, focus placed | If applicable | Automatable | Critical |
| VAL-05 | Accessibility | Always | Not color-only | View in grayscale | Error clear without color | Required | Manual | Important |
| VAL-06 | Functional | Always | Clearing | Correct the value | Error removed, summary updated | Required | Automatable | Important |
| VAL-07 | Data | Server validation | Server errors | Return field errors, an unknown error and a network failure | Mapped, generic fallback, data kept | Required | Automatable | Critical |
| VAL-08 | Validation | Cross-field rules | Cross-field | Set conflicting values | Error on the right field, resolved when either is fixed | If applicable | Automatable | Important |
| VAL-09 | Data | Async checks | Async checks | Type quickly, delay responses, fail the check | Pending shown, latest result only, failure not reported as invalid | If applicable | Automatable | Important |
| VAL-10 | Accessibility | Always | Required marking | Review all fields | Consistent, exposed | Required | Automatable | Important |
| VAL-11 | Layout | Always | Translation and length | Use a language with longer text | Messages fit, layout intact | Required | Manual | Nice-to-have |
| VAL-12 | Functional | Success indication | Success | Complete a field correctly | Shown only after a full check | Optional | Automatable | Nice-to-have |
| VAL-13 | Accessibility | Always | Single announcement | Trigger an error with a screen reader | Announced once | Required | Manual | Important |
| VAL-14 | Functional | Always | Submit available | Submit an invalid form | Submit works and reports errors | Required | Automatable | Important |
| VAL-15 | Data | Always | Kept value | Fail validation | Entered value unchanged | Required | Automatable | Critical |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
