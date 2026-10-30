---
component: Card
id-prefix: CRD
status: draft
---

# Card

## 1. When to use it vs alternatives

- **Card**: a self-contained summary of one item (product, article, person) in a collection, leading to more detail.
- **List row** or **table row** (`TBL`): items compared by attributes.
- **Plain section**: content that is not part of a collection.

## 2. Anatomy and variants

Parts: optional media, heading, text, metadata, one primary action, optional secondary actions.

Variants: whole card activatable vs only the heading, selectable card, with or without image, in a grid or a list, with a loading placeholder.

## 3. States

Default, hover, focus, selected, disabled, loading, error.

## 4. Behavior and keyboard interaction

Tab reaches the primary link and each secondary control once, in reading order.

## 5. Component-specific accessibility

- The card has a heading at the right level.
- A whole-card target does not wrap other interactive elements illegally.
- Secondary actions have names that include the card they belong to.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| CRD-01 | A heading at the right level, and one primary action with a clear name | Always | Required | Application's job |
| CRD-02 | When the whole card is activatable, one link is the target and other controls still work independently | Whole card activatable | Required | Application's job |
| CRD-03 | Images have a text alternative or are decorative, reserve their space and have a fallback | Media | Required | Application's job |
| CRD-04 | Long text, missing optional parts and unequal content keep the cards consistent | Always | Required | Application's job |
| CRD-05 | Cards in a grid reflow, keep reading order equal to visual order, and use list semantics | Grid of cards | Required | Application's job |
| CRD-06 | Focus is visible on the card and inner controls, and hover is not the only affordance | Always | Required | Application's job |
| CRD-07 | A selectable card exposes its state and works by keyboard | Selectable card | If applicable | Application's job |
| CRD-08 | Loading and error states keep the card's size | Async content | If applicable | Application's job |
| CRD-09 | Action menus and buttons have names that include the card | Secondary actions | If applicable | Application's job |
| CRD-10 | Targets are large enough, and the card works at 200% zoom and in right-to-left layout | Always | Required | Application's job |

## 7. Anti-patterns

- Wrapping a whole card in a link that contains buttons.
- Every secondary button named 'More'.
- Cards in a different DOM order than they appear.
- Image with no reserved size.
- Hover as the only way to reveal actions.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| CRD-01 | Accessibility | Always | A heading at the right level, and one primary action with a clear name | Inspect the heading and the primary action | Right level, a single clear primary action | Required | Automatable | Important |
| CRD-02 | Functional | Whole card activatable | When the whole card is activatable, one link is the target and other controls still work independently | Activate the card, then its inner controls | Primary action by card, inner controls separate | Required | Automatable | Critical |
| CRD-03 | Layout | Media | Images have a text alternative or are decorative, reserve their space and have a fallback | Render with the image missing and slow | Alt correct, no layout shift, fallback shown | Required | Automatable | Important |
| CRD-04 | Layout | Always | Long text, missing optional parts and unequal content keep the cards consistent | Use very long titles, no image, no description | Layout consistent and intact | Required | Automatable | Important |
| CRD-05 | Layout | Grid of cards | Cards in a grid reflow, keep reading order equal to visual order, and use list semantics | Resize and tab through | Order logical, list semantics present | Required | Automatable | Important |
| CRD-06 | Accessibility | Always | Focus is visible on the card and inner controls, and hover is not the only affordance | Tab through and hover | Visible focus and affordance | Required | Manual | Important |
| CRD-07 | Accessibility | Selectable card | A selectable card exposes its state and works by keyboard | Select with keyboard and screen reader | State exposed | If applicable | Automatable | Important |
| CRD-08 | States | Async content | Loading and error states keep the card's size | Load slowly and fail | Placeholder same size, error with retry | If applicable | Automatable | Important |
| CRD-09 | Accessibility | Secondary actions | Action menus and buttons have names that include the card | List the action names | Each unique and contextual | If applicable | Automatable | Important |
| CRD-10 | Layout | Always | Targets are large enough, and the card works at 200% zoom and in right-to-left layout | Zoom, mirror, touch | Usable | Required | Manual | Nice-to-have |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
