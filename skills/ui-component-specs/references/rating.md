---
component: Rating
id-prefix: RTG
status: draft
---

# Rating

## 1. When to use it vs alternatives

- **Rating input**: collecting a score from the user (stars, hearts, a numeric scale).
- **Rating display**: showing an aggregate score; it is not interactive.
- **Radio group** (`RAD`) or **dropdown** (`DD`): when the scale is short and labeled in words.
- **Slider** (`SLD`): a continuous value.

## 2. Anatomy and variants

Parts: label, scale items, optional value text, optional count of ratings, optional clear action.

Variants: input vs display only, whole vs fractional values, with an average and a count, rating saved immediately vs on submit.

## 3. States

Empty, hover preview, focus, selected value, read-only, disabled, error, saving.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| ArrowRight / ArrowUp | Increases the value by one step |
| ArrowLeft / ArrowDown | Decreases the value by one step |
| Home / End | Lowest / highest value |
| Tab | Moves in and out as one control |

## 5. Component-specific accessibility

- The value is exposed as text such as '3 of 5', not only as filled shapes.
- The label says what is being rated.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| RTG-01 | Choose a value by pointer and keyboard; the control is exposed as a single value with its range | Rating input | Required | Application's job |
| RTG-02 | A display-only rating exposes its value and count as text and is not interactive | Display only | Required | Application's job |
| RTG-03 | Fractional values display with a defined rounding, and input granularity is defined | Fractional values | If applicable | Application's job |
| RTG-04 | The rating can be cleared and a required rating is validated with an associated message | Clearable or required | If applicable | Application's job |
| RTG-05 | Hover preview does not change the value, and touch devices select without hover | Rating input | Required | Application's job |
| RTG-06 | Filled and empty items differ by shape or pattern, not color alone, with sufficient contrast | Always | Required | Application's job |
| RTG-07 | Form value, initial value, reset and retention after a failed submit | Inside a form | Required | Application's job |
| RTG-08 | Saving immediately shows pending state and reverts with an error on failure | Immediate save | If applicable | Application's job |
| RTG-09 | Direction follows right-to-left layout | Always | Required | Application's job |
| RTG-10 | A label states what is rated and what the ends of the scale mean | Always | Required | Application's job |
| RTG-11 | Items are large enough to hit and work at 200% zoom | Rating input | Required | Application's job |

## 7. Anti-patterns

- Stars exposed only as images with no value.
- Hover changing the stored value.
- Color as the only difference between filled and empty.
- A rating that cannot be cleared or corrected.
- Showing an average with no count.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| RTG-01 | Keyboard | Rating input | Choose a value by pointer and keyboard; the control is exposed as a single value with its range | Set a value by pointer, then with each key, then inspect with a screen reader | Value changes, announced as a value out of the maximum | Required | Manual | Critical |
| RTG-02 | Accessibility | Display only | A display-only rating exposes its value and count as text and is not interactive | Inspect a display rating | Text such as '4.5 out of 5, 120 ratings', no focusable parts | Required | Automatable | Important |
| RTG-03 | Data | Fractional values | Fractional values display with a defined rounding, and input granularity is defined | Display 3.2, 3.5, 3.8 and set a half value | Rendering matches the rule, stored value is exact | If applicable | Automatable | Important |
| RTG-04 | Validation | Clearable or required | The rating can be cleared and a required rating is validated with an associated message | Clear the value, submit empty when required | Empty is possible, error associated when required | If applicable | Automatable | Important |
| RTG-05 | Functional | Rating input | Hover preview does not change the value, and touch devices select without hover | Hover over items, leave, use a touch device | Value unchanged by hover, touch selects | Required | Manual | Important |
| RTG-06 | Accessibility | Always | Filled and empty items differ by shape or pattern, not color alone, with sufficient contrast | View in grayscale and check contrast | Value readable without color | Required | Manual | Important |
| RTG-07 | Data | Inside a form | Form value, initial value, reset and retention after a failed submit | Submit, reset, fail validation | Value correct, reset restores, retained after failure | Required | Automatable | Critical |
| RTG-08 | Data | Immediate save | Saving immediately shows pending state and reverts with an error on failure | Rate with a slow and a failing save | Pending shown, previous value restored on failure | If applicable | Automatable | Important |
| RTG-09 | Layout | Always | Direction follows right-to-left layout | Switch to right-to-left layout | Scale and arrow keys mirrored | Required | Manual | Nice-to-have |
| RTG-10 | Accessibility | Always | A label states what is rated and what the ends of the scale mean | Review label and scale ends | Meaning clear to all users | Required | Manual | Important |
| RTG-11 | Layout | Rating input | Items are large enough to hit and work at 200% zoom | Use a touch device and zoom | Reliable to select, nothing clipped | Required | Manual | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
