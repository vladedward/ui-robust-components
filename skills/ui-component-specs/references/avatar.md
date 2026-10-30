---
component: Avatar
id-prefix: AVT
status: draft
---

# Avatar

## 1. When to use it vs alternatives

- **Avatar**: a small image or initials representing a person or entity.
- **Image** (`IMG`): content imagery.
- **Icon**: a symbol that is not a person.

## 2. Anatomy and variants

Parts: image, initials fallback, optional status indicator, optional group with overflow.

Variants: image vs initials, single vs stacked group, with status indicator, interactive (opens a profile or menu).

## 3. States

Loading, image shown, fallback shown, with status, hover and focus if interactive.

## 4. Behavior and keyboard interaction

Not interactive unless it opens something. If it does, it is a button or a link.

## 5. Component-specific accessibility

- The person is named in text, either by the avatar or by an adjacent name.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| AVT-01 | The image has a text alternative with the name, or is decorative when the name is adjacent, and initials are the fallback | Always | Required | Application's job |
| AVT-02 | Initials work for single names, non-Latin scripts, emoji and empty names | Initials fallback | Required | Application's job |
| AVT-03 | A failed or slow image falls back without a broken icon or layout change | Image | Required | Application's job |
| AVT-04 | Shape and size are consistent, and non-square images crop sensibly | Image | Required | Application's job |
| AVT-05 | The fallback color is stable per person and has sufficient contrast | Initials fallback | Required | Application's job |
| AVT-06 | Status indicators have a text alternative and are not color-only | Status indicator | If applicable | Application's job |
| AVT-07 | Stacked groups show an overflow count and make the full list available | Group | If applicable | Application's job |
| AVT-08 | An interactive avatar is a button or link with a name | Interactive | If applicable | Application's job |
| AVT-09 | Zoom, right-to-left layout and dark mode keep it readable | Always | Required | Application's job |

## 7. Anti-patterns

- Alt text 'avatar' on every image.
- Initials from the first two letters of an email.
- A broken-image icon for a missing photo.
- A green dot as the only presence signal.
- Stack overflow count that hides who the others are.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| AVT-01 | Accessibility | Always | The image has a text alternative with the name, or is decorative when the name is adjacent, and initials are the fallback | Render with and without an adjacent name | No duplicate or missing name | Required | Automatable | Important |
| AVT-02 | Data | Initials fallback | Initials work for single names, non-Latin scripts, emoji and empty names | Use 'Ana', 'Ion Popescu', '李雷', an emoji and an empty name | Sensible initials or a neutral placeholder | Required | Automatable | Important |
| AVT-03 | States | Image | A failed or slow image falls back without a broken icon or layout change | Block the image, delay it | Fallback shown, same size | Required | Automatable | Critical |
| AVT-04 | Layout | Image | Shape and size are consistent, and non-square images crop sensibly | Use wide and tall images | Uniform shape, face area kept where possible | Required | Manual | Important |
| AVT-05 | Accessibility | Initials fallback | The fallback color is stable per person and has sufficient contrast | Render many names | Stable colors, readable initials | Required | Automatable | Important |
| AVT-06 | Accessibility | Status indicator | Status indicators have a text alternative and are not color-only | Inspect with a screen reader and in grayscale | Status announced and distinct | If applicable | Manual | Important |
| AVT-07 | Functional | Group | Stacked groups show an overflow count and make the full list available | Render more avatars than fit | Overflow count shown, all members reachable | If applicable | Automatable | Important |
| AVT-08 | Functional | Interactive | An interactive avatar is a button or link with a name | Activate by keyboard | Operable and named | If applicable | Automatable | Important |
| AVT-09 | Layout | Always | Zoom, right-to-left layout and dark mode keep it readable | Zoom, mirror, dark mode | Readable | Required | Manual | Nice-to-have |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
