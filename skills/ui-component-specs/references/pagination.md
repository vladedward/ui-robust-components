---
component: Pagination
id-prefix: PAG
status: draft
---

# Pagination

> Used with `table.md` and lists. Table-specific behavior such as selection across pages is in `table.md` (TBL-07, TBL-08).

## 1. When to use it vs alternatives

- **Pagination**: a large set where users need to know the size, jump to a position, return to a position or share a link to it.
- **Load more** or **infinite scroll** (`INF`): browsing a feed where position does not matter.
- **Filtering and search** (`SRC`): often reduces the need for deep paging.

## 2. Anatomy and variants

Parts: navigation region, previous and next controls, page links or buttons, current page, optional first and last, optional ellipsis, optional page size control, optional range and total text.

Variants that change which capabilities apply:

- Numbered pages vs previous and next only (cursor based, no known total)
- Few vs very many pages
- With vs without page size choice
- Client-side vs server-side data
- With state in the URL vs local state

## 3. States

Default, current page, first page (previous unavailable), last page (next unavailable), loading, empty, error, disabled control.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Tab / Shift+Tab | Moves through the controls |
| Enter / Space | Goes to the page |

## 5. Component-specific accessibility

- A named navigation region.
- The current page is exposed as current.
- Controls have descriptive names, not only numbers or arrows.
- A change of page is perceivable to assistive technology.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| PAG-01 | A named region, the current page exposed, controls with real link or button semantics | Always | Required | Application's job |
| PAG-02 | Previous and next are unavailable at the boundaries without disappearing or shifting the layout | Always | Required | Application's job |
| PAG-03 | With many pages, a window of pages is shown, with the first and last always reachable and a way to jump far | Very many pages | If applicable | Application's job |
| PAG-04 | Changing the page size keeps the user's position as decided and updates the range | Page size choice | If applicable | Application's job |
| PAG-05 | A current page that no longer exists after the data shrinks or a filter changes is corrected | Always | Required | Application's job |
| PAG-06 | The page, and the page size, are in the URL, and reload, back and shared links restore them | State in the URL | If applicable | Application's job |
| PAG-07 | After a page change, focus and scroll go to a logical place, and the new page is announced | Always | Required | Application's job |
| PAG-08 | A loading state during a page change prevents repeated requests and avoids layout jumps | Server-side data | If applicable | Application's job |
| PAG-09 | The range and total are shown, and zero results are handled | Total known | Required | Application's job |
| PAG-10 | Controls have descriptive names such as "page 3" and "next page" | Always | Required | Application's job |
| PAG-11 | A compact form is used on small viewports | Always | Required | Application's job |
| PAG-12 | A cursor based variant offers only previous and next, with no invented total | No known total | If applicable | Application's job |
| PAG-13 | Targets are large enough and focus is visible | Always | Required | Application's job |

## 7. Anti-patterns

- Controls that are only numbers or arrows, with no names.
- Page 7 left selected after a filter leaves 3 pages.
- Focus left on the control while the content above changes.
- Hundreds of page links in a row.
- The previous control disappearing on page one and moving the layout.
- Paging state kept only in memory, so back and refresh lose it.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| PAG-01 | Accessibility | Always | Semantics | Inspect the accessibility tree | Named region, current page exposed | Required | Automatable | Critical |
| PAG-02 | States | Always | Boundaries | Go to the first and the last page | Previous or next unavailable, layout stable | Required | Automatable | Important |
| PAG-03 | Functional | Very many pages | Page windowing | Use a very large page count and jump | First and last reachable, no excess controls | If applicable | Automatable | Important |
| PAG-04 | Functional | Page size choice | Page size | Change the size on a later page | Position handled as decided, range correct | If applicable | Automatable | Important |
| PAG-05 | Data | Always | Out of range page | Go to the last page, then filter or delete so it no longer exists | Corrected to a valid page | Required | Automatable | Critical |
| PAG-06 | Functional | State in the URL | URL state | Change the page, reload, go back, open a shared link | Same page each time | If applicable | Automatable | Critical |
| PAG-07 | Keyboard | Always | Focus and announcement | Change page by keyboard with a screen reader | Focus and scroll in a logical place, change announced | Required | Manual | Critical |
| PAG-08 | States | Server-side data | Loading | Change page with a slow response, click repeatedly | One request, loading shown, no jump | If applicable | Automatable | Important |
| PAG-09 | Data | Total known | Range and total | Check the text on several pages and with zero results | Correct range and total, empty state handled | Required | Automatable | Important |
| PAG-10 | Accessibility | Always | Control names | Inspect each control name | Descriptive | Required | Automatable | Important |
| PAG-11 | Layout | Always | Small viewports | Use a narrow viewport | Compact, no overflow | Required | Automatable | Important |
| PAG-12 | Functional | No known total | Cursor based | Move through pages with previous and next | Works with no total shown | If applicable | Automatable | Important |
| PAG-13 | Accessibility | Always | Targets and focus | Tab through, use a touch device | Focus visible, targets usable | Required | Manual | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
