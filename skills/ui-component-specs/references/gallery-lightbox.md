---
component: Gallery / lightbox
id-prefix: GAL
status: draft
---

# Gallery / lightbox

> The lightbox is a modal dialog: also verify `dialog.md` (focus, Escape, focus return, inert page, scroll lock).

## 1. When to use it vs alternatives

- **Gallery**: a set of images (thumbnails) that the user can open at a larger size and browse.
- **Carousel** (`CAR`): a rotating set of slides in place.
- **Image** (`IMG`): one image.

## 2. Anatomy and variants

Parts: thumbnail grid or strip, lightbox with the large image, previous and next controls, counter, caption, close action, optional zoom, optional thumbnail strip.

Variants: images only vs mixed media, with zoom and pan, with deep links, touch gestures.

## 3. States

Closed, open, loading image, image failed, zoomed, first and last item.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Arrow keys | Previous / next item |
| Escape | Closes the lightbox, returning focus to the thumbnail |
| Home / End | First / last item, where defined |

## 5. Component-specific accessibility

- The lightbox has dialog semantics and a name.
- The position ('3 of 12') and each image's alternative and caption are exposed.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| GAL-01 | Opening and closing follow dialog behavior: focus in, Escape closes, focus returns to the thumbnail | Always | Required | Usually provided by primitives |
| GAL-02 | Previous and next work by controls and arrow keys, the ends are defined, and the position is announced | Always | Required | Application's job |
| GAL-03 | Each item has an alternative and a caption that fits | Always | Required | Application's job |
| GAL-04 | Zoom and pan have keyboard alternatives, a reset, and do not break closing | Zoom and pan | If applicable | Application's job |
| GAL-05 | Adjacent images preload, with loading and failure states per image | Always | Required | Application's job |
| GAL-06 | A thumbnail strip marks the current item and scrolls it into view | Thumbnail strip | If applicable | Application's job |
| GAL-07 | Swipe has control equivalents and does not conflict with page gestures | Touch gestures | If applicable | Application's job |
| GAL-08 | A deep link opens a specific item, and the back action closes the lightbox | Deep links | If applicable | Application's job |
| GAL-09 | Tall, wide and small images fit the viewport, including on rotation and resize | Always | Required | Application's job |
| GAL-10 | Video items pause when navigating away from them | Mixed media | If applicable | Application's job |
| GAL-11 | The page behind is inert and does not scroll | Always | Required | Usually provided by primitives |
| GAL-12 | Download and share actions are named | Actions | Optional | Application's job |
| GAL-13 | An empty gallery and a single image are handled | Always | Required | Application's job |
| GAL-14 | Thumbnails keep their aspect ratios and order, and load lazily | Always | Required | Application's job |

## 7. Anti-patterns

- A lightbox that does not trap focus.
- Navigation by swipe only.
- No counter or caption.
- Opening the full-size file for every thumbnail at once.
- A blank view while the next image loads.
- Page scrolling behind the lightbox.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| GAL-01 | Keyboard | Always | Opening and closing follow dialog behavior: focus in, Escape closes, focus returns to the thumbnail | Open from a thumbnail, close | Focus inside, returns to the same thumbnail | Required | Automatable | Critical |
| GAL-02 | Keyboard | Always | Previous and next work by controls and arrow keys, the ends are defined, and the position is announced | Browse to both ends | Works, counter announced | Required | Automatable | Critical |
| GAL-03 | Accessibility | Always | Each item has an alternative and a caption that fits | Inspect items, use long captions | Alternative present, caption wraps | Required | Automatable | Important |
| GAL-04 | Keyboard | Zoom and pan | Zoom and pan have keyboard alternatives, a reset, and do not break closing | Zoom, pan, reset, close | All by keyboard, reset works | If applicable | Automatable | Important |
| GAL-05 | States | Always | Adjacent images preload, with loading and failure states per image | Browse on a slow network, block an image | Loading shown, failure handled, no blank view | Required | Automatable | Critical |
| GAL-06 | Functional | Thumbnail strip | A thumbnail strip marks the current item and scrolls it into view | Browse far along | Current visible and marked | If applicable | Automatable | Important |
| GAL-07 | Functional | Touch gestures | Swipe has control equivalents and does not conflict with page gestures | Use a touch device | Both work | If applicable | Manual | Important |
| GAL-08 | Functional | Deep links | A deep link opens a specific item, and the back action closes the lightbox | Open a link, press back | Correct item, back closes | If applicable | Automatable | Important |
| GAL-09 | Layout | Always | Tall, wide and small images fit the viewport, including on rotation and resize | Use extreme aspect ratios, rotate | Fully visible, not cropped without control | Required | Manual | Important |
| GAL-10 | Functional | Mixed media | Video items pause when navigating away from them | Browse away from a playing video | It pauses | If applicable | Automatable | Important |
| GAL-11 | Functional | Always | The page behind is inert and does not scroll | Interact with the page behind | Inert and locked | Required | Automatable | Important |
| GAL-12 | Accessibility | Actions | Download and share actions are named | Inspect names | Names say what and for which image | Optional | Automatable | Nice-to-have |
| GAL-13 | States | Always | An empty gallery and a single image are handled | Render 0 and 1 items | Meaningful state, controls hidden | Required | Automatable | Important |
| GAL-14 | Layout | Always | Thumbnails keep their aspect ratios and order, and load lazily | Use mixed aspect ratios | Tidy grid, logical reading order | Required | Automatable | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
