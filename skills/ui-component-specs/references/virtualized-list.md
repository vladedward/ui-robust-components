---
component: Virtualized list
id-prefix: VLS
status: draft
---

# Virtualized list

## 1. When to use it vs alternatives

- **Virtualized list**: very long lists where rendering every item would be too slow.
- **Pagination** (`PAG`) or **load more**: when position and sharing matter more than continuous scrolling.
- **Plain list**: up to a few hundred simple items.

## 2. Anatomy and variants

Parts: scroll container, rendered window of items, spacers or total height, optional placeholders.

Variants: fixed vs variable item heights, items that change size, data that grows or changes at the top, loading pages on demand.

## 3. States

Idle, scrolling, loading more, empty, error, item focused, item selected.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Arrow keys | Move between items (when the list uses item focus) |
| Home / End | First / last item, even if not yet rendered |
| PageUp / PageDown | Move by a page |

## 5. Component-specific accessibility

- The total number of items and the position of each rendered item are exposed.
- The focused item stays reachable while it scrolls out of view.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| VLS-01 | Only the visible window is rendered, and the scrollbar reflects the full length | Always | Required | Application's job |
| VLS-02 | Variable heights are measured without visible jumps, and size changes after render are absorbed | Variable heights | Required | Application's job |
| VLS-03 | Keyboard navigation works across rendered and unrendered items, Home and End jump to the ends, and the focused item is not lost when scrolled out | Always | Required | Application's job |
| VLS-04 | The set size and position of items are exposed to assistive technology | Always | Required | Application's job |
| VLS-05 | Scroll position is restored on return, and scrolling to an item that is not rendered works | Always | Required | Application's job |
| VLS-06 | Find in page and select all do not silently miss unrendered items; a search alternative exists | Long text lists | If applicable | Application's job |
| VLS-07 | Items inserted or removed above the viewport do not move what the user is looking at | Changing data | Required | Application's job |
| VLS-08 | Pages load at the ends with placeholders and failure states | On-demand loading | If applicable | Application's job |
| VLS-09 | Resizing, zooming and rotating recompute the layout correctly | Always | Required | Application's job |
| VLS-10 | Item state (focus, selection, entered text) does not leak between recycled items | Items hold state | Required | Application's job |
| VLS-11 | Empty list, a single item and huge counts are handled | Always | Required | Application's job |
| VLS-12 | Fast scrolling does not show blank areas for long | Always | Required | Application's job |

## 7. Anti-patterns

- Recycled rows keeping the previous item's checked state.
- Losing the focused element when it scrolls out.
- Total count not exposed.
- List jumping when items above the view load.
- Home and End reaching only the rendered ends.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| VLS-01 | Layout | Always | Only the visible window is rendered, and the scrollbar reflects the full length | Scroll through a very long list | Smooth, correct scrollbar size and position | Required | Automatable | Critical |
| VLS-02 | Layout | Variable heights | Variable heights are measured without visible jumps, and size changes after render are absorbed | Use items of different and changing height | No jumps, no overlap | Required | Automatable | Critical |
| VLS-03 | Keyboard | Always | Keyboard navigation works across rendered and unrendered items, Home and End jump to the ends, and the focused item is not lost when scrolled out | Focus an item, scroll away, press keys, press End | Focus preserved, jumps reach the real ends | Required | Automatable | Critical |
| VLS-04 | Accessibility | Always | The set size and position of items are exposed to assistive technology | Inspect rendered items with a screen reader | Position 'n of N' available | Required | Manual | Critical |
| VLS-05 | Functional | Always | Scroll position is restored on return, and scrolling to an item that is not rendered works | Navigate away and back, jump to a far item | Position restored, item shown | Required | Automatable | Important |
| VLS-06 | Functional | Long text lists | Find in page and select all do not silently miss unrendered items; a search alternative exists | Use the browser find on a long list | Alternative search available or limitation clear | If applicable | Manual | Important |
| VLS-07 | Data | Changing data | Items inserted or removed above the viewport do not move what the user is looking at | Insert and remove items at the top while scrolled down | View stays anchored | Required | Automatable | Critical |
| VLS-08 | States | On-demand loading | Pages load at the ends with placeholders and failure states | Scroll to the end, delay and fail loading | Placeholders, retry, no duplicates | If applicable | Automatable | Important |
| VLS-09 | Layout | Always | Resizing, zooming and rotating recompute the layout correctly | Resize, zoom to 200%, rotate | Correct window, no gaps | Required | Automatable | Important |
| VLS-10 | Data | Items hold state | Item state (focus, selection, entered text) does not leak between recycled items | Select and edit an item, scroll away and back, scroll further | State stays with its item only | Required | Automatable | Critical |
| VLS-11 | States | Always | Empty list, a single item and huge counts are handled | Render 0, 1 and a million items | Correct and responsive | Required | Automatable | Important |
| VLS-12 | Layout | Always | Fast scrolling does not show blank areas for long | Scroll very quickly | Content appears without long blanks | Required | Manual | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
