---
component: Menu / dropdown menu
id-prefix: MNU
status: draft
---

# Menu / dropdown menu

> Shares dismissal, positioning and typeahead behavior with `dropdown.md` and `popover.md`. A menu holds actions. A list that holds a value to choose is a dropdown.

## 1. When to use it vs alternatives

- **Menu**: a list of actions or commands behind a trigger (for example "Edit, Duplicate, Delete").
- **Dropdown** (`DD`): choosing a value for a field.
- **Navigation list** (`NAV`): links to pages. Site navigation is not a menu in the application sense.
- **Context menu** (`CTX`): the same list opened on a secondary action.
- **Split button** (`SPB`): a default action plus alternatives.

## 2. Anatomy and variants

Parts: trigger, menu, items, optional groups and separators, optional submenus, optional shortcut hints, optional checkable items.

Variants that change which capabilities apply:

- Plain actions only vs checkable items (checkbox and radio items)
- With vs without submenus
- Static vs dynamic or asynchronous items
- Short vs long menu

Also covers the **context menu** variant through the **Applies when** column (`MNU-18` to `MNU-20`). A menu opened from a button is the base case.

## 3. States

Closed, open, item highlighted, item disabled, item checked, submenu open, loading, empty.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Enter, Space, ArrowDown on the trigger | Opens the menu, highlights the first item |
| ArrowUp on the trigger | Opens the menu, highlights the last item |
| ArrowDown / ArrowUp | Moves the highlight, wrapping |
| Home / End | First / last item |
| Printable character | Highlights the next item starting with it |
| Enter / Space | Runs the item and closes the menu (checkable items follow their own rule) |
| ArrowRight (mirrored in right-to-left) | Opens the submenu |
| ArrowLeft (mirrored) / Escape | Closes the submenu, or the menu, returning focus to the parent item or the trigger |
| Tab | Closes the menu and moves on |

## 5. Component-specific accessibility

- The menu and its items expose menu roles, checkable items expose their checked state.
- Disabled items are perceivable.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| MNU-01 | The menu opens by activation and by arrow keys on the trigger, highlighting the right item | Always | Required | Usually provided by primitives |
| MNU-02 | Arrow keys move through items, wrapping, with Home and End | Always | Required | Usually provided by primitives |
| MNU-03 | Typeahead highlights the matching item | Always | Required | Usually provided by primitives |
| MNU-04 | Activating an item runs its action once and closes the menu | Always | Required | Usually provided by primitives |
| MNU-05 | Escape closes the menu and returns focus to the trigger | Always | Required | Usually provided by primitives |
| MNU-06 | Tab closes the menu and moves focus on | Always | Required | Usually provided by primitives |
| MNU-07 | Disabled items cannot be activated and are handled consistently by keyboard navigation | Can be disabled | If applicable | Usually provided by primitives |
| MNU-08 | Submenus open and close by keyboard, with mirrored keys in right-to-left layout, and pointer movement toward a submenu does not close it | Submenus | If applicable | Usually provided by primitives |
| MNU-09 | Checkable items expose their state, and whether the menu stays open is defined | Checkable items | If applicable | Usually provided by primitives |
| MNU-10 | Menu semantics are used for actions only, not for navigation links | Always | Required | Application's job |
| MNU-11 | Destructive items are separated or confirmed | Destructive items | If applicable | Application's job |
| MNU-12 | Dynamic and asynchronous items show loading and empty states, and items that change while open are handled | Dynamic items | If applicable | Application's job |
| MNU-13 | A long menu scrolls and fits the viewport | Always | Required | Application's job |
| MNU-14 | The menu is fully visible: flips, is not clipped, is stacked above content | Always | Required | Application's job |
| MNU-15 | Shortcut hints match real shortcuts and do not conflict with others | Shortcut hints | Optional | Application's job |
| MNU-16 | Usable by touch, with targets large enough | Always | Required | Application's job |
| MNU-17 | Groups and separators have names where they group items | Groups | If applicable | Usually provided by primitives |
| MNU-18 | The menu opens by the secondary pointer action, the menu key, the keyboard equivalent and a long press on touch devices | Context menu | If applicable | Application's job |
| MNU-19 | The menu is positioned at the pointer or target and stays inside the viewport, and the native menu is not suppressed where users need it (text fields, links) | Context menu | If applicable | Application's job |
| MNU-20 | The actions apply to the target that was chosen, not to an earlier selection, and focus returns to that target on close | Context menu | If applicable | Application's job |

## 7. Anti-patterns

- Menu semantics on a site navigation list.
- Focus not returning to the trigger.
- The menu closing when the pointer travels diagonally to a submenu.
- Destructive item next to a common item with no separation.
- A long menu that overflows the viewport.
- An item that runs twice on a fast double activation.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| MNU-01 | Keyboard | Always | Opening | Open by activation, ArrowDown and ArrowUp on the trigger | Opens each way, first or last item highlighted | Required | Automatable | Critical |
| MNU-02 | Keyboard | Always | Navigation | Use arrows to wrap around, Home and End | Highlight moves and wraps as specified | Required | Automatable | Critical |
| MNU-03 | Keyboard | Always | Typeahead | Type the start of an item name | Matching item highlighted | Required | Automatable | Important |
| MNU-04 | Functional | Always | Activation | Activate an item, then activate quickly twice | Action runs once, menu closes | Required | Automatable | Critical |
| MNU-05 | Keyboard | Always | Escape | Open and press Escape | Closed, focus on the trigger | Required | Automatable | Critical |
| MNU-06 | Keyboard | Always | Tab | Open and press Tab | Closed, focus moves on | Required | Automatable | Important |
| MNU-07 | Keyboard | Can be disabled | Disabled items | Navigate past a disabled item, try to activate it | Handled as decided, not activatable | If applicable | Automatable | Important |
| MNU-08 | Keyboard | Submenus | Submenus | Open, move into and out of submenus by keyboard and pointer, in right-to-left layout | Opens and closes correctly, focus returns to the parent item, keys mirrored | If applicable | Automatable | Important |
| MNU-09 | Accessibility | Checkable items | Checkable items | Toggle items, inspect state | State exposed, menu open or closed as decided | If applicable | Automatable | Important |
| MNU-10 | Accessibility | Always | Menu for actions only | Review where menu semantics are used | No navigation links in a menu | Required | Manual | Important |
| MNU-11 | Functional | Destructive items | Destructive items | Locate and activate a destructive item | Separated or confirmed | If applicable | Automatable | Important |
| MNU-12 | Data | Dynamic items | Dynamic items | Open with items loading, empty, and changing while open | Loading and empty states shown, highlight stays valid | If applicable | Automatable | Important |
| MNU-13 | Layout | Always | Long menu | Use many items in a short viewport | Scrolls inside the viewport, highlighted item stays visible | Required | Automatable | Important |
| MNU-14 | Layout | Always | Positioning | Open near viewport edges and inside a clipping container | Fully visible | Required | Automatable | Critical |
| MNU-15 | Functional | Shortcut hints | Shortcut hints | Use each listed shortcut | Each does what the hint says | Optional | Manual | Nice-to-have |
| MNU-16 | Layout | Always | Touch | Use a touch device | Items easy to hit, no hover dependence | Required | Manual | Important |
| MNU-17 | Accessibility | Groups | Groups | Navigate across groups with a screen reader | Group names announced | If applicable | Manual | Nice-to-have |
| MNU-18 | Keyboard | Context menu | The menu opens by the secondary pointer action, the menu key, the keyboard equivalent and a long press on touch devices | Open by each means | Opens everywhere it should | If applicable | Automatable | Critical |
| MNU-19 | Layout | Context menu | The menu is positioned at the pointer or target and stays inside the viewport, and the native menu is not suppressed where users need it (text fields, links) | Open at each viewport edge and over a text field and a link | Fully visible, native menu kept where needed | If applicable | Automatable | Important |
| MNU-20 | Functional | Context menu | The actions apply to the target that was chosen, not to an earlier selection, and focus returns to that target on close | Open on different targets, run an action, close | Right target affected, focus returned | If applicable | Automatable | Critical |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
