---
component: Video / audio player
id-prefix: MED
status: draft
---

# Video / audio player

## 1. When to use it vs alternatives

- **Player**: playing recorded or live video and audio.
- **Native controls**: the default choice for simple needs.
- **Custom controls**: when branding or features require them; they must match the native accessibility.
- **Iframe embed** (`IFR`): hosted players from a provider.

## 2. Anatomy and variants

Parts: media, play and pause, seek bar, time display, volume and mute, captions toggle, speed, fullscreen, poster image, transcript.

Variants: video vs audio, recorded vs live, custom vs native controls, single player vs several on a page.

## 3. States

Idle, loading, buffering, playing, paused, ended, error, muted, fullscreen, captions on.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Space or Enter on the play control | Plays or pauses |
| Arrow keys on the seek bar | Seek by a step |
| Arrow keys on the volume control | Change the volume |
| Escape in fullscreen | Exits fullscreen, returning focus |

Player shortcuts only apply when the player has focus.

## 5. Component-specific accessibility

- Every control has a name and exposes its state.
- Captions or a transcript are available for any spoken content.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| MED-01 | Play, pause, seek, volume, mute, captions and fullscreen are keyboard operable, named, and expose their state | Always | Required | Application's job |
| MED-02 | Captions for video and a transcript for audio are available and selectable, with readable captions | Spoken content | Required | Application's job |
| MED-03 | An audio description or equivalent is available when visuals carry information | Visual information | If applicable | Application's job |
| MED-04 | Media with sound does not start on its own, muted autoplay can be stopped, and moving content over five seconds can be paused | Autoplay | Required | Application's job |
| MED-05 | The seek bar exposes time as its value and can be moved by keyboard in steps | Always | Required | Application's job |
| MED-06 | Loading, buffering, error with retry, and an unsupported format fallback such as a download link, are shown | Always | Required | Application's job |
| MED-07 | Starting one player pauses the others | Several players | If applicable | Application's job |
| MED-08 | Resume position, end state and replay are defined | Long media | If applicable | Application's job |
| MED-09 | On mobile playback is inline as decided, fullscreen and orientation work, and data use is considered | Mobile use | Required | Application's job |
| MED-10 | Keyboard shortcuts do not clash with the page or assistive technology | Shortcuts | Required | Application's job |
| MED-11 | A poster image has a text alternative and the player reserves its aspect ratio | Always | Required | Application's job |
| MED-12 | A live stream shows a live indicator and does not offer a misleading seek bar | Live | If applicable | Application's job |
| MED-13 | Reduced motion and reduced data preferences are respected | Always | Optional | Application's job |
| MED-14 | Exiting fullscreen returns focus to the player | Fullscreen | Required | Application's job |
| MED-15 | A playback speed control is available and keyboard operable | Speed control | Optional | Application's job |

## 7. Anti-patterns

- Autoplay with sound.
- Custom controls built from unnamed icons.
- Captions burned into the video.
- A seek bar that works only by dragging.
- Shortcuts that capture keys for the whole page.
- No fallback when the format is unsupported.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| MED-01 | Keyboard | Always | Play, pause, seek, volume, mute, captions and fullscreen are keyboard operable, named, and expose their state | Use every control by keyboard with a screen reader | All operable, named, state exposed | Required | Manual | Critical |
| MED-02 | Accessibility | Spoken content | Captions for video and a transcript for audio are available and selectable, with readable captions | Turn captions on, change language | Captions in sync and legible, transcript reachable | Required | Manual | Critical |
| MED-03 | Accessibility | Visual information | An audio description or equivalent is available when visuals carry information | Review content without sight | Equivalent available | If applicable | Manual | Important |
| MED-04 | Functional | Autoplay | Media with sound does not start on its own, muted autoplay can be stopped, and moving content over five seconds can be paused | Load the page and watch for autoplay | No sound, pausable | Required | Automatable | Critical |
| MED-05 | Keyboard | Always | The seek bar exposes time as its value and can be moved by keyboard in steps | Seek by keyboard | Time value announced, steps work | Required | Automatable | Important |
| MED-06 | States | Always | Loading, buffering, error with retry, and an unsupported format fallback such as a download link, are shown | Throttle, break the source, use an unsupported format | States shown, fallback available | Required | Automatable | Critical |
| MED-07 | Functional | Several players | Starting one player pauses the others | Play two players | Only one plays | If applicable | Automatable | Important |
| MED-08 | Data | Long media | Resume position, end state and replay are defined | Leave and return, finish, replay | As defined | If applicable | Automatable | Important |
| MED-09 | Functional | Mobile use | On mobile playback is inline as decided, fullscreen and orientation work, and data use is considered | Use real devices | Works without surprises | Required | Manual | Important |
| MED-10 | Keyboard | Shortcuts | Keyboard shortcuts do not clash with the page or assistive technology | Use the shortcuts with and without focus in the player | Only active in the player | Required | Automatable | Important |
| MED-11 | Layout | Always | A poster image has a text alternative and the player reserves its aspect ratio | Load slowly | No shift, poster described | Required | Automatable | Important |
| MED-12 | States | Live | A live stream shows a live indicator and does not offer a misleading seek bar | Play a live stream | Indicator shown, seek as defined | If applicable | Automatable | Important |
| MED-13 | Functional | Always | Reduced motion and reduced data preferences are respected | Enable the preferences | Respected | Optional | Manual | Nice-to-have |
| MED-14 | Keyboard | Fullscreen | Exiting fullscreen returns focus to the player | Enter and exit fullscreen by keyboard | Focus returns to the control | Required | Automatable | Important |
| MED-15 | Keyboard | Speed control | A playback speed control is available and keyboard operable | Change speed by keyboard | Operable | Optional | Automatable | Nice-to-have |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
