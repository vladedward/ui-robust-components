---
component: Image (alt, lazy loading, errors)
id-prefix: IMG
status: draft
---

# Image (alt, lazy loading, errors)

## 1. When to use it vs alternatives

- **Image**: content or illustration shown with the page.
- **Avatar** (`AVT`): a person representation.
- **Gallery** (`GAL`): several images explored together.
- **CSS background**: decoration only, never meaningful content.

## 2. Anatomy and variants

Parts: image, text alternative, optional caption, placeholder.

Variants: informative, decorative, functional (inside a link or button), complex (chart, diagram), user uploaded vs authored, above vs below the first screen.

## 3. States

Loading, loaded, failed, placeholder, lazy not yet loaded.

## 4. Behavior and keyboard interaction

Not interactive on its own. A functional image takes the keyboard behavior of its link or button.

## 5. Component-specific accessibility

- The alternative text serves the image's purpose: describes content, names the action, or is empty when decorative.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| IMG-01 | The text alternative matches the purpose: described, empty when decorative, names the action when functional, with a long description for complex images | Always | Required | Application's job |
| IMG-02 | A failed image does not break the layout and the alternative or a fallback is visible | Always | Required | Application's job |
| IMG-03 | Dimensions or aspect ratio are reserved, so the page does not shift while images load | Always | Required | Application's job |
| IMG-04 | Below-the-fold images load lazily and the main image of the first screen loads first | Always | Required | Application's job |
| IMG-05 | Responsive sources deliver a suitable size and format, and art direction crops are right | Always | Required | Application's job |
| IMG-06 | A placeholder avoids a blank space on slow connections | Slow loading | If applicable | Application's job |
| IMG-07 | Text inside images is avoided, and when present the alternative repeats it | Images with text | Required | Application's job |
| IMG-08 | Dark mode, transparency and high contrast mode keep the image usable | Always | If applicable | Application's job |
| IMG-09 | Images do not overflow their container at 200% zoom | Always | Required | Application's job |
| IMG-10 | User uploaded images are handled: orientation data, huge sizes, odd formats, animation | Uploaded images | If applicable | Application's job |
| IMG-11 | Meaningful images are content, not CSS backgrounds | Always | Required | Application's job |
| IMG-12 | Animated images respect reduced motion and can be paused | Animated | If applicable | Application's job |

## 7. Anti-patterns

- Alt text 'image' or the file name.
- Decorative images with long descriptions.
- No width and height, causing layout shift.
- Lazy loading the main image of the first screen.
- Text baked into an image.
- A meaningful photo set as a CSS background.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| IMG-01 | Accessibility | Always | The text alternative matches the purpose: described, empty when decorative, names the action when functional, with a long description for complex images | Review each image type | Correct alternative for each purpose | Required | Manual | Critical |
| IMG-02 | States | Always | A failed image does not break the layout and the alternative or a fallback is visible | Block images | Layout intact, fallback or alt shown | Required | Automatable | Critical |
| IMG-03 | Layout | Always | Dimensions or aspect ratio are reserved, so the page does not shift while images load | Load slowly and measure layout shift | No visible shift | Required | Automatable | Critical |
| IMG-04 | Layout | Always | Below-the-fold images load lazily and the main image of the first screen loads first | Inspect loading behavior | Lazy below, prioritized above | Required | Automatable | Important |
| IMG-05 | Layout | Always | Responsive sources deliver a suitable size and format, and art direction crops are right | Test several viewport sizes and densities | Suitable source, no oversized download | Required | Automatable | Important |
| IMG-06 | States | Slow loading | A placeholder avoids a blank space on slow connections | Throttle the network | Placeholder shown | If applicable | Manual | Nice-to-have |
| IMG-07 | Accessibility | Images with text | Text inside images is avoided, and when present the alternative repeats it | Find images with text | Alternative equals the text | Required | Manual | Important |
| IMG-08 | Layout | Always | Dark mode, transparency and high contrast mode keep the image usable | Check each mode | Readable | If applicable | Manual | Nice-to-have |
| IMG-09 | Layout | Always | Images do not overflow their container at 200% zoom | Zoom and resize | Contained | Required | Automatable | Important |
| IMG-10 | Data | Uploaded images | User uploaded images are handled: orientation data, huge sizes, odd formats, animation | Use rotated, huge, animated and unusual files | Displayed correctly and efficiently | If applicable | Automatable | Critical |
| IMG-11 | Accessibility | Always | Meaningful images are content, not CSS backgrounds | Review meaningful imagery | Present as content with alternative | Required | Automatable | Important |
| IMG-12 | Accessibility | Animated | Animated images respect reduced motion and can be paused | Enable reduced motion | Static or pausable | If applicable | Manual | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
