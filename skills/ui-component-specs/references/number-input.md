---
component: Number input / stepper
id-prefix: NUM
status: draft
---

# Number input / stepper

> Builds on `text-input.md`. Also verify the text input capabilities that apply (label, validation timing, paste, error association).

## 1. When to use it vs alternatives

- **Number input**: a quantity or measurement where arithmetic is meaningful (amount, age, count).
- **Text input** (`TXT`) with a numeric keyboard: identifiers that only look like numbers (phone, postal code, card, ID). Leading zeros and length matter, arithmetic does not.
- **Slider** (`SLD`): an approximate value within a range, where exactness is not needed.
- **Dropdown** (`DD`) or **radio group** (`RAD`): a small set of allowed values.

## 2. Anatomy and variants

Parts: label, input, optional increment and decrement controls, optional unit as prefix or suffix, helper and error text.

Variants that change which capabilities apply:

- Integer vs decimal
- With vs without minimum, maximum and step
- With vs without increment and decrement controls
- With a unit or a currency
- Locale with a different decimal separator and grouping

## 3. States

Empty, filled, focus, at minimum, at maximum, disabled, read-only, error.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| ArrowUp / ArrowDown | Increase / decrease by the step, when steppers exist |
| PageUp / PageDown | Increase / decrease by a larger step, where defined |
| Home / End | Set the minimum / maximum, where defined |
| Typing | Accepts digits, the locale decimal separator and a sign where allowed |

## 5. Component-specific accessibility

- The unit and the limits are part of the label or the associated hint.
- Increment and decrement controls have names, or are hidden from assistive technology when the field itself supports arrow keys.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| NUM-01 | Valid characters are accepted and the rest are handled without breaking input or paste | Always | Required | Application's job |
| NUM-02 | Minimum, maximum and step are enforced, and the behavior for typed values out of range (correct or report) is defined | Limits or step | If applicable | Application's job |
| NUM-03 | Arrow keys, larger steps and the increment and decrement controls work and stop at the limits | Steppers | If applicable | Usually provided by primitives |
| NUM-04 | Empty and zero are different, in the display and in the value | Always | Required | Application's job |
| NUM-05 | The decimal separator and grouping follow the locale, including for pasted text | Always | Required | Application's job |
| NUM-06 | Scrolling the page with the pointer over the field does not change the value | Always | Required | Application's job |
| NUM-07 | Floating point and rounding errors do not show up in the value or the display | Decimals | Required | Application's job |
| NUM-08 | Negative values, leading zeros, exponent notation and very large numbers are handled | Always | Required | Application's job |
| NUM-09 | Pasted text with spaces, units or currency symbols is cleaned or rejected clearly | Always | Required | Application's job |
| NUM-10 | The unit or currency is associated with the field and not part of the value | Unit or currency | If applicable | Application's job |
| NUM-11 | Mobile keyboards offer the right layout, and validation happens at the right moment | Always | Required | Application's job |
| NUM-12 | Disabled, read-only and error states, with the message associated with the field | Always | Required | Application's job |
| NUM-13 | Holding a stepper control repeats the step at a reasonable speed and stops at the limit | Steppers | If applicable | Application's job |
| NUM-14 | Identifiers keep their leading zeros and length, and are not stored as numbers | Identifier values | If applicable | Application's job |

## 7. Anti-patterns

- A number input for postal codes, phone numbers or card numbers.
- Scroll wheel changing the value by accident.
- `0.1 + 0.2` shown as `0.30000000000000004`.
- Treating an empty field as zero.
- Accepting a comma as decimal in the display but a dot only in the parser.
- Steppers with no limits, going below the minimum.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| NUM-01 | Data | Always | Accepted characters | Type letters, signs and separators, paste mixed text | Only valid input kept, no crash | Required | Automatable | Critical |
| NUM-02 | Validation | Limits or step | Limits | Type below the minimum, above the maximum, off the step | Corrected or reported as decided | If applicable | Automatable | Critical |
| NUM-03 | Keyboard | Steppers | Stepping | Use arrows, page keys and the controls at the limits | Steps correctly, stops at limits | If applicable | Automatable | Important |
| NUM-04 | Data | Always | Empty vs zero | Clear the field and enter 0, then submit | Distinct values | Required | Automatable | Critical |
| NUM-05 | Data | Always | Locale | Use locales with comma and dot decimals, paste "1.234,56" and "1,234.56" | Parsed per locale or rejected clearly | Required | Automatable | Critical |
| NUM-06 | Functional | Always | Scroll wheel | Scroll with the pointer over the focused and unfocused field | Value unchanged | Required | Automatable | Important |
| NUM-07 | Data | Decimals | Precision | Add 0.1 repeatedly, enter many decimals | Clean values, rounding as defined | Required | Automatable | Important |
| NUM-08 | Data | Always | Extreme values | Enter negatives, 007, 1e5 and a huge number | Handled consistently | Required | Automatable | Important |
| NUM-09 | Data | Always | Pasted text | Paste "12 kg", "$1,200", " 42 " | Cleaned or rejected with a message | Required | Automatable | Important |
| NUM-10 | Accessibility | Unit or currency | Unit | Inspect label and value | Unit available to assistive technology, value is numeric | If applicable | Automatable | Important |
| NUM-11 | Functional | Always | Mobile keyboard | Use a real device | Appropriate keyboard, no premature errors | Required | Manual | Nice-to-have |
| NUM-12 | Validation | Always | States | Submit invalid, set disabled and read-only | Error associated, states respected | Required | Automatable | Important |
| NUM-13 | Functional | Steppers | Press and hold | Hold a stepper control | Repeats then stops at the limit | If applicable | Automatable | Nice-to-have |
| NUM-14 | Data | Identifier values | Identifiers | Enter 00123 and submit | Leading zeros kept | If applicable | Automatable | Critical |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
