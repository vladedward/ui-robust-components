---
component: Timeline
id-prefix: TML
status: draft
---

# Timeline

## 1. When to use it vs alternatives

- **Timeline**: events in chronological order (activity, history, order tracking).
- **Stepper** (`STP`): steps the user progresses through.
- **Table** (`TBL`): events compared across attributes.

## 2. Anatomy and variants

Parts: ordered list of events, each with a time, title, description and optional status or icon, optional grouping by date.

Variants: newest first vs oldest first, vertical vs horizontal, grouped vs flat, static vs live, with expandable details.

## 3. States

Default, event expanded, loading more, empty, new event arriving.

## 4. Behavior and keyboard interaction

Tab reaches the interactive parts of events in order. Expandable details follow the accordion keyboard rules.

## 5. Component-specific accessibility

- It is an ordered list, and the direction of order is stated.
- Times are available in a machine readable form and in text.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| TML-01 | It is an ordered list and the order direction is stated | Always | Required | Application's job |
| TML-02 | Each event has a date and time shown in the user's locale, with the time zone available and a machine readable value; relative times have an absolute form | Always | Required | Application's job |
| TML-03 | Status and order are not conveyed by position or color alone | Always | Required | Application's job |
| TML-04 | Long timelines are paged or loaded progressively with feedback | Long timelines | If applicable | Application's job |
| TML-05 | An empty timeline and a single event look right | Always | Required | Application's job |
| TML-06 | Events with the same time keep a stable order, and groups by date are labeled | Always | Required | Application's job |
| TML-07 | Expandable details work by keyboard with exposed state | Expandable events | If applicable | Application's job |
| TML-08 | The layout adapts to small viewports and keeps reading order | Always | Required | Application's job |
| TML-09 | New events inserted live do not move the user's position or focus, and are announced politely | Live updates | If applicable | Application's job |

## 7. Anti-patterns

- Relative times like '3 days ago' as the only form.
- Alternating left and right layout that breaks reading order.
- A vertical line that implies order without a list.
- Dates formatted in one fixed locale.
- New events pushing the user's view.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| TML-01 | Accessibility | Always | It is an ordered list and the order direction is stated | Inspect semantics and read the order | List with stated order | Required | Automatable | Important |
| TML-02 | Data | Always | Each event has a date and time shown in the user's locale, with the time zone available and a machine readable value; relative times have an absolute form | Show events across time zones, daylight saving, locales | Correct and consistent, absolute time available | Required | Automatable | Critical |
| TML-03 | Accessibility | Always | Status and order are not conveyed by position or color alone | View in grayscale | Status in text | Required | Manual | Important |
| TML-04 | States | Long timelines | Long timelines are paged or loaded progressively with feedback | Load a very long timeline | Responsive, loading and failure shown | If applicable | Automatable | Important |
| TML-05 | States | Always | An empty timeline and a single event look right | Render with zero and one events | Meaningful empty state, no broken line | Required | Automatable | Important |
| TML-06 | Data | Always | Events with the same time keep a stable order, and groups by date are labeled | Use identical timestamps and grouping across midnight | Stable order, correct groups | Required | Automatable | Important |
| TML-07 | Keyboard | Expandable events | Expandable details work by keyboard with exposed state | Expand by keyboard | State exposed | If applicable | Automatable | Important |
| TML-08 | Layout | Always | The layout adapts to small viewports and keeps reading order | Resize and tab through | Readable and ordered | Required | Automatable | Important |
| TML-09 | Functional | Live updates | New events inserted live do not move the user's position or focus, and are announced politely | Add events while scrolled and focused | Position and focus kept | If applicable | Automatable | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
