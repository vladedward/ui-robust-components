# Component catalog and priorities

Each element gets one `skills/ui-component-specs/references/<element>.md`. ID prefixes keep edge cases and test cases traceable (for example `DD-07`).

Priorities:

- **P1**: used in almost every project, together covering every major behavior family (focus trap, keyboard on lists, async states, validation, overlays).
- **P2**: very common, many edge cases, or often built wrongly.
- **P3**: less frequent, narrower, or largely built on behaviors covered by P1 and P2.

## P1

| # | Element | ID prefix | Main areas that generate edge cases |
|---|---|---|---|
| 1 | Button | `BTN` | All states, loading, double submit, disabled vs aria-disabled, destructive actions, icon-only, long labels |
| 2 | Text input | `TXT` | Label, helper and error text, required, validation timing, autofill, paste, max length, IME and special characters, read-only |
| 3 | Dropdown / select (single and multiple) | `DD` | Open/close, typeahead, empty list, long lists and long text, clear/reset, option groups, preselected value missing, positioning and clipping |
| 4 | Checkbox | `CHK` | Indeterminate state, groups, select all, label click target, validation |
| 5 | Radio group | `RAD` | Arrow-key behavior, default selection, required, disabled options, group labeling |
| 6 | Dialog / modal | `DLG` | Focus trap and return, Escape, scroll lock, backdrop click, nested dialogs, long content, destructive confirmation, mobile |
| 7 | Tabs | `TAB` | Keyboard model, activation behavior, overflow, deep linking, dynamic add/remove, disabled tabs |
| 8 | Tooltip | `TIP` | Hover vs focus, dismissal, delay, touch devices, positioning, keyboard access, no essential info only in tooltip |
| 9 | Toast / snackbar | `TST` | Duration, hover and focus pause, stacking, announcements, actions inside toast, dismissal, persistence across navigation |
| 10 | Date picker | `DTP` | Typed vs picked input, formats and locales, min/max, disabled dates, keyboard grid, time zones, invalid dates |
| 11 | Table | `TBL` | Sorting, filtering, row selection, pagination, empty and loading states, sticky headers, responsive behavior, long cell content |

## P2

| Element | ID prefix | Notes |
|---|---|---|
| Combobox / autocomplete | `CMB` | Async results, debounce, no results, free text vs list only, highlight and active option |
| Textarea | `TXA` | Auto-resize, character counter, max length, paste of long text |
| Switch / toggle | `SWT` | Immediate vs submit-based effect, labeling, state announcement |
| Popover | `POP` | Dismissal, focus management, positioning, interactive content |
| Menu / dropdown menu | `MNU` | Keyboard model, submenus, disabled items, typeahead, dismissal |
| Navbar / header | `NAV` | Mobile collapse, active state, keyboard, skip link, sticky behavior |
| Sidebar | `SID` | Collapse and expand, nested items, persistence, mobile behavior |
| Breadcrumbs | `BRD` | Truncation, current page, long labels |
| Pagination | `PAG` | Boundaries, large page counts, page size, state in URL |
| Stepper / wizard | `STP` | Back and forward, validation per step, saved progress, error recovery |
| File upload | `UPL` | Drag and drop, size and type limits, multiple files, progress, cancel, retry, errors |
| Accordion / collapsible | `ACC` | Single vs multiple open, keyboard, deep linking, animation and reduced motion |
| Alert / banner | `ALR` | Severity levels, dismissal, announcements, persistence |
| Inline validation and error messages | `VAL` | Timing, association with field, summary of errors, server errors |
| Progress, spinner, skeleton | `PRG` | Determinate vs indeterminate, announcements, timeouts, layout shift |
| Empty state and error state | `EMP` | Actionable next step, partial failure, retry |
| Search input | `SRC` | Clear, submit behavior, debounce, recent searches, no results |
| Number input / stepper | `NUM` | Min/max/step, decimals and locales, scroll wheel, paste, empty vs zero |
| Link | `LNK` | External links, current page, descriptive text, new tab behavior |
| Drawer / sheet | `DRW` | Same family as dialog, plus swipe and positioning |
| Slider / range | `SLD` | Keyboard steps, dual handles, value display, touch |
| Form (complete) | `FRM` | Validation, submit, double submit, server errors, unsaved changes, autosave |

## P3

Two kinds. Seventeen elements are variants of an earlier reference and have no file of their own: password, email / phone / URL, masked input and OTP (in `text-input.md`), date range, time picker and calendar (in `date-picker.md`), listbox, tree select and transfer list (in `dropdown.md`), chips and command palette (in `combobox.md`), icon button and split button (in `button.md`), context menu (in `menu.md`), segmented control (in `radio-group.md`) and skip link (in `link.md`). The mapping with IDs is in `SKILL.md`. The other sixteen have their own reference, so their ID prefixes below are used as written; the prefixes of the seventeen are not used.

| Element | ID prefix |
|---|---|
| Password input (show/hide, strength, paste) | `PWD` |
| Email / phone / URL inputs | `EML` |
| Masked input (card, IBAN, phone) | `MSK` |
| OTP / PIN code input | `OTP` |
| Rating | `RTG` |
| Color picker | `CLR` |
| Listbox | `LST` |
| Segmented control | `SEG` |
| Chips / tags (selectable, removable) | `CHP` |
| Transfer list | `TRF` |
| Tree select | `TRS` |
| Date range | `DTR` |
| Time picker | `TMP` |
| Calendar | `CAL` |
| Context menu | `CTX` |
| Command palette | `CMD` |
| Icon button | `ICB` |
| Split button | `SPB` |
| Skip link | `SKP` |
| Footer | `FTR` |
| Data grid (editing, virtualization) | `GRD` |
| Virtualized list | `VLS` |
| Card | `CRD` |
| Tree view | `TRV` |
| Badge | `BDG` |
| Avatar | `AVT` |
| Timeline | `TML` |
| Charts (accessibility level) | `CHT` |
| Image (alt, lazy loading, errors) | `IMG` |
| Carousel | `CAR` |
| Gallery / lightbox | `GAL` |
| Video / audio player | `MED` |
| Iframe / embeds | `IFR` |

## Page-level patterns (after the components)

| Pattern | ID prefix | Priority |
|---|---|---|
| Authentication (sign in, sign up, reset) | `AUT` | P2 |
| Search with filters | `FLT` | P2 |
| Settings page | `SET` | P3 |
| Onboarding | `ONB` | P3 |
| Checkout | `CKO` | P3 |
| Infinite scroll / load more | `INF` | P3 |

## Shared behavior families (candidate traits)

If duplication becomes a problem, define these once and reference them by ID from the element files.

| Family | Used by |
|---|---|
| Dismissible (Escape, outside click, focus return) | Dialog, drawer, popover, menu, dropdown, tooltip, toast |
| Focus trap and focus return | Dialog, drawer, some popovers |
| Roving focus / arrow-key navigation | Tabs, radio group, menu, listbox, toolbar |
| Typeahead | Dropdown, combobox, menu, listbox, tree |
| Anchored positioning (flip, clipping, z-index) | Dropdown, popover, tooltip, menu, date picker |
| Async states (loading, empty, error, retry) | Dropdown, combobox, table, list, upload, search |
| Validation and error association | All form fields, form |
| Selection model (single, multiple, clear all) | Dropdown, listbox, table rows, tree, chips, transfer list |

## Writing order

1. Button, text input, dropdown (establishes the template and the test case format)
2. Checkbox, radio group, dialog, tabs
3. Tooltip, toast, date picker, table (completes P1)
4. Combobox, menu, popover, form validation, file upload
5. Remaining P2, then P3 as real bugs and needs appear
6. Page-level patterns last

## Other skills

After the component references: `accessibility` (cross-cutting rules, linked from components instead of repeated), then `seo` (page-level concerns only).
