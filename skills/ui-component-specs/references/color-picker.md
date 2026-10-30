---
component: Color picker
id-prefix: CLR
status: draft
---

# Color picker

## 1. When to use it vs alternatives

- **Color picker**: choosing an arbitrary color (theme editors, design tools).
- **Swatches or a dropdown** (`DD`): a limited palette is enough and safer.
- **Text input** (`TXT`): when users already have the color code.

## 2. Anatomy and variants

Parts: color area, hue slider, optional alpha slider, text input for the value, optional preset swatches, preview, optional eyedropper.

Variants: with or without alpha, presets only vs free color, output format (hex, rgb, hsl), inline vs inside a popover.

## 3. States

Empty, a color selected, dragging, focus, invalid typed value, disabled, read-only.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Arrow keys on the color area | Move saturation and brightness |
| Arrow keys on a slider | Change hue or alpha by a step |
| Page keys, Home, End | Larger steps, ends of the range |
| Enter on a swatch | Selects it |

## 5. Component-specific accessibility

- Colors are named or described in text, not only shown.
- Each slider and the area expose name, value and range.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| CLR-01 | A color can be chosen by pointer and by keyboard in the area and the sliders, and typed | Always | Required | Application's job |
| CLR-02 | Typed formats are accepted or rejected clearly: with and without a hash, shorthand, case, rgb, hsl | Typed input | Required | Application's job |
| CLR-03 | Alpha is optional, shown and output in a defined format | Alpha channel | If applicable | Application's job |
| CLR-04 | Presets are keyboard operable and named in text | Presets | If applicable | Application's job |
| CLR-05 | The current color is available in text for assistive technology | Always | Required | Application's job |
| CLR-06 | A contrast check against the intended background is offered | Used for text or backgrounds | Optional | Application's job |
| CLR-07 | An eyedropper is offered where supported, with a graceful absence otherwise | Eyedropper | Optional | Application's job |
| CLR-08 | Empty and default are distinct from black, and the value can be cleared | Optional color | If applicable | Application's job |
| CLR-09 | When shown in a popup, it dismisses, returns focus and positions like a popover | In a popover | If applicable | Application's job |
| CLR-10 | The form value uses a normalized format, resets, and survives a failed submit | Inside a form | Required | Application's job |
| CLR-11 | Touch dragging does not scroll the page, and targets are large enough | Touch devices | Required | Application's job |

## 7. Anti-patterns

- Only a visual picker with no way to type or hear the value.
- Hex input that rejects a leading hash or lowercase.
- Hue sliders that rely on seeing the color to be usable.
- Treating no color as black.
- A picker that traps focus in the color area.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| CLR-01 | Keyboard | Always | A color can be chosen by pointer and by keyboard in the area and the sliders, and typed | Set a color with the pointer, with each key, and by typing | Value updates everywhere and the same color results | Required | Automatable | Critical |
| CLR-02 | Validation | Typed input | Typed formats are accepted or rejected clearly: with and without a hash, shorthand, case, rgb, hsl | Type '#fff', 'FFF', '#FFFFFF', 'rgb(1,2,3)', and invalid text | Valid forms accepted and normalized, invalid reported | Required | Automatable | Critical |
| CLR-03 | Data | Alpha channel | Alpha is optional, shown and output in a defined format | Change alpha and read the output value | Format as defined, alpha preserved | If applicable | Automatable | Important |
| CLR-04 | Accessibility | Presets | Presets are keyboard operable and named in text | Tab to presets and inspect names | Each has a text name or value | If applicable | Manual | Important |
| CLR-05 | Accessibility | Always | The current color is available in text for assistive technology | Use a screen reader on the area and sliders | Color name or value announced as it changes | Required | Manual | Critical |
| CLR-06 | Accessibility | Used for text or backgrounds | A contrast check against the intended background is offered | Pick low contrast colors | Warning shown | Optional | Automatable | Nice-to-have |
| CLR-07 | Functional | Eyedropper | An eyedropper is offered where supported, with a graceful absence otherwise | Use in supported and unsupported browsers | Works or is hidden cleanly | Optional | Manual | Nice-to-have |
| CLR-08 | States | Optional color | Empty and default are distinct from black, and the value can be cleared | Clear the value and submit | Empty value, not black | If applicable | Automatable | Important |
| CLR-09 | Keyboard | In a popover | When shown in a popup, it dismisses, returns focus and positions like a popover | Open, press Escape, open near an edge | Closed with focus returned, fully visible | If applicable | Automatable | Important |
| CLR-10 | Data | Inside a form | The form value uses a normalized format, resets, and survives a failed submit | Submit, reset, fail validation | Normalized value, reset works, value kept | Required | Automatable | Critical |
| CLR-11 | Layout | Touch devices | Touch dragging does not scroll the page, and targets are large enough | Drag on a touch device | Selection follows the finger, page stays | Required | Manual | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
