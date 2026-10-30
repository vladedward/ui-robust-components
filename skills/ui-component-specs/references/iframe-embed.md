---
component: Iframe / embeds
id-prefix: IFR
status: draft
---

# Iframe / embeds

## 1. When to use it vs alternatives

- **Iframe**: embedding content from another origin (maps, videos, payment forms, widgets).
- **Native component**: preferred when you control the content.
- **Link**: when the embedded content is optional and heavy.

## 2. Anatomy and variants

Parts: frame, title, placeholder or facade, optional consent step, fallback link.

Variants: first party vs third party, fixed vs content-sized height, loaded immediately vs on demand, with messaging between page and frame.

## 3. States

Not loaded, loading, loaded, blocked or failed, awaiting consent.

## 4. Behavior and keyboard interaction

Keyboard focus can enter and leave the frame. Tab continues through the page after the frame.

## 5. Component-specific accessibility

- The frame has a descriptive title.
- Content inside the frame must itself be accessible, which the page cannot fix.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| IFR-01 | The frame has a descriptive title | Always | Required | Application's job |
| IFR-02 | The frame is restricted: sandbox, minimal permissions, trusted origins, and the page controls who may embed it | Always | Required | Application's job |
| IFR-03 | Loading is deferred where possible, with a placeholder and a fallback if blocked or failed | Always | Required | Application's job |
| IFR-04 | The size is responsive without double scrollbars, and height changes from the frame are accepted only from the expected origin | Content-sized | Required | Application's job |
| IFR-05 | Keyboard focus cannot get trapped in the frame and the order around it is logical | Always | Required | Application's job |
| IFR-06 | Third-party content that tracks users is not loaded before consent, with a placeholder to ask for it | Third-party tracking | If applicable | Application's job |
| IFR-07 | Touch scrolling does not get stuck inside the frame | Scrollable frame | Required | Application's job |
| IFR-08 | Messages to and from the frame validate origin and schema | Messaging | If applicable | Application's job |
| IFR-09 | Print and no-script users get a link or a text alternative | Always | Required | Application's job |
| IFR-10 | Heavy embeds use a lightweight facade so they do not delay the main content | Heavy embeds | If applicable | Application's job |
| IFR-11 | Zoom and small viewports keep the frame usable | Always | Required | Application's job |
| IFR-12 | Fullscreen is allowed only where needed and can be exited by keyboard | Fullscreen | Optional | Application's job |

## 7. Anti-patterns

- An untitled frame.
- A frame with full permissions from an unknown origin.
- Trusting any postMessage.
- A map that traps the Tab key.
- Loading ad or tracking frames before consent.
- A fixed height that clips content on mobile.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| IFR-01 | Accessibility | Always | The frame has a descriptive title | Inspect each frame | Descriptive title present | Required | Automatable | Critical |
| IFR-02 | Validation | Always | The frame is restricted: sandbox, minimal permissions, trusted origins, and the page controls who may embed it | Review the frame attributes and response headers | Least privilege applied | Required | Manual | Critical |
| IFR-03 | States | Always | Loading is deferred where possible, with a placeholder and a fallback if blocked or failed | Block the frame and throttle the network | Placeholder, fallback link | Required | Automatable | Critical |
| IFR-04 | Layout | Content-sized | The size is responsive without double scrollbars, and height changes from the frame are accepted only from the expected origin | Resize and change frame content height | Fits, no double scroll, origin checked | Required | Automatable | Important |
| IFR-05 | Keyboard | Always | Keyboard focus cannot get trapped in the frame and the order around it is logical | Tab in and out | Can leave the frame in both directions | Required | Automatable | Critical |
| IFR-06 | Functional | Third-party tracking | Third-party content that tracks users is not loaded before consent, with a placeholder to ask for it | Load without consent and grant it | Not loaded until consent | If applicable | Automatable | Critical |
| IFR-07 | Layout | Scrollable frame | Touch scrolling does not get stuck inside the frame | Scroll over the frame on a touch device | Page scroll continues | Required | Manual | Important |
| IFR-08 | Validation | Messaging | Messages to and from the frame validate origin and schema | Send a message from another origin and a malformed one | Rejected | If applicable | Automatable | Critical |
| IFR-09 | Accessibility | Always | Print and no-script users get a link or a text alternative | Print and disable scripts | Alternative present | Required | Manual | Important |
| IFR-10 | Functional | Heavy embeds | Heavy embeds use a lightweight facade so they do not delay the main content | Measure loading with and without the facade | Main content not delayed | If applicable | Automatable | Important |
| IFR-11 | Layout | Always | Zoom and small viewports keep the frame usable | Zoom to 200% and use a narrow viewport | Usable | Required | Manual | Important |
| IFR-12 | Keyboard | Fullscreen | Fullscreen is allowed only where needed and can be exited by keyboard | Enter and leave fullscreen | Escape exits | Optional | Automatable | Nice-to-have |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
