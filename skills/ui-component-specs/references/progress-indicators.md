---
component: Progress, spinner, skeleton
id-prefix: PRG
status: draft
---

# Progress, spinner, skeleton

## 1. When to use it vs alternatives

- **Progress bar (determinate)**: the amount of work is known (upload, multi-step process).
- **Spinner (indeterminate)**: the duration is unknown and short.
- **Skeleton**: the layout of the content is known, and the content is loading.
- **Stepper** (`STP`): navigable steps, not a loading indicator.
- **No indicator**: operations that finish fast, where a flash of an indicator is worse than none.

## 2. Anatomy and variants

Parts: indicator, optional label or percentage, optional cancel action, optional busy region.

Variants that change which capabilities apply:

- Determinate vs indeterminate
- Standalone vs inside a button or overlaying a region
- Skeleton placeholders vs spinner
- A single operation vs several concurrent ones

## 3. States

Hidden (not yet shown), loading, progressing, completed, failed, canceled, timed out.

## 4. Behavior and keyboard interaction

Indicators are not interactive, except an optional cancel action. They do not take focus. A region that is loading can stay focusable if its controls are still valid.

## 5. Component-specific accessibility

- Determinate progress exposes its value and range. Indeterminate progress exposes that it is in progress.
- The loading region exposes a busy state.
- Completion and failure are announced, not each percentage.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| PRG-01 | The kind of indicator matches what is known, and a determinate value, range and text are exposed | Always | Required | Usually provided by primitives |
| PRG-02 | The indicator has an accessible name and exposes that it is in progress | Always | Required | Application's job |
| PRG-03 | Completion and failure are announced, with updates only at meaningful points | Always | Required | Application's job |
| PRG-04 | A long indeterminate wait leads to a message, a way to cancel, or a failure state | Long waits | If applicable | Application's job |
| PRG-05 | Skeletons match the final layout, cause no layout shift and are not read as content, with a busy state on the region | Skeletons | If applicable | Application's job |
| PRG-06 | An indicator appears only after a short delay and, once shown, stays long enough not to flash | Always | Required | Application's job |
| PRG-07 | An overlay or an in-button indicator blocks the right interaction and keeps focus in a logical place | Overlay or in-button | If applicable | Application's job |
| PRG-08 | The transition from loading to loaded, to failure with retry, and to empty is defined | Always | Required | Application's job |
| PRG-09 | Animation respects reduced motion | Animated | Required | Application's job |
| PRG-10 | The indicator reserves its space so the layout does not move | Always | Required | Application's job |
| PRG-11 | A determinate value never goes backward, never exceeds the maximum, and reaches it only when the work is done | Determinate | If applicable | Application's job |
| PRG-12 | Concurrent operations do not stack many indicators | Several operations | If applicable | Application's job |
| PRG-13 | Contrast is sufficient and meaning does not rely on color | Always | Required | Application's job |

## 7. Anti-patterns

- A spinner flashing for 50 milliseconds.
- A progress bar that reaches 100% and then keeps waiting.
- A percentage announced every second to a screen reader.
- An endless spinner with no failure state.
- Skeletons that are a different shape from the content, causing a jump.
- A full-page overlay for a small part of the page.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| PRG-01 | Accessibility | Always | Kind and value | Inspect a determinate and an indeterminate indicator | Value, range or in-progress state exposed | Required | Automatable | Critical |
| PRG-02 | Accessibility | Always | Name | Inspect the name | Meaningful | Required | Automatable | Important |
| PRG-03 | Accessibility | Always | Announcements | Run an operation with a screen reader | Completion and failure announced, no flood | Required | Manual | Critical |
| PRG-04 | Functional | Long waits | Long waits | Delay the operation far beyond normal | Message, cancel or failure appears | If applicable | Automatable | Important |
| PRG-05 | Layout | Skeletons | Skeleton layout | Load slowly and compare with the loaded layout | No shift, not read as content | If applicable | Automatable | Important |
| PRG-06 | Functional | Always | Delay and minimum duration | Run a very fast and a slightly slow operation | No flash for fast, no blink for slow | Required | Automatable | Important |
| PRG-07 | Keyboard | Overlay or in-button | Interaction | Operate controls during loading | Blocked or allowed as decided, focus logical | If applicable | Automatable | Important |
| PRG-08 | States | Always | Transitions | Finish, fail and return nothing | Right state each time, retry works | Required | Automatable | Critical |
| PRG-09 | Accessibility | Animated | Reduced motion | Enable the reduced motion preference | Animation reduced | Required | Manual | Nice-to-have |
| PRG-10 | Layout | Always | Stable space | Show and hide the indicator | No layout movement | Required | Automatable | Important |
| PRG-11 | Data | Determinate | Value accuracy | Run with uneven progress and a restart | Value monotonic, within range, full only at the end | If applicable | Automatable | Important |
| PRG-12 | Layout | Several operations | Concurrent operations | Start several at once | One coherent indication | If applicable | Automatable | Nice-to-have |
| PRG-13 | Accessibility | Always | Contrast and color | Check contrast, view in grayscale | Visible, not color-dependent | Required | Manual | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
