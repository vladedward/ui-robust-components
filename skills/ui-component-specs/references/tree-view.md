---
component: Tree view
id-prefix: TRV
status: draft
---

# Tree view

## 1. When to use it vs alternatives

- **Tree view**: hierarchical data the user navigates by expanding and collapsing (files, categories, outlines).
- **Tree select** (inside `dropdown.md`): choosing a value from a hierarchy.
- **Accordion** (`ACC`): a few sections, one level.
- **Sidebar** (`SID`): navigation with nesting.

## 2. Anatomy and variants

Parts: tree, nodes (branches and leaves), expand toggles, labels, optional checkboxes, optional icons.

Variants: single vs multiple selection, with checkboxes, lazy loaded children, drag and drop, inline rename, very large trees.

## 3. States

Collapsed, expanded, focused, selected, checked, indeterminate, loading children, empty branch, error.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| ArrowDown / ArrowUp | Next / previous visible node |
| ArrowRight | Expands a collapsed branch, or moves to its first child |
| ArrowLeft | Collapses an expanded branch, or moves to its parent |
| Home / End | First / last visible node |
| Enter / Space | Activates or selects the node |
| Typeahead | Moves to the matching node |

## 5. Component-specific accessibility

- Tree and node roles, expanded state, level and position are exposed.
- The tree is one tab stop.
- Arrow keys are mirrored in right-to-left layout.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| TRV-01 | Roles, expanded state, level and position in the set are exposed | Always | Required | Usually provided by primitives |
| TRV-02 | Arrow keys, Home, End and typeahead navigate as specified | Always | Required | Usually provided by primitives |
| TRV-03 | The tree is a single tab stop with moving focus | Always | Required | Usually provided by primitives |
| TRV-04 | Selection model is defined: focus vs selection, single or multiple, checkbox trees with indeterminate parents | Selection | If applicable | Application's job |
| TRV-05 | Children can load lazily, with loading, empty-branch and failure states | Lazy children | If applicable | Application's job |
| TRV-06 | The expand toggle and the node label are separate, sufficiently large targets | Always | Required | Application's job |
| TRV-07 | Large trees and deep nesting stay responsive and readable | Large trees | If applicable | Application's job |
| TRV-08 | Expanded nodes persist and the current node is scrolled into view | Tree is navigation or state | If applicable | Application's job |
| TRV-09 | Reordering by dragging has a keyboard alternative | Drag and drop | If applicable | Application's job |
| TRV-10 | Renaming inline has a defined start, commit and cancel | Rename | If applicable | Application's job |
| TRV-11 | Branches and leaves differ by more than color | Always | Required | Application's job |
| TRV-12 | Nodes added or removed while viewing keep focus valid | Dynamic data | If applicable | Application's job |
| TRV-13 | Arrow keys are mirrored in right-to-left layout | Always | Required | Usually provided by primitives |

## 7. Anti-patterns

- Every node a tab stop.
- Selection tied to expansion.
- A toggle too small to hit.
- Focus lost when a branch collapses over the focused child.
- Indentation by spaces that screen readers read.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| TRV-01 | Accessibility | Always | Roles, expanded state, level and position in the set are exposed | Inspect nodes and use a screen reader | Role, level, position and state announced | Required | Manual | Critical |
| TRV-02 | Keyboard | Always | Arrow keys, Home, End and typeahead navigate as specified | Use each key | Focus moves as specified | Required | Automatable | Critical |
| TRV-03 | Keyboard | Always | The tree is a single tab stop with moving focus | Tab through the page | One stop, entering at the current or first node | Required | Automatable | Critical |
| TRV-04 | Functional | Selection | Selection model is defined: focus vs selection, single or multiple, checkbox trees with indeterminate parents | Select, multi-select, check a parent | Selection and mixed states as defined | If applicable | Automatable | Critical |
| TRV-05 | States | Lazy children | Children can load lazily, with loading, empty-branch and failure states | Expand a branch slowly, with none, and failing | Loading, empty and error shown | If applicable | Automatable | Important |
| TRV-06 | Layout | Always | The expand toggle and the node label are separate, sufficiently large targets | Use the toggle and the label by pointer and touch | Each does its own action | Required | Manual | Important |
| TRV-07 | Layout | Large trees | Large trees and deep nesting stay responsive and readable | Use thousands of nodes and ten levels | Responsive, indentation does not overflow | If applicable | Manual | Important |
| TRV-08 | Data | Tree is navigation or state | Expanded nodes persist and the current node is scrolled into view | Expand, navigate away and back | State restored, current node visible | If applicable | Automatable | Important |
| TRV-09 | Keyboard | Drag and drop | Reordering by dragging has a keyboard alternative | Move a node with the keyboard | Result the same as dragging | If applicable | Manual | Important |
| TRV-10 | Functional | Rename | Renaming inline has a defined start, commit and cancel | Rename, commit, cancel, enter a duplicate | As defined, conflicts reported | If applicable | Automatable | Important |
| TRV-11 | Accessibility | Always | Branches and leaves differ by more than color | View in grayscale | Distinct | Required | Manual | Important |
| TRV-12 | Data | Dynamic data | Nodes added or removed while viewing keep focus valid | Remove the focused node | Focus moves to a logical node | If applicable | Automatable | Important |
| TRV-13 | Keyboard | Always | Arrow keys are mirrored in right-to-left layout | Use ArrowLeft and ArrowRight in right-to-left layout | Mirrored | Required | Automatable | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
