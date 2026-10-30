---
component: Charts (accessibility level)
id-prefix: CHT
status: draft
---

# Charts (accessibility level)

> Covers the accessibility and data-handling level of charts, not how to design a good visualization.

## 1. When to use it vs alternatives

- **Chart**: showing trends, comparisons or distributions that text would make hard to grasp.
- **Table** (`TBL`): when exact values matter. Offer it next to or behind the chart.
- **Plain text or a single number**: when one figure is the message.

## 2. Anatomy and variants

Parts: title, plot, axes with units, series, legend, optional tooltips, optional controls (filters, zoom).

Variants: static vs interactive, single vs multiple series, small vs very large data sets, live data.

## 3. States

Loading, empty, partial data, error, hover and focus on a data point, series toggled off.

## 4. Behavior and keyboard interaction

Interactive charts expose data points to the keyboard: arrows move between points and the tooltip appears on focus.

## 5. Component-specific accessibility

- A text summary of the main point and a data table or description are available.
- Color is never the only way to tell series apart.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| CHT-01 | A text alternative states the key message, and the data is available as a table or description | Always | Required | Application's job |
| CHT-02 | Series are distinguished by more than color (labels, patterns, shapes) and meet contrast, in a way usable with color blindness | Always | Required | Application's job |
| CHT-03 | Title, axes, units and legend are present, and scales are honest (bars start at zero) | Always | Required | Application's job |
| CHT-04 | Data points are reachable by keyboard and tooltips appear on focus as well as hover | Interactive | If applicable | Application's job |
| CHT-05 | A legend that toggles series exposes state and works by keyboard | Interactive legend | If applicable | Application's job |
| CHT-06 | Empty, loading, error, single point, all zero and extreme outliers are handled | Always | Required | Application's job |
| CHT-07 | Resizing keeps labels readable, without collisions, with a minimum size | Always | Required | Application's job |
| CHT-08 | Very large data is reduced or summarized in a stated way and stays responsive | Large data sets | If applicable | Application's job |
| CHT-09 | Numbers, dates and negative values are formatted per locale, and missing data is a gap, not zero | Always | Required | Application's job |
| CHT-10 | Animation respects reduced motion | Animated | Required | Application's job |
| CHT-11 | Dark mode, high contrast mode and print remain readable | Always | Required | Application's job |
| CHT-12 | Live updates do not disorient or flood announcements | Live data | If applicable | Application's job |
| CHT-13 | Zoom and pan have keyboard alternatives and a reset | Zoom or pan | If applicable | Application's job |

## 7. Anti-patterns

- A chart image with no text alternative.
- Series told apart only by hue.
- A truncated axis that exaggerates a change.
- Missing values drawn as zero.
- Tooltips available only on hover.
- Announcing every data update.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| CHT-01 | Accessibility | Always | A text alternative states the key message, and the data is available as a table or description | Inspect with a screen reader | Summary and data reachable | Required | Manual | Critical |
| CHT-02 | Accessibility | Always | Series are distinguished by more than color (labels, patterns, shapes) and meet contrast, in a way usable with color blindness | Simulate color blindness and grayscale | All series distinguishable | Required | Manual | Critical |
| CHT-03 | Data | Always | Title, axes, units and legend are present, and scales are honest (bars start at zero) | Review each chart | Complete and not misleading | Required | Manual | Important |
| CHT-04 | Keyboard | Interactive | Data points are reachable by keyboard and tooltips appear on focus as well as hover | Move through points by keyboard | Each point and its value reachable | If applicable | Automatable | Critical |
| CHT-05 | Keyboard | Interactive legend | A legend that toggles series exposes state and works by keyboard | Toggle series by keyboard | State exposed, chart updates | If applicable | Automatable | Important |
| CHT-06 | States | Always | Empty, loading, error, single point, all zero and extreme outliers are handled | Render each case | Meaningful state, no broken scale | Required | Automatable | Critical |
| CHT-07 | Layout | Always | Resizing keeps labels readable, without collisions, with a minimum size | Resize to very small and large | Readable, no overlap | Required | Automatable | Important |
| CHT-08 | Data | Large data sets | Very large data is reduced or summarized in a stated way and stays responsive | Load a very large data set | Responsive, reduction stated | If applicable | Manual | Important |
| CHT-09 | Data | Always | Numbers, dates and negative values are formatted per locale, and missing data is a gap, not zero | Use nulls, negatives and different locales | Correct formatting, gaps preserved | Required | Automatable | Critical |
| CHT-10 | Accessibility | Animated | Animation respects reduced motion | Enable reduced motion | Reduced | Required | Manual | Nice-to-have |
| CHT-11 | Layout | Always | Dark mode, high contrast mode and print remain readable | Check each mode | Readable | Required | Manual | Important |
| CHT-12 | Accessibility | Live data | Live updates do not disorient or flood announcements | Stream updates with a screen reader | Limited announcements | If applicable | Manual | Important |
| CHT-13 | Keyboard | Zoom or pan | Zoom and pan have keyboard alternatives and a reset | Zoom and pan by keyboard | Operable, reset available | If applicable | Automatable | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
