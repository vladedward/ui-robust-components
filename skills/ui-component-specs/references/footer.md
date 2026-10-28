---
component: Footer
id-prefix: FTR
status: draft
---

# Footer

## 1. When to use it vs alternatives

- **Footer**: site-wide information and secondary links (company, legal, support, contact).
- **Navbar** (`NAV`): primary navigation, not repeated in the footer without reason.
- **Page-level content**: anything the user needs to complete a task belongs in the main content.

## 2. Anatomy and variants

Parts: content-info region, link groups with headings, legal text, optional language or region switch, optional newsletter form, optional social links.

Variants: simple vs multi-column, sticky vs end of page, with forms or controls, with infinite scrolling pages.

## 3. States

Default, link states, switch open, form states if present.

## 4. Behavior and keyboard interaction

Links and controls are reached in visual order at the end of the page. A user can reach the footer without scrolling through endless content.

## 5. Component-specific accessibility

- The footer is a content-info region, one per page.
- Link groups have headings or names.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| FTR-01 | The footer is a content-info region, once per page | Always | Required | Application's job |
| FTR-02 | Link groups have headings or names and use lists | Link groups | Required | Application's job |
| FTR-03 | The footer is reachable by keyboard even on pages that load more content while scrolling | Infinite scrolling pages | Required | Application's job |
| FTR-04 | On short pages the footer sits at the bottom of the viewport, and a sticky footer never covers content | Always | Required | Application's job |
| FTR-05 | Links are descriptive, external links are identified, and icon links have names | Always | Required | Application's job |
| FTR-06 | The layout reflows to a single column on small viewports and at 200% zoom | Always | Required | Application's job |
| FTR-07 | Language, region and consent controls work, persist and are named | Controls present | If applicable | Application's job |
| FTR-08 | Contrast, right-to-left layout and dark mode are respected | Always | Required | Application's job |
| FTR-09 | A form in the footer follows the form rules | Newsletter form | If applicable | Application's job |
| FTR-10 | Dynamic content such as the year is correct | Dynamic content | Optional | Application's job |

## 7. Anti-patterns

- A footer so long it hides the page end on infinite scroll.
- Footer links grouped only by spacing, with no headings.
- An icon-only social link with no name.
- A sticky footer covering the focused element.
- Copyright year hard coded.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| FTR-01 | Accessibility | Always | The footer is a content-info region, once per page | Inspect the accessibility tree | One content-info region | Required | Automatable | Important |
| FTR-02 | Accessibility | Link groups | Link groups have headings or names and use lists | Inspect each group | Named group, links in lists | Required | Automatable | Important |
| FTR-03 | Keyboard | Infinite scrolling pages | The footer is reachable by keyboard even on pages that load more content while scrolling | Reach the end of such a page by keyboard | Footer links reachable without a loop | Required | Automatable | Critical |
| FTR-04 | Layout | Always | On short pages the footer sits at the bottom of the viewport, and a sticky footer never covers content | Render a short page, a long page and a sticky footer | At the bottom, nothing covered | Required | Automatable | Important |
| FTR-05 | Accessibility | Always | Links are descriptive, external links are identified, and icon links have names | List the links with names | Meaningful, no unnamed icon links | Required | Automatable | Important |
| FTR-06 | Layout | Always | The layout reflows to a single column on small viewports and at 200% zoom | Resize and zoom | No overflow, order logical | Required | Manual | Important |
| FTR-07 | Functional | Controls present | Language, region and consent controls work, persist and are named | Change language and reload | Applied and persisted, labeled | If applicable | Automatable | Important |
| FTR-08 | Layout | Always | Contrast, right-to-left layout and dark mode are respected | Check contrast, direction, dark mode | Readable and mirrored | Required | Manual | Nice-to-have |
| FTR-09 | Validation | Newsletter form | A form in the footer follows the form rules | Submit empty, invalid and valid | Errors associated, success shown | If applicable | Automatable | Important |
| FTR-10 | Data | Dynamic content | Dynamic content such as the year is correct | Render at year boundaries | Correct | Optional | Automatable | Nice-to-have |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
