---
component: Carousel
id-prefix: CAR
status: draft
---

# Carousel

## 1. When to use it vs alternatives

- **Carousel**: showing several slides in the same space when space is limited and no slide is critical.
- **Tabs** (`TAB`): switching between known views.
- **List or grid**: content users should compare or find easily. Do not hide important content only in a carousel.

## 2. Anatomy and variants

Parts: slides, previous and next controls, optional slide indicators, optional play and pause control.

Variants: manual vs autoplaying, one vs several slides in view, looping vs finite, touch swipe or not.

## 3. States

Slide active, other slides hidden, autoplaying, paused, first slide, last slide, loading.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Tab | Reaches controls and focusable content in the visible slide |
| Enter / Space | Activates the focused control |
| Arrow keys | May move between indicators, where the pattern defines it |

## 5. Component-specific accessibility

- The carousel is a named region and slides are labeled with their position ('2 of 5').
- Slides that are not visible are not focusable and are hidden from assistive technology.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| CAR-01 | Previous and next controls are named, keyboard operable, and the behavior at the ends is defined | Always | Required | Application's job |
| CAR-02 | Autoplay is off by default or has a pause control, stops on hover and focus, and respects reduced motion | Autoplay | If applicable | Application's job |
| CAR-03 | Indicators are controls named by position, with the current one exposed | Indicators | If applicable | Application's job |
| CAR-04 | The region and slides are labeled with position, and hidden slides are not focusable or announced | Always | Required | Usually provided by primitives |
| CAR-05 | Swipe and drag have control equivalents, and vertical page scrolling is not blocked | Touch gestures | If applicable | Application's job |
| CAR-06 | Slide changes are announced politely when manual and not announced during autoplay | Always | Required | Application's job |
| CAR-07 | Looping behavior is defined and consistent | Looping | Required | Application's job |
| CAR-08 | Only nearby slide media load, and slides of different heights do not cause jumps | Always | Required | Application's job |
| CAR-09 | Zero, one and many slides are handled | Always | Required | Application's job |
| CAR-10 | Several slides in view keep the focused slide visible | Multiple slides in view | If applicable | Application's job |
| CAR-11 | Moving between slides does not move focus unexpectedly | Always | Required | Application's job |
| CAR-12 | Transitions are reduced and interrupted transitions end in a consistent state | Animated | Required | Application's job |
| CAR-13 | Direction follows right-to-left layout | Always | Required | Application's job |

## 7. Anti-patterns

- Autoplay with no way to stop it.
- Hidden slides still in the tab order.
- Critical content shown only in a carousel.
- Dots with no names.
- Announcing every autoplay change.
- Swipe as the only way to move.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| CAR-01 | Keyboard | Always | Previous and next controls are named, keyboard operable, and the behavior at the ends is defined | Use the controls at the first and last slide | Works, ends handled as defined | Required | Automatable | Critical |
| CAR-02 | Accessibility | Autoplay | Autoplay is off by default or has a pause control, stops on hover and focus, and respects reduced motion | Observe autoplay, hover, focus, reduced motion | Pausable and stops on interaction | If applicable | Automatable | Critical |
| CAR-03 | Accessibility | Indicators | Indicators are controls named by position, with the current one exposed | Use the indicators with a screen reader | 'Slide 2 of 5', current exposed | If applicable | Manual | Important |
| CAR-04 | Accessibility | Always | The region and slides are labeled with position, and hidden slides are not focusable or announced | Tab and read with a screen reader | Only the visible slide reachable | Required | Manual | Critical |
| CAR-05 | Functional | Touch gestures | Swipe and drag have control equivalents, and vertical page scrolling is not blocked | Swipe and use the controls on a touch device | Both work, page scrolls | If applicable | Manual | Important |
| CAR-06 | Accessibility | Always | Slide changes are announced politely when manual and not announced during autoplay | Change slides with a screen reader | Announced as appropriate | Required | Manual | Important |
| CAR-07 | Functional | Looping | Looping behavior is defined and consistent | Go past the last and first slides | Loops or stops as defined | Required | Automatable | Important |
| CAR-08 | Layout | Always | Only nearby slide media load, and slides of different heights do not cause jumps | Use slides of different size and slow network | No jumps, efficient loading | Required | Automatable | Important |
| CAR-09 | States | Always | Zero, one and many slides are handled | Render 0, 1, 50 slides | Controls hidden or disabled as defined | Required | Automatable | Important |
| CAR-10 | Keyboard | Multiple slides in view | Several slides in view keep the focused slide visible | Tab to a partly visible slide | It is scrolled fully into view | If applicable | Automatable | Important |
| CAR-11 | Keyboard | Always | Moving between slides does not move focus unexpectedly | Change slides with focus on a control | Focus stays | Required | Automatable | Critical |
| CAR-12 | Functional | Animated | Transitions are reduced and interrupted transitions end in a consistent state | Change slides rapidly, enable reduced motion | Consistent | Required | Automatable | Important |
| CAR-13 | Layout | Always | Direction follows right-to-left layout | Switch to right-to-left layout | Controls and motion mirrored | Required | Manual | Nice-to-have |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
