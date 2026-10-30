---
name: ui-component-specs
description: Generic, framework-agnostic specs and test cases for common front-end UI components (dropdown, select, combobox, dialog, modal, drawer, tabs, navigation, form field, input, password, OTP, masked input, date picker, date range, table, data grid, toast, tooltip, menu, carousel, chart, image, video player, and more). Use when building, reviewing or testing a UI component to cover every state, keyboard interaction, accessibility requirement and edge case, such as empty list, very long text, async loading, focus return and validation.
---

# UI Component Specs

A catalog of what must be built and what must be tested for each common UI element. One reference file per component. Load only the reference you need.

## How to use

1. Identify the component being built, changed or reviewed.
2. Find it in the index below, which is alphabetical and includes variants (password, OTP, date range, split button and so on). If there is no entry, say so and fall back to the closest component.
3. Open the reference. If it starts with a "Builds on" note, also open the base reference it names. For a variant that lives inside another reference, use the rows whose **Applies when** names the variant, together with the base rows.
4. Decide which variant you are building (for example single or multiple selection). Each capability has an **Applies when** condition. Skip the ones that do not apply.
5. Build every **Required** capability. Build **If applicable** capabilities that match the variant. Treat **Optional** ones as enhancements.
6. Cover every ID that applies with a test, written in the project's own test stack. Do not skip **Critical** priority cases.
7. Finish with the reference's Definition of done checklist.

## Rules

- **Capabilities, not mechanisms.** References say what must exist and what is observable afterwards. They never say how a library or design system achieves it. Choose the mechanism in the style of the project's own stack.
- **Component libraries.** If the project uses a component library (Angular Material, shadcn, Radix, MUI and so on), use its primitives and treat the reference as a verification list. Implement only what the library does not cover. Do not re-implement keyboard, focus or ARIA behavior the library already provides, but do verify it with the test cases.
- **Ownership column.** Each capability states who usually owns it: "Usually provided by primitives" (keyboard, ARIA, focus trap) or "Application's job" (empty state, validation, data, layout). Verify the first, build the second.
- **Project conventions win.** Naming, test framework, selectors, design tokens and file layout come from the project, never from these references.
- **General accessibility.** References link to general accessibility rules for focus, contrast, target size, zoom and reduced motion. Until a dedicated accessibility skill is installed, apply WCAG 2.2 level AA for those.
- **Tests carry the ID.** Put the ID in the test name, so coverage can be searched and a failing test points to the capability that broke.
- **Report coverage.** When asked to "cover all IDs", list each applicable ID with its status: implemented and tested, implemented only, not applicable (with the reason), or missing.

## Example

Request: "Build a multi-select dropdown for the filters form. Cover all applicable IDs."

The agent opens `references/dropdown.md`, keeps the rows that apply to a multiple selection form field (for example `DD-01` to `DD-08`, `DD-11`, `DD-14`, `DD-17`, `DD-18`), builds the ones the project's library does not provide, writes tests named with their IDs, and ends with a report like this:

| ID | Status | Note |
|---|---|---|
| DD-07 | Implemented and tested | "No options" message shown |
| DD-11 | Implemented and tested | Missing preselected value is flagged, not hidden |
| DD-14 | Implemented only | Reset action built, test pending |
| DD-22 | Not applicable | Desktop only, per the brief |
| DD-26 | Missing | Options still identified by label |

## Reference index

Status values: `draft`, `stable`, `deprecated`.

| Component | ID prefix or IDs | Reference | Status |
|---|---|---|---|
| Accordion / collapsible | `ACC` | [accordion](references/accordion.md) | draft |
| Alert / banner | `ALR` | [alert](references/alert.md) | draft |
| Avatar | `AVT` | [avatar](references/avatar.md) | draft |
| Badge | `BDG` | [badge](references/badge.md) | draft |
| Breadcrumbs | `BRD` | [breadcrumbs](references/breadcrumbs.md) | draft |
| Button | `BTN` | [button](references/button.md) | draft |
| Calendar (always visible) | `DTP-26` | [date-picker](references/date-picker.md), variant rows | draft |
| Card | `CRD` | [card](references/card.md) | draft |
| Carousel | `CAR` | [carousel](references/carousel.md) | draft |
| Charts (accessibility level) | `CHT` | [charts](references/charts.md) | draft |
| Checkbox | `CHK` | [checkbox](references/checkbox.md) | draft |
| Chips / tags | `CMB-17, CMB-18` | [combobox](references/combobox.md), variant rows | draft |
| Color picker | `CLR` | [color-picker](references/color-picker.md) | draft |
| Combobox / autocomplete | `CMB` | [combobox](references/combobox.md) | draft |
| Command palette | `CMB-19, CMB-20` | [combobox](references/combobox.md), variant rows | draft |
| Context menu | `MNU-18 to MNU-20` | [menu](references/menu.md), variant rows | draft |
| Data grid (editing, virtualization) | `GRD` | [data-grid](references/data-grid.md) | draft |
| Date picker | `DTP` | [date-picker](references/date-picker.md) | draft |
| Date range | `DTP-21 to DTP-23` | [date-picker](references/date-picker.md), variant rows | draft |
| Dialog / modal | `DLG` | [dialog](references/dialog.md) | draft |
| Drawer / sheet | `DRW` | [drawer](references/drawer.md) | draft |
| Dropdown / select (single and multiple) | `DD` | [dropdown](references/dropdown.md) | draft |
| Email, phone, URL input | `TXT-22` | [text-input](references/text-input.md), variant rows | draft |
| Empty state and error state | `EMP` | [empty-state](references/empty-state.md) | draft |
| File upload | `UPL` | [file-upload](references/file-upload.md) | draft |
| Footer | `FTR` | [footer](references/footer.md) | draft |
| Form (complete) | `FRM` | [form](references/form.md) | draft |
| Gallery / lightbox | `GAL` | [gallery-lightbox](references/gallery-lightbox.md) | draft |
| Icon-only button | `BTN-16` | [button](references/button.md), variant rows | draft |
| Iframe / embeds | `IFR` | [iframe-embed](references/iframe-embed.md) | draft |
| Image (alt, lazy loading, errors) | `IMG` | [image](references/image.md) | draft |
| Inline validation and error messages | `VAL` | [inline-validation](references/inline-validation.md) | draft |
| Link | `LNK` | [link](references/link.md) | draft |
| Listbox | `DD-27, DD-28` | [dropdown](references/dropdown.md), variant rows | draft |
| Masked input (card, IBAN, phone) | `TXT-23, TXT-24` | [text-input](references/text-input.md), variant rows | draft |
| Menu / dropdown menu | `MNU` | [menu](references/menu.md) | draft |
| Navbar / header navigation | `NAV` | [navbar](references/navbar.md) | draft |
| Number input / stepper | `NUM` | [number-input](references/number-input.md) | draft |
| One-time code (OTP) | `TXT-25, TXT-26` | [text-input](references/text-input.md), variant rows | draft |
| Pagination | `PAG` | [pagination](references/pagination.md) | draft |
| Password input | `TXT-20, TXT-21` | [text-input](references/text-input.md), variant rows | draft |
| Popover | `POP` | [popover](references/popover.md) | draft |
| Progress, spinner, skeleton | `PRG` | [progress-indicators](references/progress-indicators.md) | draft |
| Radio group | `RAD` | [radio-group](references/radio-group.md) | draft |
| Rating | `RTG` | [rating](references/rating.md) | draft |
| Search input | `SRC` | [search-input](references/search-input.md) | draft |
| Segmented control | `RAD-17, RAD-18` | [radio-group](references/radio-group.md), variant rows | draft |
| Sidebar | `SID` | [sidebar](references/sidebar.md) | draft |
| Skip link | `LNK-15, LNK-16` | [link](references/link.md), variant rows | draft |
| Slider / range | `SLD` | [slider](references/slider.md) | draft |
| Split button | `BTN-17, BTN-18` | [button](references/button.md), variant rows | draft |
| Stepper / wizard | `STP` | [stepper](references/stepper.md) | draft |
| Switch / toggle | `SWT` | [switch](references/switch.md) | draft |
| Table | `TBL` | [table](references/table.md) | draft |
| Tabs | `TAB` | [tabs](references/tabs.md) | draft |
| Text input | `TXT` | [text-input](references/text-input.md) | draft |
| Textarea | `TXA` | [textarea](references/textarea.md) | draft |
| Time picker | `DTP-24, DTP-25` | [date-picker](references/date-picker.md), variant rows | draft |
| Timeline | `TML` | [timeline](references/timeline.md) | draft |
| Toast / snackbar | `TST` | [toast](references/toast.md) | draft |
| Tooltip | `TIP` | [tooltip](references/tooltip.md) | draft |
| Transfer list | `DD-31` | [dropdown](references/dropdown.md), variant rows | draft |
| Tree select | `DD-29, DD-30` | [dropdown](references/dropdown.md), variant rows | draft |
| Tree view | `TRV` | [tree-view](references/tree-view.md) | draft |
| Video / audio player | `MED` | [media-player](references/media-player.md) | draft |
| Virtualized list | `VLS` | [virtualized-list](references/virtualized-list.md) | draft |
