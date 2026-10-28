---
component: Tabs
id-prefix: TAB
status: draft
---

# Tabs

## 1. When to use it vs alternatives

- **Tabs**: switching between peer views of the same content area, where one view is shown at a time.
- **Navigation links**: moving between pages or routes. If it navigates, it is navigation, even if styled as tabs.
- **Accordion** (`ACC`): sections that can be open together or read in sequence.
- **Segmented control** (`SEG`): switching a display mode of the same data.
- **Stepper** (`STP`): ordered steps.

## 2. Anatomy and variants

Parts: tab list, tabs, panels, optional overflow handling, optional add and close actions on tabs.

Variants that change which capabilities apply:

- Automatic vs manual activation
- Horizontal vs vertical
- Few vs many tabs (overflow)
- Static vs dynamic (tabs added and removed)
- With deep linking vs local state only
- Eager vs lazily loaded panels

## 3. States

Selected, unselected, hover, focus, disabled, panel loading, panel error, overflowing.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Tab | Moves focus to the selected tab, then into the panel |
| ArrowRight / ArrowLeft (ArrowDown / ArrowUp when vertical) | Moves focus to the next or previous tab, wrapping |
| Home / End | Moves focus to the first or last tab |
| Enter / Space | Activates the focused tab when activation is manual |

With automatic activation moving focus also shows the panel. In right-to-left layout the horizontal arrows are mirrored.

## 5. Component-specific accessibility

- The tab list, tabs and panels expose their roles, each tab is linked to its panel and each panel is named by its tab.
- Only the selected tab is a tab stop.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| TAB-01 | Selecting a tab shows its panel and hides the others; exactly one is selected | Always | Required | Usually provided by primitives |
| TAB-02 | Arrow keys, Home and End move between tabs; the list is a single tab stop; Tab moves into the panel | Always | Required | Usually provided by primitives |
| TAB-03 | Activation behavior is consistent, and manual when showing a panel is expensive | Always | Required | Application's job |
| TAB-04 | Roles and relationships between tab list, tabs and panels are exposed | Always | Required | Usually provided by primitives |
| TAB-05 | A defined tab is selected on first render | Always | Required | Application's job |
| TAB-06 | Disabled tabs cannot be activated and are handled consistently by keyboard navigation | Can be disabled | If applicable | Usually provided by primitives |
| TAB-07 | Many tabs or narrow space: all tabs stay reachable and the selected tab stays visible | Overflow | If applicable | Application's job |
| TAB-08 | The selected tab is reflected in the URL and restored on reload and the back action | Deep linking | If applicable | Application's job |
| TAB-09 | Adding or removing tabs: removing the selected one selects a neighbor, and focus is placed deliberately | Dynamic tabs | If applicable | Application's job |
| TAB-10 | Panel state (entered data, scroll position) is preserved when switching away and back, or the decision is explicit | Panels hold state | Required | Application's job |
| TAB-11 | A lazily loaded panel shows a loading state and an error with retry | Lazy panels | If applicable | Application's job |
| TAB-12 | Long and localized labels do not break the layout | Always | Required | Application's job |
| TAB-13 | Content that navigates uses links, not tabs | Always | Required | Application's job |
| TAB-14 | Vertical orientation and right-to-left layout use the correct arrow keys | Vertical or right-to-left | If applicable | Usually provided by primitives |
| TAB-15 | A panel with no focusable content is still reachable from the keyboard | Always | Required | Usually provided by primitives |
| TAB-16 | The selected tab is distinguishable without color alone, with sufficient contrast | Always | Required | Application's job |
| TAB-17 | Counts or status on a tab are part of its accessible name and update | Counts or badges | Optional | Application's job |

## 7. Anti-patterns

- Tabs that navigate to different pages without link semantics.
- Every tab is its own tab stop.
- Automatic activation on a tab whose panel takes seconds to load.
- Unmounting panels and losing the user's entered data.
- Overflowing tabs that are cut off with no way to reach them.
- A selected tab that is later removed with no tab selected.
- Selected state shown only by color.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| TAB-01 | Functional | Always | Selection | Select each tab in turn | Only the selected panel visible, one tab selected | Required | Automatable | Critical |
| TAB-02 | Keyboard | Always | Keyboard model | Tab into the list, use arrows, Home, End, then Tab | Single tab stop, focus moves as specified, Tab enters the panel | Required | Automatable | Critical |
| TAB-03 | Keyboard | Always | Activation | Move focus across tabs | Panel shows on focus (automatic) or only after Enter or Space (manual), consistently | Required | Automatable | Important |
| TAB-04 | Accessibility | Always | Exposed semantics | Inspect the accessibility tree, use a screen reader | Roles, relationships and selected state exposed | Required | Manual | Critical |
| TAB-05 | States | Always | Initial tab | Render with and without a requested tab | A defined tab is selected | Required | Automatable | Important |
| TAB-06 | Keyboard | Can be disabled | Disabled tab | Navigate past a disabled tab, try to activate it | Handled consistently, not activatable | If applicable | Automatable | Important |
| TAB-07 | Layout | Overflow | Overflow | Add many tabs, use a narrow viewport, select the last tab | Every tab reachable, selected tab visible | If applicable | Automatable | Important |
| TAB-08 | Functional | Deep linking | Deep linking | Select a tab, reload, use the back action, open a direct link | The right tab is selected each time | If applicable | Automatable | Important |
| TAB-09 | Functional | Dynamic tabs | Add and remove | Remove the selected tab, remove the last tab, add a tab | A neighbor is selected, focus is deliberate, no state with nothing selected | If applicable | Automatable | Important |
| TAB-10 | Data | Panels hold state | Preserved state | Enter data in a panel, switch away and back | Data and scroll position kept as decided | Required | Automatable | Critical |
| TAB-11 | Data | Lazy panels | Lazy panels | Open a lazy panel slowly, then make it fail | Loading shown, error with retry, tabs still operable | If applicable | Automatable | Important |
| TAB-12 | Layout | Always | Long labels | Use very long labels | Layout intact, labels readable | Required | Automatable | Nice-to-have |
| TAB-13 | Accessibility | Always | Tabs vs links | Review each tab set that changes the page | Navigation uses links | Required | Manual | Important |
| TAB-14 | Keyboard | Vertical or right-to-left | Orientation and direction | Use the arrows in vertical and in right-to-left layouts | Keys match the orientation and direction | If applicable | Automatable | Important |
| TAB-15 | Keyboard | Always | Panel reachability | Use a panel with no focusable content, press Tab from the tab | The panel can be reached, or the next element is correct by design | Required | Manual | Important |
| TAB-16 | Accessibility | Always | Selected indicator | View in grayscale, check contrast | Selected tab clear without color | Required | Manual | Important |
| TAB-17 | Accessibility | Counts or badges | Counts | Change the count, use a screen reader | Name includes the count and updates | Optional | Manual | Nice-to-have |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
