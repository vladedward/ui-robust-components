---
component: Link
id-prefix: LNK
status: draft
---

# Link

## 1. When to use it vs alternatives

- **Link**: navigates to another page, a location in the page, a file, or an external site.
- **Button** (`BTN`): performs an action on the current page. If it does not navigate, it is a button, even when styled as a link.
- **Navigation components** (`NAV`, `SID`, `BRD`): collections of links with their own rules.

## 2. Anatomy and variants

Parts: link text (or an image with alternative text), optional icon, destination.

Variants that change which capabilities apply:

- Inline in text vs standalone
- Internal vs external destination
- Opens in the same or a new window
- A file download
- In-page anchor
- Email or phone link
- Image link

Also covers the **skip link** variant through the **Applies when** column (`LNK-15`, `LNK-16`). Where skip links sit in the page is in `navbar.md` (`NAV-04`).

## 3. States

Default, visited, hover, focus, active, current page, disabled (avoid).

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Enter | Follows the link |
| Tab / Shift+Tab | Moves between links |

A real link also works with the browser's "open in a new tab", copy address and middle-button behavior.

## 5. Component-specific accessibility

- The name makes sense out of context, for example in a list of links.
- Links are not identified by color alone in text.
- A change of window or a download is stated.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| LNK-01 | A real link with a destination, so keyboard, new-tab and copy behavior work | Always | Required | Application's job |
| LNK-02 | The text describes the destination, and identical text does not lead to different places | Always | Required | Application's job |
| LNK-03 | Links in running text are distinguishable without color alone | Inline links | Required | Application's job |
| LNK-04 | The current page link is exposed | Link to the current page | If applicable | Application's job |
| LNK-05 | External links are identified, safe against the opened page controlling the origin, and a new window is announced and avoided by default | External links | If applicable | Application's job |
| LNK-06 | Hover, focus, visited and active states are distinct and have sufficient contrast | Always | Required | Application's job |
| LNK-07 | Downloads state the file type and size | Download links | If applicable | Application's job |
| LNK-08 | Navigation is a link, an action is a button | Always | Required | Application's job |
| LNK-09 | In-page anchors point to an existing target, and focus and scroll move to it | In-page anchors | Required | Application's job |
| LNK-10 | Long addresses wrap without breaking the layout | Always | Required | Application's job |
| LNK-11 | A link that is unavailable is removed or explained instead of being silently disabled | Can be unavailable | If applicable | Application's job |
| LNK-12 | Targets are large enough for standalone links | Standalone links | Required | Application's job |
| LNK-13 | An image link has alternative text describing the destination | Image links | If applicable | Application's job |
| LNK-14 | Email and phone links work on the devices that use them and show the address or number | Email or phone links | If applicable | Application's job |
| LNK-15 | A skip link is the first focusable element, becomes visible on focus, and moves focus to the main content, which can receive focus | Skip link | Required | Application's job |
| LNK-16 | Skip links keep working after navigation inside an application, and several skip links lead to the right targets | Skip link | If applicable | Application's job |

## 7. Anti-patterns

- "Click here" and "read more" repeated with no context.
- A link element with no destination, used as a button.
- A button used to navigate, so the page cannot be opened in a new tab.
- Links that differ only by color in a paragraph.
- Opening a new window without saying so.
- An anchor pointing at an id that does not exist.
- A disabled link that cannot be explained.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| LNK-01 | Functional | Always | Real link | Follow with Enter, open in a new tab, copy the address | All work | Required | Automatable | Critical |
| LNK-02 | Accessibility | Always | Descriptive text | List all links on a page | Each makes sense out of context, no clashes | Required | Automatable | Important |
| LNK-03 | Accessibility | Inline links | Visual distinction | View a paragraph in grayscale | Links distinguishable | Required | Manual | Important |
| LNK-04 | Accessibility | Link to the current page | Current page | Inspect the link | Exposed as current | If applicable | Automatable | Important |
| LNK-05 | Functional | External links | External links | Inspect and follow external links | Identified, safe attributes, new window announced | If applicable | Automatable | Important |
| LNK-06 | Accessibility | Always | States | Hover, focus, visit and press | Each state distinct, contrast sufficient | Required | Manual | Important |
| LNK-07 | Functional | Download links | Download | Inspect the link text | Type and size stated | If applicable | Manual | Nice-to-have |
| LNK-08 | Accessibility | Always | Link vs button | Review each control | Navigation is a link, action is a button | Required | Manual | Important |
| LNK-09 | Functional | In-page anchors | Anchors | Follow each anchor | Target exists, focus and scroll move there | Required | Automatable | Important |
| LNK-10 | Layout | Always | Long addresses | Use a very long address in text | Wraps, no overflow | Required | Automatable | Nice-to-have |
| LNK-11 | States | Can be unavailable | Unavailable link | Make a link unavailable | Removed or explained | If applicable | Manual | Nice-to-have |
| LNK-12 | Layout | Standalone links | Target size | Measure and use a touch device | Large enough | Required | Manual | Important |
| LNK-13 | Accessibility | Image links | Image link | Inspect the name | Describes the destination | If applicable | Automatable | Important |
| LNK-14 | Functional | Email or phone links | Email and phone | Follow on a real device | Opens the right application, value visible | If applicable | Manual | Nice-to-have |
| LNK-15 | Keyboard | Skip link | A skip link is the first focusable element, becomes visible on focus, and moves focus to the main content, which can receive focus | Press Tab on load and activate it | First stop, visible, focus lands in the main content | Required | Automatable | Critical |
| LNK-16 | Functional | Skip link | Skip links keep working after navigation inside an application, and several skip links lead to the right targets | Navigate to another route, activate the skip link | Focus lands in the new main content | If applicable | Automatable | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
