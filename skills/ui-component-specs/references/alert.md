---
component: Alert / banner
id-prefix: ALR
status: draft
---

# Alert / banner

## 1. When to use it vs alternatives

- **Alert or banner**: a message about the page or a section that the user should notice and that may need to stay (a failed save, a maintenance notice, a policy change).
- **Toast** (`TST`): brief feedback about something that just happened.
- **Inline validation** (`VAL`): errors tied to a field.
- **Dialog** (`DLG`): when the user must decide before continuing.
- **Empty or error state** (`EMP`): a region that has nothing to show.

## 2. Anatomy and variants

Parts: icon, title, message, optional action, optional dismiss control.

Variants that change which capabilities apply:

- Severity: info, success, warning, error
- Page-wide banner vs message inside a section
- Dismissible vs persistent
- Present at page load vs inserted after an event
- With or without an action

## 3. States

Visible, dismissed, hover and focus on its controls, several alerts stacked.

## 4. Behavior and keyboard interaction

Alerts do not take focus when they appear. Their controls are reached in the normal tab order.

| Key | Result |
|---|---|
| Tab | Reaches the action and dismiss controls |
| Enter / Space | Activates the focused control |

## 5. Component-specific accessibility

- A message inserted after load is announced, with urgency matching severity. A message present at load is part of the page content.
- Severity is conveyed in text or an icon with a name.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| ALR-01 | Severity is shown by text or a named icon, not by color alone | Always | Required | Application's job |
| ALR-02 | A message inserted after load is announced, with urgency matching severity, and is not announced twice | Inserted after an event | Required | Usually provided by primitives |
| ALR-03 | A dismiss control is keyboard operable, and focus goes somewhere logical after dismissal | Dismissible | If applicable | Application's job |
| ALR-04 | A dismissed banner stays dismissed across reloads and pages as decided | Dismissible banners | If applicable | Application's job |
| ALR-05 | An action inside the alert is reachable and works | Alert with action | If applicable | Application's job |
| ALR-06 | Placement is near the relevant content, and sticky banners do not cover content, focus or fixed controls, including at 200% zoom | Always | Required | Application's job |
| ALR-07 | Several alerts are prioritized, stacked in a defined order and de-duplicated | Several alerts | If applicable | Application's job |
| ALR-08 | Long messages wrap and links inside them are usable | Always | Required | Application's job |
| ALR-09 | Alerts that matter are never removed automatically | Always | Required | Application's job |
| ALR-10 | Contrast, dark mode, zoom and right-to-left layout are respected | Always | Required | Application's job |

## 7. Anti-patterns

- Color as the only severity cue.
- An alert that moves keyboard focus.
- An important error that disappears after a few seconds.
- A dismissed banner that returns on every page.
- An alert announced both on insertion and again on every render.
- A sticky banner that hides the focused element.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| ALR-01 | Accessibility | Always | Severity cues | View each severity in grayscale | Distinguishable without color | Required | Manual | Important |
| ALR-02 | Accessibility | Inserted after an event | Announcement | Insert an error and an info alert with a screen reader | Announced once, error more urgent | Required | Manual | Critical |
| ALR-03 | Keyboard | Dismissible | Dismissal | Dismiss by keyboard | Removed, focus logical | If applicable | Automatable | Important |
| ALR-04 | Data | Dismissible banners | Dismissal persistence | Dismiss, reload, navigate | Stays dismissed as decided | If applicable | Automatable | Important |
| ALR-05 | Functional | Alert with action | Action | Activate the action | Works, alert updated | If applicable | Automatable | Important |
| ALR-06 | Layout | Always | Placement | Show a sticky banner, tab through, zoom to 200% | Nothing covered | Required | Manual | Important |
| ALR-07 | Functional | Several alerts | Several alerts | Trigger several, including duplicates | Prioritized, stacked, de-duplicated | If applicable | Automatable | Nice-to-have |
| ALR-08 | Layout | Always | Long messages | Use a very long message with a link | Wraps, link usable | Required | Automatable | Nice-to-have |
| ALR-09 | Functional | Always | No auto-removal | Wait after an error appears | Still there | Required | Automatable | Critical |
| ALR-10 | Layout | Always | Contrast and layout | Check contrast, dark mode, zoom, right-to-left | Readable and mirrored | Required | Manual | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
