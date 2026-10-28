---
component: Stepper / wizard
id-prefix: STP
status: draft
---

# Stepper / wizard

> Each step is a form: also apply `form.md` where it exists, and the field references for the controls inside steps.

## 1. When to use it vs alternatives

- **Stepper**: a long or complex task split into ordered steps (checkout, onboarding, application).
- **Single page form** (`FRM`): short tasks where seeing everything at once is faster.
- **Tabs** (`TAB`): unordered peer sections.
- **Progress indicator** (`PRG`): showing progress with no steps to navigate.

## 2. Anatomy and variants

Parts: step list (indicator), current step content, back, next and submit actions, optional review step, optional save for later.

Variants that change which capabilities apply:

- Linear (strict order) vs free navigation between steps
- With optional or conditional steps
- With saved progress vs in-memory only
- With one URL per step vs a single URL

## 3. States

Per step: upcoming, current, completed, error, optional, disabled. Overall: in progress, submitting, submitted, failed.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Tab / Shift+Tab | Moves through the step content and the actions |
| Enter | Activates the focused action; inside a step form, submits that step |

## 5. Component-specific accessibility

- The step indicator exposes which step is current and how many there are, without relying on color.
- A change of step moves focus to the new step and is announced.
- Errors name the step and the field.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| STP-01 | The step list shows current, completed and upcoming steps, with the position, exposed and not color-only | Always | Required | Application's job |
| STP-02 | Going forward and back keeps the data entered in every step | Always | Required | Application's job |
| STP-03 | Moving forward validates the current step with associated errors, and going back is allowed without validating | Always | Required | Application's job |
| STP-04 | The navigation rule is defined: strict order, or free jumps to completed steps, with future steps clearly locked | Always | Required | Application's job |
| STP-05 | Progress is saved so that a reload or return resumes it | Saved progress | If applicable | Application's job |
| STP-06 | On a step change focus moves to the step heading or first field, and the new step and its position are announced | Always | Required | Application's job |
| STP-07 | The final submission shows loading, prevents double submit and offers a review before sending | Always | Required | Application's job |
| STP-08 | A server error returns the user to the right step with the message, data intact | Server submission | Required | Application's job |
| STP-09 | Optional and conditional steps can be skipped or appear, and the count and progress stay correct | Optional or conditional steps | If applicable | Application's job |
| STP-10 | The browser back and forward actions and the URL match the step | One URL per step | If applicable | Application's job |
| STP-11 | Leaving with unsaved progress asks for confirmation | Progress not saved | If applicable | Application's job |
| STP-12 | Long labels and many steps adapt to small viewports and zoom | Always | Required | Application's job |
| STP-13 | After completion the success state is shown and going back cannot submit again | Always | Required | Application's job |

## 7. Anti-patterns

- Losing the data of earlier steps when going back.
- Blocking back navigation because the current step is invalid.
- Progress shown only by color or a bar with no text.
- No focus change on a step change.
- A server error that leaves the user on the last step with no sign of which step failed.
- Back after success resubmitting the order.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| STP-01 | Accessibility | Always | Step indicator | Inspect each state with a screen reader and in grayscale | Current, completed, upcoming and position exposed without color | Required | Manual | Critical |
| STP-02 | Data | Always | Data kept | Fill steps, go back and forward | All data intact | Required | Automatable | Critical |
| STP-03 | Validation | Always | Step validation | Go forward with invalid data, then go back | Forward blocked with associated errors, back allowed | Required | Automatable | Critical |
| STP-04 | Functional | Always | Navigation rule | Jump to a completed step, try an upcoming one | As defined, future steps locked | Required | Automatable | Important |
| STP-05 | Data | Saved progress | Saved progress | Fill part, reload, return later | Resumes at the right step with the data | If applicable | Automatable | Important |
| STP-06 | Keyboard | Always | Focus on step change | Go to the next step by keyboard with a screen reader | Focus in the new step, change announced | Required | Manual | Critical |
| STP-07 | Functional | Always | Final submission | Submit with a slow server, submit twice | Loading shown, one submission, review shown first | Required | Automatable | Critical |
| STP-08 | Data | Server submission | Server error | Make the server reject a field from an earlier step | User returned to that step, message shown, data intact | Required | Automatable | Critical |
| STP-09 | Functional | Optional or conditional steps | Optional and conditional steps | Skip an optional step, trigger a conditional one | Count and progress correct | If applicable | Automatable | Important |
| STP-10 | Functional | One URL per step | URL and history | Use browser back and forward, open a step URL directly | Step matches, guarded as decided | If applicable | Automatable | Important |
| STP-11 | Functional | Progress not saved | Leave protection | Leave with entered data | Confirmation asked | If applicable | Automatable | Important |
| STP-12 | Layout | Always | Small viewports and zoom | Use many long labels on a narrow viewport and at 200% zoom | Adapts, nothing clipped | Required | Manual | Important |
| STP-13 | Functional | Always | Completion | Finish, then use back | Success state shown, no duplicate submission | Required | Automatable | Critical |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
