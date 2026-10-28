---
component: Slider / range
id-prefix: SLD
status: draft
---

# Slider / range

## 1. When to use it vs alternatives

- **Slider**: choosing an approximate value within a known range where exactness is not essential (volume, brightness, a price range filter).
- **Number input** (`NUM`): an exact value. Sliders often need one next to them.
- **Dropdown** (`DD`) or **radio group** (`RAD`): a few discrete values.
- **Stepper controls**: small adjustments of a quantity.

## 2. Anatomy and variants

Parts: track, filled range, thumb (one or two), label, value display, optional tick marks and labels, optional input for exact values.

Variants that change which capabilities apply:

- Single value vs a range with two thumbs
- Continuous vs stepped (discrete)
- Linear vs non-linear scale
- Updates continuously vs when released
- Horizontal vs vertical

## 3. States

Default, hover, focus, dragging, disabled, read-only, at minimum, at maximum, error.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| ArrowRight / ArrowUp | Increase by one step |
| ArrowLeft / ArrowDown | Decrease by one step |
| PageUp / PageDown | Increase / decrease by a larger step |
| Home / End | Set the minimum / maximum |

In right-to-left layout the horizontal arrows are mirrored.

## 5. Component-specific accessibility

- Each thumb exposes its role, name, current value and range, with a value text that includes units when the number alone is not clear.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| SLD-01 | Role, name, value, range and a meaningful value text are exposed for each thumb | Always | Required | Usually provided by primitives |
| SLD-02 | Arrow, page, Home and End keys change the value as specified | Always | Required | Usually provided by primitives |
| SLD-03 | Pointer and touch dragging and activating the track work, dragging continues outside the track, and touch dragging does not scroll the page | Always | Required | Usually provided by primitives |
| SLD-04 | Minimum, maximum and step are enforced with snapping, and non-linear scales map correctly | Always | Required | Application's job |
| SLD-05 | The current value is displayed, updated while dragging, and an exact value can be entered where precision matters | Value display or precision | If applicable | Application's job |
| SLD-06 | Two thumbs cannot cross, or the crossing rule is defined, a minimum distance is respected, and each thumb is named and focusable in order | Range | If applicable | Application's job |
| SLD-07 | Disabled and read-only states | Always | Required | Usually provided by primitives |
| SLD-08 | The form value is submitted, the initial value shown and reset restores it | Inside a form | Required | Application's job |
| SLD-09 | The value is applied as decided: continuously, or when released for expensive work | Expensive updates | If applicable | Application's job |
| SLD-10 | Tick marks and labels are aligned with values and not announced as noise | Ticks | If applicable | Application's job |
| SLD-11 | Vertical orientation and right-to-left layout use the right directions | Vertical or right-to-left | If applicable | Usually provided by primitives |
| SLD-12 | The thumb target is large enough, and the control works at 200% zoom | Always | Required | Application's job |

## 7. Anti-patterns

- A slider as the only way to enter a precise value.
- A thumb without a name or value text.
- Touch dragging that scrolls the page instead.
- Two thumbs that can pass each other and swap meaning.
- Sending a request on every pixel of dragging.
- Value shown only while dragging.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| SLD-01 | Accessibility | Always | Exposed semantics | Inspect and use a screen reader | Name, value, range and value text announced | Required | Manual | Critical |
| SLD-02 | Keyboard | Always | Keyboard | Use each key from the table | Values as specified, limits respected | Required | Automatable | Critical |
| SLD-03 | Functional | Always | Pointer and touch | Drag, activate the track, drag outside the track, drag on a touch device | Value follows, page does not scroll | Required | Manual | Critical |
| SLD-04 | Data | Always | Limits and snapping | Set values beyond limits and between steps, use a non-linear scale | Snapped and in range | Required | Automatable | Important |
| SLD-05 | Functional | Value display or precision | Value display and exact entry | Drag and type an exact value | Display matches, entry syncs the thumb | If applicable | Automatable | Important |
| SLD-06 | Functional | Range | Two thumbs | Move one thumb across the other, tab between them | Crossing rule held, both reachable | If applicable | Automatable | Critical |
| SLD-07 | States | Always | Disabled and read-only | Try to change in each state | Unchanged | Required | Automatable | Important |
| SLD-08 | Data | Inside a form | Form value | Submit, reset | Value correct, reset restores | Required | Automatable | Critical |
| SLD-09 | Functional | Expensive updates | Applying the value | Drag with an expensive action | Applied as decided, no request storm | If applicable | Automatable | Important |
| SLD-10 | Layout | Ticks | Ticks | Compare ticks with values | Aligned | If applicable | Manual | Nice-to-have |
| SLD-11 | Keyboard | Vertical or right-to-left | Orientation | Use keys in each layout | Directions right | If applicable | Automatable | Important |
| SLD-12 | Layout | Always | Target and zoom | Use a touch device, zoom to 200% | Usable | Required | Manual | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
