---
component: <Component name>
id-prefix: <XX>
status: draft
---

# <Component name>

> Template for every `references/<component>.md`. Keep all nine sections, in this order. Delete this note and the guidance text in each section when writing a real reference. Write capabilities, not mechanisms: state what must exist and what is observable, never which library or UI step achieves it. No implementation code, selectors or framework names.

## 1. When to use it vs alternatives

When this component fits, and when a native element or another component is a better choice (for example native select vs combobox vs radio group).

## 2. Anatomy and variants

Parts of the component, and the variants that change which capabilities apply (for example single vs multiple selection, short vs long list).

## 3. States

Default, hover, focus, open, disabled, error, loading, empty, read-only. Mark the ones that do not apply.

## 4. Behavior and keyboard interaction

Expected behavior in neutral verbs (open, close, select an option, trigger the reset action, move focus). Keyboard model as a table of key and result. Link shared behavior families by ID once traits exist.

## 5. Component-specific accessibility

Only what is specific to this component. General rules live in the `accessibility` skill and are linked, not repeated.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| XX-01 | One sentence, what must exist | Always, or the variant condition | Required / If applicable / Optional | Usually provided by primitives / Application's job |

## 7. Anti-patterns

Common wrong implementations and why they fail.

## 8. Test cases

Generic, observable behavior only. Every ID from section 6 that is testable has at least one row here.

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| XX-01 | Functional | Always | Name | What to do, in neutral verbs | Final state, form value, focus position, announcements | Required | Automatable | Critical |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
