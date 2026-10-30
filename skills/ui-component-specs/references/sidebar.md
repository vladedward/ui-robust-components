---
component: Sidebar
id-prefix: SID
status: draft
---

# Sidebar

> Shares link and current-page rules with `navbar.md`, and overlay behavior on small viewports with `dialog.md`.

## 1. When to use it vs alternatives

- **Sidebar**: persistent navigation for an application with many sections or a hierarchy.
- **Navbar** (`NAV`): a few top-level sections.
- **Tabs** (`TAB`): views within one page.
- **Drawer** (`DRW`): temporary content opened on demand, not persistent navigation.

## 2. Anatomy and variants

Parts: navigation region, list of items, optional groups with headings, optional nested items, optional collapse control, optional header and footer areas.

Variants that change which capabilities apply:

- Always expanded vs collapsible (including an icon-only collapsed mode)
- Flat vs nested items
- Persistent beside the content vs an overlay on small viewports
- Static vs dynamic items (permissions, counts)

## 3. States

Expanded, collapsed, item current, item hover and focus, group expanded and collapsed, overlay open and closed (small viewports), loading.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Tab / Shift+Tab | Moves through items in visual order |
| Enter | Follows a link |
| Enter / Space on a group or the collapse control | Expands or collapses it |
| Escape | Closes the sidebar when it is an overlay, returning focus to its control |

## 5. Component-specific accessibility

- The sidebar is a named navigation region and the current item is exposed.
- Expandable groups and the collapse control expose their expanded state.
- In collapsed mode every item keeps an accessible name.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| SID-01 | A named navigation region, with the current item exposed and marked | Always | Required | Application's job |
| SID-02 | The collapse control exposes its state and works by keyboard | Collapsible | If applicable | Application's job |
| SID-03 | In collapsed mode items keep their names and their labels are available | Icon-only collapsed mode | If applicable | Application's job |
| SID-04 | Nested items expand and collapse with exposed state, and ancestors of the current item are expanded on load | Nested items | If applicable | Application's job |
| SID-05 | The collapsed and expanded state, and which groups are open, persist across navigation and reload as decided | Collapsible or nested | If applicable | Application's job |
| SID-06 | On small viewports it becomes an overlay with a control to open it, dismissal, focus handling and an inert page behind | Overlay on small viewports | If applicable | Application's job |
| SID-07 | A long sidebar scrolls independently and keeps the current item in view | Always | Required | Application's job |
| SID-08 | Keyboard order is logical, focus is visible, and there is no focus trap outside the overlay mode | Always | Required | Application's job |
| SID-09 | Long and numerous labels are handled, with the full text available | Always | Required | Application's job |
| SID-10 | Crossing breakpoints keeps one version active and preserves state | Overlay on small viewports | Required | Application's job |
| SID-11 | Toggling the sidebar re-lays out the content without overlap or hidden content | Collapsible | Required | Application's job |
| SID-12 | Items, counts and permissions that change are reflected without a stale state | Dynamic items | If applicable | Application's job |
| SID-13 | Usable at 200% zoom, in right-to-left layout and in dark mode | Always | Required | Application's job |

## 7. Anti-patterns

- Collapsed mode with icons that have no name.
- The collapsed sidebar still reachable by Tab but invisible.
- State lost on every page load.
- A mobile overlay with the page still scrollable and focusable behind it.
- Content hidden behind a fixed sidebar.
- The current item not visible in a long scrolled list.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| SID-01 | Accessibility | Always | Region and current item | Inspect the accessibility tree on several pages | Named region, current item exposed | Required | Automatable | Critical |
| SID-02 | Keyboard | Collapsible | Collapse control | Collapse and expand by keyboard | State exposed, operable | If applicable | Automatable | Critical |
| SID-03 | Accessibility | Icon-only collapsed mode | Collapsed names | Inspect each item in collapsed mode | Each has a name and a visible label on focus or hover | If applicable | Automatable | Critical |
| SID-04 | Functional | Nested items | Nested items | Load a deep page, expand and collapse groups | Ancestors open on load, state exposed | If applicable | Automatable | Important |
| SID-05 | Data | Collapsible or nested | Persistence | Change the state, navigate, reload | State persists as decided | If applicable | Automatable | Important |
| SID-06 | Keyboard | Overlay on small viewports | Overlay | Open on a small viewport, press Tab, press Escape | Page inert behind, focus contained, closes and returns focus | If applicable | Automatable | Critical |
| SID-07 | Layout | Always | Scrolling | Use many items and a deep current page | Sidebar scrolls alone, current item visible | Required | Automatable | Important |
| SID-08 | Keyboard | Always | Keyboard order | Tab through | Logical order, focus visible | Required | Automatable | Important |
| SID-09 | Layout | Always | Long labels | Use very long labels and many items | No breakage, full text available | Required | Automatable | Important |
| SID-10 | Layout | Overlay on small viewports | Breakpoints | Resize through the breakpoint with groups open | One version active, state kept | Required | Automatable | Important |
| SID-11 | Layout | Collapsible | Content layout | Toggle the sidebar | Content re-flows without overlap | Required | Automatable | Important |
| SID-12 | Data | Dynamic items | Dynamic items | Change permissions and counts while visible | Items and counts update | If applicable | Automatable | Important |
| SID-13 | Layout | Always | Zoom, direction and dark mode | Zoom to 200%, right-to-left, dark mode | Nothing clipped, mirrored | Required | Manual | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
