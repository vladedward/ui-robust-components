---
component: Data grid (editing, virtualization)
id-prefix: GRD
status: draft
---

# Data grid (editing, virtualization)

> Extends `table.md`. Use a plain table when cells are only read. A data grid has cell-by-cell keyboard navigation, editing or large data. Also verify the table capabilities that apply (empty, loading, error, sorting, filtering, selection, pagination).

## 1. When to use it vs alternatives

- **Data grid**: spreadsheet-like data with cell navigation, inline editing, selection, large data sets.
- **Table** (`TBL`): read-only tabular data.
- **Form with repeated rows**: a small, fixed number of editable rows.

## 2. Anatomy and variants

Parts: header cells, row headers, cells, editor inside a cell, optional pinned rows and columns, optional group rows, toolbar.

Variants: read-only vs editable cells, virtualized rows or columns, with grouping or tree data, with range selection, with pinned parts.

## 3. States

Cell focused, cell selected, cell in edit mode, cell invalid, row selected, dirty cell, loading rows, error.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Arrow keys | Move between cells |
| Home / End | First / last cell in the row |
| Ctrl+Home / Ctrl+End | First / last cell of the grid |
| PageUp / PageDown | Move by a page of rows |
| Enter or F2 | Start editing, or commit when editing |
| Escape | Cancel editing |
| Tab | Next cell, or out of the grid as decided |

## 5. Component-specific accessibility

- The grid is one tab stop with moving focus inside.
- Row and column counts and the position are exposed when only part is rendered.
- Moving focus announces the cell with its headers.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| GRD-01 | The grid is a single tab stop, arrow keys move between cells, with Home, End and page keys | Always | Required | Usually provided by primitives |
| GRD-02 | Cells enter and leave edit mode in a defined way, and Escape cancels and Enter commits | Editable | If applicable | Application's job |
| GRD-03 | Cell validation shows an associated message, and the rule for leaving an invalid cell is defined | Editable | If applicable | Application's job |
| GRD-04 | With virtualization the total and the position of rows and columns are exposed, and focus survives scrolling | Virtualized | If applicable | Application's job |
| GRD-05 | Cell, row and range selection work by keyboard and pointer, with select all and copy | Selection | If applicable | Application's job |
| GRD-06 | Sorting and filtering from headers are keyboard operable and exposed | Sorting or filtering | If applicable | Application's job |
| GRD-07 | Resizing, reordering and pinning columns are possible by keyboard | Column customization | If applicable | Application's job |
| GRD-08 | Pinned rows and columns keep a logical focus order and do not hide the focused cell | Pinned parts | If applicable | Application's job |
| GRD-09 | Edits are tracked: dirty cells are marked, saves can partly fail, and undo and redo work | Editable | If applicable | Application's job |
| GRD-10 | Rows load progressively with loading and failure states | Async rows | If applicable | Application's job |
| GRD-11 | Large data sets stay responsive and scroll position is restored | Large data | If applicable | Application's job |
| GRD-12 | Group and tree rows expand and collapse by keyboard with exposed state | Grouping or tree data | If applicable | Application's job |
| GRD-13 | Interactive content in cells has a defined interaction mode that does not break arrow navigation | Interactive cells | If applicable | Application's job |
| GRD-14 | Headers and row headers are associated, and the cell is announced with them on focus | Always | Required | Application's job |

## 7. Anti-patterns

- Treating a data grid as a table with arrow keys added later.
- Every cell a tab stop.
- Edit mode that cannot be left with the keyboard.
- Virtualization that drops the focused row.
- Losing edits when sorting or scrolling.
- Row counts not exposed when only some rows exist.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| GRD-01 | Keyboard | Always | The grid is a single tab stop, arrow keys move between cells, with Home, End and page keys | Tab into the grid, use each navigation key | Focus moves as specified, one tab stop | Required | Automatable | Critical |
| GRD-02 | Keyboard | Editable | Cells enter and leave edit mode in a defined way, and Escape cancels and Enter commits | Edit, commit, cancel, move away while editing | Value committed or restored as defined, focus logical | If applicable | Automatable | Critical |
| GRD-03 | Validation | Editable | Cell validation shows an associated message, and the rule for leaving an invalid cell is defined | Enter invalid values and try to move on | Message associated, behavior as defined | If applicable | Automatable | Critical |
| GRD-04 | Accessibility | Virtualized | With virtualization the total and the position of rows and columns are exposed, and focus survives scrolling | Scroll far, move focus, use a screen reader | Counts and positions announced, focus kept | If applicable | Manual | Critical |
| GRD-05 | Functional | Selection | Cell, row and range selection work by keyboard and pointer, with select all and copy | Select with Shift+arrows, select all, copy | Selection and clipboard as defined | If applicable | Automatable | Important |
| GRD-06 | Keyboard | Sorting or filtering | Sorting and filtering from headers are keyboard operable and exposed | Sort and filter without a pointer | Operable, state exposed | If applicable | Automatable | Important |
| GRD-07 | Keyboard | Column customization | Resizing, reordering and pinning columns are possible by keyboard | Resize, reorder and pin by keyboard | Operable, announced | If applicable | Manual | Nice-to-have |
| GRD-08 | Layout | Pinned parts | Pinned rows and columns keep a logical focus order and do not hide the focused cell | Navigate across pinned parts | Focused cell always visible | If applicable | Automatable | Important |
| GRD-09 | Data | Editable | Edits are tracked: dirty cells are marked, saves can partly fail, and undo and redo work | Edit several cells, fail one save, undo | Dirty marked, partial failure reported, undo works | If applicable | Automatable | Important |
| GRD-10 | States | Async rows | Rows load progressively with loading and failure states | Scroll to unloaded rows, fail a load | Placeholder, error with retry | If applicable | Automatable | Important |
| GRD-11 | Data | Large data | Large data sets stay responsive and scroll position is restored | Load a very large data set, navigate away and back | Responsive, position restored | If applicable | Manual | Important |
| GRD-12 | Keyboard | Grouping or tree data | Group and tree rows expand and collapse by keyboard with exposed state | Expand and collapse groups by keyboard | State exposed, focus logical | If applicable | Automatable | Important |
| GRD-13 | Keyboard | Interactive cells | Interactive content in cells has a defined interaction mode that does not break arrow navigation | Move through cells with buttons and inputs | Navigation and control use are both possible | If applicable | Automatable | Critical |
| GRD-14 | Accessibility | Always | Headers and row headers are associated, and the cell is announced with them on focus | Move focus with a screen reader | Cell content with its headers announced | Required | Manual | Critical |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
