---
component: Table
id-prefix: TBL
status: draft
---

# Table

## 1. When to use it vs alternatives

- **Table**: tabular data compared across rows and columns.
- **List or cards**: items that are not compared by attributes, or that need rich layouts.
- **Data grid** (`GRD`): inline editing, virtualization and cell-level keyboard navigation.
- **Description list**: one item's attributes.
- Never use a table for layout.

## 2. Anatomy and variants

Parts: caption or name, header row and header cells, body rows, cells, optional toolbar (search, filters), optional selection column, optional row actions, optional pagination, optional footer.

Variants that change which capabilities apply:

- Static vs data loaded asynchronously
- With sorting, filtering, row selection, pagination, expandable rows
- Short vs large data sets
- Wide tables that need horizontal scroll or a stacked layout on small viewports
- With sticky headers or columns

## 3. States

Default, loading (first load and refresh), empty, no results after filtering, error, partial failure, row hover, row focus, row selected, sorted, filtered, row expanded.

## 4. Behavior and keyboard interaction

A table is read like a document: every control inside it (sort, select, action) is reachable in a logical order.

| Key | Result |
|---|---|
| Tab / Shift+Tab | Moves between interactive controls (sort controls, selection, row actions) |
| Enter / Space | Activates the focused control |

Cell-by-cell arrow navigation belongs to the data grid pattern (`GRD`), not to a table.

## 5. Component-specific accessibility

- A table has an accessible name, header cells are associated with data cells.
- Sort direction is exposed on the sorted column.
- Row actions have names that include the row context.
- Changes in results (filter, page) are announced.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| TBL-01 | Semantic structure: name, header cells associated with data cells | Always | Required | Application's job |
| TBL-02 | Empty state with a message and, where relevant, a next step | Always | Required | Application's job |
| TBL-03 | Loading state for first load and refresh, without layout shift | Async data | If applicable | Application's job |
| TBL-04 | Error state with retry, and partial failure handling | Async data | If applicable | Application's job |
| TBL-05 | Sorting with visible indicator, exposed direction, stable order and a defined cycle | Sorting | If applicable | Application's job |
| TBL-06 | Filtering with result count, a no results state and a clear filters action | Filtering | If applicable | Application's job |
| TBL-07 | Row selection: select a row, select the page, select all, mixed state, selected count, clear | Row selection | If applicable | Application's job |
| TBL-08 | Pagination: boundaries, page size change, a page that no longer exists after data shrinks, state in the URL | Pagination | If applicable | Application's job |
| TBL-09 | Long cell content wraps or is truncated with the full value available | Always | Required | Application's job |
| TBL-10 | Sticky header or column stays aligned and does not hide content | Sticky parts | If applicable | Application's job |
| TBL-11 | Small viewports: horizontal scroll that is keyboard reachable, or a stacked layout that keeps headers associated | Always | Required | Application's job |
| TBL-12 | Numbers, dates and missing values are formatted consistently by locale, with an explicit placeholder for no value | Always | Required | Application's job |
| TBL-13 | Row actions are keyboard accessible and named with their row | Row actions | If applicable | Application's job |
| TBL-14 | Data changing while viewing keeps selection, sort and position, and announces relevant updates | Live data | If applicable | Application's job |
| TBL-15 | Large data sets stay responsive and keyboard accessible | Large data | If applicable | Application's job |
| TBL-16 | Special characters, emoji and very long unbroken strings display safely | Always | Required | Application's job |
| TBL-17 | Column resize, reorder and visibility choices are operable by keyboard and persisted as decided | Column customization | Optional | Application's job |
| TBL-18 | Expandable rows expose their state and keep focus logical | Expandable rows | If applicable | Application's job |
| TBL-19 | Usable at 200% zoom, in right-to-left layout and dark mode, and printable where required | Always | Required | Application's job |

## 7. Anti-patterns

- Tables used for layout, or a grid of divs with no header association.
- Empty body with only headers when there is no data.
- Sort indicator drawn but not exposed.
- Selection that silently covers only the current page when "select all" is shown.
- Page 5 shown after filtering leaves 2 pages.
- Wide table clipped with no way to scroll it by keyboard.
- Truncated text with no way to read the full value.
- Row action buttons all named "Edit".

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| TBL-01 | Accessibility | Always | Structure | Inspect the accessibility tree, use a screen reader across cells | Name present, every data cell announced with its headers | Required | Manual | Critical |
| TBL-02 | States | Always | Empty state | Render with no rows | A message is shown, not just headers | Required | Automatable | Critical |
| TBL-03 | States | Async data | Loading | Load slowly, then refresh | Loading indicated, layout stable, busy state exposed | If applicable | Automatable | Important |
| TBL-04 | States | Async data | Error | Make loading fail, then retry, then partially fail | Error and retry shown, partial data handled | If applicable | Automatable | Critical |
| TBL-05 | Functional | Sorting | Sorting | Sort a column through its full cycle, sort data with equal and missing values | Order correct and stable, direction visible and exposed | If applicable | Automatable | Important |
| TBL-06 | Functional | Filtering | Filtering | Apply filters matching some, none, and clear them | Count correct, no results state shown, clear restores all | If applicable | Automatable | Important |
| TBL-07 | Functional | Row selection | Selection | Select rows, the page, all, change page, clear | Counts and mixed state correct, scope of "all" explicit | If applicable | Automatable | Critical |
| TBL-08 | Functional | Pagination | Pagination | Go to first and last page, change page size, shrink data on the last page | Boundaries respected, no out of range page, state in URL | If applicable | Automatable | Important |
| TBL-09 | Layout | Always | Long cell content | Use very long text and unbroken strings in cells | Layout intact, full value available | Required | Automatable | Important |
| TBL-10 | Layout | Sticky parts | Sticky parts | Scroll vertically and horizontally | Sticky parts stay aligned, nothing hidden | If applicable | Automatable | Nice-to-have |
| TBL-11 | Layout | Always | Small viewports | Use a narrow viewport and the keyboard | All columns reachable, headers still associated | Required | Manual | Important |
| TBL-12 | Data | Always | Formatting | Use large numbers, dates, negative values, nulls and different locales | Consistent formatting, placeholder for missing | Required | Automatable | Important |
| TBL-13 | Accessibility | Row actions | Row actions | Tab to row actions, inspect names | Reachable, each name includes row context | If applicable | Automatable | Important |
| TBL-14 | Data | Live data | Live updates | Update data while a row is selected and a sort is active | Selection and sort kept, updates announced where relevant | If applicable | Automatable | Important |
| TBL-15 | Data | Large data | Large data | Load a very large set, scroll and navigate with the keyboard | Responsive, focus and selection intact | If applicable | Manual | Nice-to-have |
| TBL-16 | Data | Always | Special characters | Use markup characters, emoji, right-to-left text | Displayed literally and safely | Required | Automatable | Important |
| TBL-17 | Functional | Column customization | Column customization | Resize, reorder and hide columns with the keyboard | Operable, persistence as decided | Optional | Manual | Nice-to-have |
| TBL-18 | Keyboard | Expandable rows | Expandable rows | Expand and collapse with the keyboard | State exposed, focus logical | If applicable | Automatable | Important |
| TBL-19 | Layout | Always | Zoom, direction, dark mode | Check at 200% zoom, right-to-left, dark mode | Readable, nothing clipped, contrast sufficient | Required | Manual | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
