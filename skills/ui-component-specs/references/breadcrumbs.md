---
component: Breadcrumbs
id-prefix: BRD
status: draft
---

# Breadcrumbs

## 1. When to use it vs alternatives

- **Breadcrumbs**: showing where the page sits in a hierarchy and moving up it. Useful for deep sites (catalogs, documentation).
- **Navbar and sidebar** (`NAV`, `SID`): primary navigation.
- **Back link**: a single step back to the previous page.
- Not useful on flat sites with one or two levels.

## 2. Anatomy and variants

Parts: navigation region, ordered list of links, separators, current page item, optional collapsed middle.

Variants that change which capabilities apply:

- Full trail vs collapsed middle for long trails
- Location-based (hierarchy) vs history-based (not recommended)
- Titles known at render vs loaded asynchronously

## 3. States

Default, hover, focus, current page, collapsed, loading title.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Tab / Shift+Tab | Moves through the links in order |
| Enter | Follows a link |
| Enter / Space on the collapsed control | Reveals the hidden items |

## 5. Component-specific accessibility

- A named navigation region with an ordered list.
- The current page is exposed as current.
- Separators are decorative and not announced.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| BRD-01 | A named navigation region with an ordered list of links | Always | Required | Application's job |
| BRD-02 | The current page is marked and exposed | Always | Required | Application's job |
| BRD-03 | Separators are not announced and not selectable | Always | Required | Application's job |
| BRD-04 | A long trail collapses the middle, keeping the first and last items, and the hidden items are reachable by keyboard | Long trails | If applicable | Application's job |
| BRD-05 | Long labels are truncated or wrapped, with the full text available | Always | Required | Application's job |
| BRD-06 | The trail reflects the real hierarchy and matches the page and URL, including titles that load late | Always | Required | Application's job |
| BRD-07 | On small viewports the trail wraps or shows only the parent, without overflow | Always | Required | Application's job |
| BRD-08 | Focus is visible and targets are large enough | Always | Required | Application's job |
| BRD-09 | Separators and order are correct in right-to-left layout | Always | Required | Application's job |
| BRD-10 | Structured data for the trail is present and matches the visible trail | Public pages | Optional | Application's job |

## 7. Anti-patterns

- A trail built from browsing history.
- Separators read aloud as characters.
- The current page as a link to itself with no indication.
- A trail that disagrees with the URL.
- A long trail that overflows the screen.
- Showing breadcrumbs on a flat site.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| BRD-01 | Accessibility | Always | Region and list | Inspect the accessibility tree | Named region with an ordered list | Required | Automatable | Critical |
| BRD-02 | Accessibility | Always | Current page | Inspect the last item | Exposed as current | Required | Automatable | Critical |
| BRD-03 | Accessibility | Always | Separators | Read with a screen reader | Separators not announced | Required | Manual | Important |
| BRD-04 | Functional | Long trails | Collapsed middle | Use a very deep hierarchy, reveal hidden items by keyboard | First and last kept, hidden items reachable | If applicable | Automatable | Important |
| BRD-05 | Layout | Always | Long labels | Use very long labels | No breakage, full text available | Required | Automatable | Important |
| BRD-06 | Data | Always | Hierarchy accuracy | Visit pages at several depths, one with a title loaded late | Trail matches, no placeholder left behind | Required | Automatable | Important |
| BRD-07 | Layout | Always | Small viewports | Use a narrow viewport | No horizontal overflow | Required | Automatable | Important |
| BRD-08 | Accessibility | Always | Focus and targets | Tab through, use a touch device | Focus visible, targets usable | Required | Manual | Important |
| BRD-09 | Layout | Always | Right-to-left | Switch to right-to-left layout | Order and separators mirrored | Required | Manual | Nice-to-have |
| BRD-10 | Data | Public pages | Structured data | Compare the structured data with the visible trail | Identical | Optional | Automatable | Nice-to-have |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
