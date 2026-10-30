---
component: Form (complete)
id-prefix: FRM
status: draft
---

# Form (complete)

> The form as a whole. Field behavior is in the field references (`text-input.md`, `dropdown.md`, `checkbox.md` and others). Message and timing rules are in `inline-validation.md`. Multi-step forms also follow `stepper.md`.

## 1. When to use it vs alternatives

- **Form with a submit action**: collecting data to send once.
- **Autosaved settings**: each change applies immediately (use switches, `SWT`).
- **Multi-step flow** (`STP`): long or branching tasks.
- **Filters** (`FLT`): inputs that narrow a view, with no submission.

## 2. Anatomy and variants

Parts: fields and their labels, groups with legends, helper text, error summary, actions (submit, secondary, cancel), progress and result feedback.

Variants that change which capabilities apply:

- Create vs edit (with existing data)
- Short vs long form
- Client-only vs server-submitted
- With conditional or dependent fields
- With draft saving or autosave
- Single vs multi-step

## 3. States

Pristine, edited, invalid, submitting, submitted successfully, failed (validation or server or network), disabled while submitting, session expired.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Tab / Shift+Tab | Moves through fields and actions in visual order |
| Enter | Submits from single-line fields, inserts a line break in a multi-line field |
| Escape | Cancels only where a cancel action is defined, never silently discards |

## 5. Component-specific accessibility

- Every control has a label, and related controls are grouped with a name.
- Errors are associated with fields and summarized, and focus is managed after a failed submit.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| FRM-01 | Every control is labeled and related controls are grouped with a name | Always | Required | Application's job |
| FRM-02 | Submission works by Enter and by the submit action, with one clear primary action | Always | Required | Application's job |
| FRM-03 | A submission already in progress is not repeated, and loading is shown | Always | Required | Application's job |
| FRM-04 | A failed client validation puts focus on the error summary or the first invalid field, and shows every error | Always | Required | Application's job |
| FRM-05 | Server errors are mapped to fields, with a general fallback, network failures are reported, and data is kept | Server submission | Required | Application's job |
| FRM-06 | Entered data is retained after a failed submit and after navigating back | Always | Required | Application's job |
| FRM-07 | Success is shown clearly, and focus, reset or redirect afterward are defined | Always | Required | Application's job |
| FRM-08 | Leaving with unsaved changes asks for confirmation | Editable data | If applicable | Application's job |
| FRM-09 | Draft saving or autosave shows its state, handles conflicts and failure, and does not overwrite newer data | Drafts or autosave | If applicable | Application's job |
| FRM-10 | Required and optional fields are marked consistently | Always | Required | Application's job |
| FRM-11 | Conditional fields appear and hide correctly, hidden values are cleared or kept as decided, and hidden fields are not validated | Conditional fields | If applicable | Application's job |
| FRM-12 | Reset restores the initial values (not blank ones) and asks for confirmation when data would be lost | Reset action | If applicable | Application's job |
| FRM-13 | Autofill and password managers work, with correct field purposes | Always | Required | Application's job |
| FRM-14 | Fields are handled consistently while the form is submitting | Always | Required | Application's job |
| FRM-15 | An expired session or timeout during a long form does not lose the data | Long forms | If applicable | Application's job |
| FRM-16 | Mobile keyboards, zoom to 200% and sticky headers do not hide fields, errors or actions | Always | Required | Application's job |

## 7. Anti-patterns

- A disabled submit button as the only validation feedback.
- Clearing the form after an error.
- Allowing two submissions with a quick double activation.
- Reporting only "something went wrong" for a server validation error.
- Losing the draft when the session expires.
- A reset button next to submit, with no confirmation.
- Validating hidden conditional fields.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| FRM-01 | Accessibility | Always | Labels and groups | Inspect each control and group | Named, grouped | Required | Automatable | Critical |
| FRM-02 | Keyboard | Always | Submission | Submit by Enter in a single-line field and by the submit action | Same result, Enter in a multi-line field adds a line | Required | Automatable | Critical |
| FRM-03 | Functional | Always | No repeat submission | Submit twice quickly with a slow server | One submission, loading shown | Required | Automatable | Critical |
| FRM-04 | Validation | Always | Failed validation | Submit with several invalid fields | Focus on summary or first invalid field, all errors shown | Required | Automatable | Critical |
| FRM-05 | Data | Server submission | Server errors | Return field errors, an unknown error and a network failure | Mapped, fallback, data kept | Required | Automatable | Critical |
| FRM-06 | Data | Always | Retained data | Fail a submit, navigate back and forward | All data still there | Required | Automatable | Critical |
| FRM-07 | Functional | Always | Success | Submit successfully | Clear success, defined focus and next state | Required | Automatable | Important |
| FRM-08 | Functional | Editable data | Unsaved changes | Edit and try to leave | Confirmation asked | If applicable | Automatable | Important |
| FRM-09 | Data | Drafts or autosave | Drafts | Edit, fail the save, edit in two windows | State shown, failure and conflict handled | If applicable | Automatable | Important |
| FRM-10 | Accessibility | Always | Required marking | Review all fields | Consistent | Required | Automatable | Important |
| FRM-11 | Functional | Conditional fields | Conditional fields | Show a field, enter data, hide it, submit | Hidden value handled as decided, not validated | If applicable | Automatable | Important |
| FRM-12 | Functional | Reset action | Reset | Edit an existing record and reset | Initial values restored, confirmation shown | If applicable | Automatable | Important |
| FRM-13 | Functional | Always | Autofill | Autofill and use a password manager | Fields filled and validated | Required | Manual | Important |
| FRM-14 | States | Always | During submission | Submit slowly and try to edit fields | Handled consistently | Required | Automatable | Important |
| FRM-15 | Data | Long forms | Session expiry | Let the session expire mid-form and submit | Data not lost, user can recover | If applicable | Automatable | Important |
| FRM-16 | Layout | Always | Mobile and zoom | Use a mobile keyboard, zoom to 200%, a sticky header | Nothing hidden, errors visible | Required | Manual | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
