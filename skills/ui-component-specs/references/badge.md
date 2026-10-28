---
component: Badge
id-prefix: BDG
status: draft
---

# Badge

## 1. When to use it vs alternatives

- **Badge**: a small count or status attached to another element (unread count, status, new).
- **Chip or tag** (inside `combobox.md`): an interactive or removable value.
- **Alert** (`ALR`): a message that needs reading.

## 2. Anatomy and variants

Parts: number, short text or a dot, host element.

Variants: count, status text, dot only, standalone vs attached to an icon or button.

## 3. States

Visible, hidden at zero, capped, updating.

## 4. Behavior and keyboard interaction

Not interactive on its own. If it is clickable it is a button or a link.

## 5. Component-specific accessibility

- The meaning is available to assistive technology in context, for example '3 unread messages'.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| BDG-01 | The meaning is conveyed in text in context, not only visually | Always | Required | Application's job |
| BDG-02 | Status is not shown by color alone, and contrast is sufficient | Always | Required | Application's job |
| BDG-03 | Large counts are capped for display while the true value stays available | Counts | Required | Application's job |
| BDG-04 | Zero, hidden and dot-only behavior is defined, and a dot has a text alternative | Counts or dots | Required | Application's job |
| BDG-05 | Meaningful updates are announced, not every change | Live counts | If applicable | Application's job |
| BDG-06 | The badge does not overlap or get clipped by its host, in both layout directions | Attached to a host | Required | Application's job |
| BDG-07 | A clickable badge is a real button or link with a name | Interactive | If applicable | Application's job |
| BDG-08 | Long and translated text fits | Text badges | Required | Application's job |

## 7. Anti-patterns

- A red dot as the only signal.
- A number badge announced as a bare number.
- A badge that overlaps the icon it describes.
- A decorative badge with a click handler and no role.
- Counts that grow beyond the badge width.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| BDG-01 | Accessibility | Always | The meaning is conveyed in text in context, not only visually | Inspect the host element name with a screen reader | Name includes the badge meaning | Required | Manual | Critical |
| BDG-02 | Accessibility | Always | Status is not shown by color alone, and contrast is sufficient | View in grayscale and check contrast | Distinguishable and readable | Required | Manual | Important |
| BDG-03 | Data | Counts | Large counts are capped for display while the true value stays available | Show 0, 5, 99, 100, 10000 | Display capped, real value in text | Required | Automatable | Important |
| BDG-04 | States | Counts or dots | Zero, hidden and dot-only behavior is defined, and a dot has a text alternative | Reduce the count to zero, show a dot | Hidden or shown as defined, dot named | Required | Automatable | Important |
| BDG-05 | Accessibility | Live counts | Meaningful updates are announced, not every change | Change the count rapidly with a screen reader | Meaningful updates announced once | If applicable | Manual | Important |
| BDG-06 | Layout | Attached to a host | The badge does not overlap or get clipped by its host, in both layout directions | Check on small hosts and in right-to-left layout | Visible and positioned correctly | Required | Automatable | Important |
| BDG-07 | Functional | Interactive | A clickable badge is a real button or link with a name | Activate by keyboard | Operable and named | If applicable | Automatable | Important |
| BDG-08 | Layout | Text badges | Long and translated text fits | Use a longer language | No overflow | Required | Automatable | Nice-to-have |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
