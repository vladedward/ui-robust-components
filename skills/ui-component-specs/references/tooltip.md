---
component: Tooltip
id-prefix: TIP
status: draft
---

# Tooltip

## 1. When to use it vs alternatives

- **Tooltip**: a short, non-essential text hint for a control or term, shown on hover and keyboard focus.
- **Visible text or helper text**: anything the user needs to complete a task. Never put essential information only in a tooltip.
- **Popover** (`POP`): interactive or longer content, opened on activation.
- **Accessible name**: an icon-only control needs a name regardless of any tooltip.

## 2. Anatomy and variants

Parts: trigger, tooltip text, optional arrow.

Variants that change which capabilities apply:

- Text label for an icon-only control vs supplementary description
- Trigger enabled vs disabled
- Pointer, keyboard and touch devices

## 3. States

Hidden, delayed (pending show), visible, dismissed, trigger disabled.

## 4. Behavior and keyboard interaction

The tooltip shows when the trigger is hovered or focused after a short delay, and hides when both hover and focus are gone.

| Key | Result |
|---|---|
| Tab | Focusing the trigger shows the tooltip |
| Escape | Hides the tooltip without moving focus |

## 5. Component-specific accessibility

- The trigger is linked to the tooltip text as its description (or name for icon-only controls).
- The tooltip is dismissible, hoverable and persistent as required by WCAG 1.4.13.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| TIP-01 | The tooltip shows on pointer hover and on keyboard focus | Always | Required | Usually provided by primitives |
| TIP-02 | It can be dismissed without moving the pointer or focus | Always | Required | Usually provided by primitives |
| TIP-03 | The pointer can move onto the tooltip without it disappearing | Always | Required | Usually provided by primitives |
| TIP-04 | It stays visible until the user dismisses it or leaves both trigger and tooltip | Always | Required | Usually provided by primitives |
| TIP-05 | A short show delay avoids flicker; hiding is quick; moving between adjacent triggers is smooth | Always | Required | Usually provided by primitives |
| TIP-06 | It is exposed as the description or the name of the trigger | Always | Required | Usually provided by primitives |
| TIP-07 | No essential information or interactive content exists only in the tooltip | Always | Required | Application's job |
| TIP-08 | Touch devices have an alternative or do not depend on the tooltip | Touch support | Required | Application's job |
| TIP-09 | A disabled trigger still gives access to the explanation | Disabled trigger | If applicable | Application's job |
| TIP-10 | It is positioned within the viewport and not clipped, flipping when needed | Always | Required | Application's job |
| TIP-11 | Long text wraps with a maximum width | Always | Required | Application's job |
| TIP-12 | Only one tooltip is visible at a time | Always | Required | Usually provided by primitives |
| TIP-13 | An icon-only control has an accessible name that does not depend on the tooltip | Icon-only trigger | If applicable | Application's job |
| TIP-14 | The tooltip hides when the trigger is removed, scrolled away or the page changes | Always | Required | Application's job |
| TIP-15 | Contrast, zoom, right-to-left layout and reduced motion are respected | Always | Required | Application's job |

## 7. Anti-patterns

- Essential instructions or error messages only in a tooltip.
- Tooltip on hover only, unreachable by keyboard.
- Tooltip that disappears when the pointer moves onto it.
- Links or buttons inside a tooltip.
- Tooltip as the only name of an icon-only button.
- Tooltip on a disabled button that never shows.
- Tooltips left on screen after the trigger is gone.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| TIP-01 | Functional | Always | Show on hover and focus | Hover the trigger, then leave, then focus it with the keyboard | Tooltip appears for each, hides when both are gone | Required | Automatable | Critical |
| TIP-02 | Keyboard | Always | Dismissal | Show the tooltip, press Escape | It hides, focus and pointer unchanged | Required | Automatable | Critical |
| TIP-03 | Functional | Always | Hoverable | Move the pointer from the trigger onto the tooltip | It stays visible | Required | Automatable | Important |
| TIP-04 | Functional | Always | Persistence | Keep hover and focus in place for a while | It stays until dismissed or both are gone | Required | Automatable | Important |
| TIP-05 | Functional | Always | Delay | Move quickly across several triggers | No flicker, no stale tooltips | Required | Automatable | Nice-to-have |
| TIP-06 | Accessibility | Always | Exposed text | Focus the trigger with a screen reader | Tooltip text announced as description or name | Required | Manual | Critical |
| TIP-07 | Accessibility | Always | No essential content | Review all tooltip texts | Nothing needed to complete the task is only there | Required | Manual | Critical |
| TIP-08 | Functional | Touch support | Touch | Use a real touch device | An alternative exists or nothing depends on the tooltip | Required | Manual | Important |
| TIP-09 | States | Disabled trigger | Disabled trigger | Hover and focus a disabled control | The explanation is still reachable | If applicable | Automatable | Important |
| TIP-10 | Layout | Always | Positioning | Show tooltips at each viewport edge and inside a clipping container | Fully visible, flips when needed | Required | Automatable | Important |
| TIP-11 | Layout | Always | Long text | Use a very long text | Wraps within a maximum width | Required | Automatable | Nice-to-have |
| TIP-12 | Functional | Always | Single tooltip | Move focus and hover across triggers | Only one tooltip visible | Required | Automatable | Important |
| TIP-13 | Accessibility | Icon-only trigger | Name independent of tooltip | Check the name with tooltips disabled | Control still has a meaningful name | If applicable | Automatable | Critical |
| TIP-14 | Functional | Always | Cleanup | Remove the trigger, scroll it away, change the page while shown | Tooltip hides, nothing lingers | Required | Automatable | Important |
| TIP-15 | Layout | Always | Contrast, zoom, direction, motion | Check contrast, zoom to 200%, right-to-left, reduced motion | Readable, positioned, animation reduced | Required | Manual | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
