---
component: Navbar / header navigation
id-prefix: NAV
status: draft
---

# Navbar / header navigation

## 1. When to use it vs alternatives

- **Navbar**: the main way to move between the top-level sections of a site or app.
- **Sidebar** (`SID`): many sections or deep hierarchies in an application.
- **Breadcrumbs** (`BRD`): showing and moving up a hierarchy.
- **Tabs** (`TAB`): switching views within one page.
- **Menu** (`MNU`): actions, not navigation.

## 2. Anatomy and variants

Parts: home link or logo, list of links, optional dropdown sections, optional search and account controls, optional collapse control on small viewports, optional skip link.

Variants that change which capabilities apply:

- Flat vs links with dropdown sections
- Collapsing into a toggle on small viewports vs always visible
- Sticky vs scrolling with the page
- Several navigation regions on the same page
- Content that changes with authentication

## 3. States

Default, hover, focus, current page, expanded and collapsed (small viewport), section open, sticky and hidden on scroll.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Tab / Shift+Tab | Moves through links in visual order |
| Enter | Follows a link |
| Enter / Space on a section or collapse control | Opens or closes it |
| Escape | Closes an open section or the collapsed navigation, returning focus to its control |

## 5. Component-specific accessibility

- The navigation is a named region, and links are in a list.
- The current page is exposed, not only visually marked.
- Dropdown sections use a disclosure pattern, not application menu semantics.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| NAV-01 | The navigation is a named region and its links are in a list | Always | Required | Application's job |
| NAV-02 | The current page is indicated visually and programmatically | Always | Required | Application's job |
| NAV-03 | Every link is reachable in a logical order with visible focus and no focus trap | Always | Required | Application's job |
| NAV-04 | A skip link is the first focusable element and moves focus to the main content | Always | Required | Application's job |
| NAV-05 | On small viewports, a control with expanded state opens and closes the navigation, which closes on link selection and Escape, with focus handled | Collapsing | If applicable | Application's job |
| NAV-06 | Sections with links open by activation (and optionally hover), close with Escape and on leaving, and stay keyboard operable | Dropdown sections | If applicable | Application's job |
| NAV-07 | A sticky navigation never covers the focused element or anchor targets, and a hide-on-scroll behavior never hides focus | Sticky | If applicable | Application's job |
| NAV-08 | Long, numerous and localized labels do not break the layout, and overflow is handled | Always | Required | Application's job |
| NAV-09 | Resizing across breakpoints preserves the state and does not leave two versions active | Collapsing | Required | Application's job |
| NAV-10 | The current page indicator is right on nested routes, query strings and hashes | Always | Required | Application's job |
| NAV-11 | Several navigation regions on a page have different names | Several regions | If applicable | Application's job |
| NAV-12 | The home link or logo has an accessible name | Always | Required | Application's job |
| NAV-13 | Usable at 200% zoom and 400% reflow, in right-to-left layout and in dark mode | Always | Required | Application's job |
| NAV-14 | External links and links that open a new window are identified | External links | If applicable | Application's job |
| NAV-15 | Items that depend on authentication update when the state changes | Authentication | If applicable | Application's job |

## 7. Anti-patterns

- Application menu roles on website navigation.
- Dropdown sections that open only on hover.
- A sticky header covering the element that has focus.
- Collapsed navigation that stays in the tab order while hidden.
- No indicator for the current page.
- A hamburger control with no name or expanded state.
- Hover menus that close when the pointer moves diagonally.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| NAV-01 | Accessibility | Always | Region and list | Inspect the accessibility tree | Named navigation region, links in a list | Required | Automatable | Critical |
| NAV-02 | Accessibility | Always | Current page | Visit each section | Current link exposed and visibly marked | Required | Automatable | Critical |
| NAV-03 | Keyboard | Always | Keyboard order | Tab through the navigation | Logical order, focus visible, no trap | Required | Automatable | Critical |
| NAV-04 | Keyboard | Always | Skip link | Press Tab at page load, activate the skip link | It is first and focus lands in the main content | Required | Automatable | Critical |
| NAV-05 | Keyboard | Collapsing | Collapsed navigation | Open, select a link, reopen and press Escape on a small viewport | Expanded state follows, closes as specified, hidden links are not focusable | If applicable | Automatable | Critical |
| NAV-06 | Keyboard | Dropdown sections | Sections | Open sections by keyboard and pointer, close with Escape | Operable without hover, focus returns to the section control | If applicable | Automatable | Important |
| NAV-07 | Layout | Sticky | Sticky behavior | Tab through the page and follow in-page links with the header sticky | Focused element and targets never covered | If applicable | Automatable | Important |
| NAV-08 | Layout | Always | Labels and overflow | Use very long labels, many items, a longer language | No breakage, all items reachable | Required | Automatable | Important |
| NAV-09 | Layout | Collapsing | Breakpoints | Resize through the breakpoint with the navigation open | State preserved, one version active | Required | Automatable | Important |
| NAV-10 | Functional | Always | Nested routes | Visit nested pages, add a query string and a hash | Right item marked as current | Required | Automatable | Important |
| NAV-11 | Accessibility | Several regions | Region names | Inspect all regions | Distinct names | If applicable | Automatable | Important |
| NAV-12 | Accessibility | Always | Home link name | Inspect the name of the logo link | Meaningful name | Required | Automatable | Important |
| NAV-13 | Layout | Always | Zoom, direction and dark mode | Zoom to 200% and 400%, right-to-left, dark mode | Nothing clipped, usable | Required | Manual | Important |
| NAV-14 | Accessibility | External links | External links | Review links that leave the site or open a window | Identified to the user | If applicable | Manual | Nice-to-have |
| NAV-15 | Functional | Authentication | Authentication changes | Sign in and out | Items update without a stale state | If applicable | Automatable | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
