---
component: Textarea
id-prefix: TXA
status: draft
---

# Textarea

> Builds on `text-input.md`. Also verify the text input capabilities that apply (label, helper and error text, validation timing, autofill, read-only vs disabled, special characters), then the ones below.

## 1. When to use it vs alternatives

- **Textarea**: multi-line or long free text (comment, description, message).
- **Text input** (`TXT`): short single-line text.
- **Rich text editor**: formatting is required. It is a different, much larger component.

## 2. Anatomy and variants

Parts: label, text area, optional helper text, optional character counter, optional error text.

Variants that change which capabilities apply:

- Fixed height vs automatic growth with content
- With vs without a character limit and counter
- User-resizable vs fixed size
- Plain text vs text with line breaks that matter downstream

## 3. States

Empty, filled, focus, disabled, read-only, error, over the limit.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Enter | Inserts a line break, never submits the form |
| Tab | Moves focus out of the field |

If a submit shortcut exists, it uses a modifier key and is documented.

## 5. Component-specific accessibility

- The counter and the limit are available to assistive technology, but not announced on every keystroke.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| TXA-01 | Enter inserts a line break and does not submit | Always | Required | Usually provided by primitives |
| TXA-02 | Automatic growth follows the content up to a maximum height, then scrolls, and shrinks when text is removed, without layout jumps | Auto-grow | If applicable | Application's job |
| TXA-03 | Manual resizing stays within the layout and is disabled where not wanted | User-resizable | Optional | Application's job |
| TXA-04 | The counter counts consistently (line breaks, emoji), updates the remaining amount and tells the user when over the limit, with throttled announcements | Character limit | If applicable | Application's job |
| TXA-05 | The limit is enforced or flagged, including for pasted text, and nothing is lost silently | Character limit | If applicable | Application's job |
| TXA-06 | Pasting very long text and text with different line endings works | Always | Required | Application's job |
| TXA-07 | Line breaks and surrounding whitespace are preserved or normalized on submit as decided, and displayed back the same way | Always | Required | Application's job |
| TXA-08 | A very long unbroken string wraps without breaking the layout | Always | Required | Application's job |
| TXA-09 | Typed text is retained after a failed submit and on navigating back | Inside a form | Required | Application's job |
| TXA-10 | Undo and redo are not broken by automatic resizing or formatting | Always | Required | Application's job |
| TXA-11 | Composition input (IME), emoji and right-to-left text work | Always | Required | Application's job |
| TXA-12 | Required and error states, with the message associated with the field | Always | Required | Application's job |

## 7. Anti-patterns

- Enter submitting the form.
- A counter announced to a screen reader on every keystroke.
- Truncating pasted text without telling the user.
- Auto-grow that resets the scroll position or breaks undo.
- Line breaks lost when the saved text is displayed.
- Counting characters differently on the client and the server.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| TXA-01 | Keyboard | Always | Line break | Press Enter inside a form | A line break is inserted, form not submitted | Required | Automatable | Critical |
| TXA-02 | Layout | Auto-grow | Auto-grow | Type many lines, then delete them | Grows to the maximum then scrolls, shrinks back, no jump | If applicable | Automatable | Important |
| TXA-03 | Layout | User-resizable | Manual resizing | Resize by hand to extremes | Stays within the layout | Optional | Manual | Nice-to-have |
| TXA-04 | Functional | Character limit | Counter | Type to the limit and over it, include emoji and line breaks | Remaining count correct, over the limit stated, announcements not per keystroke | If applicable | Automatable | Important |
| TXA-05 | Validation | Character limit | Limit enforcement | Paste text longer than the limit | Enforced or flagged, user told, nothing lost silently | If applicable | Automatable | Critical |
| TXA-06 | Data | Always | Paste | Paste very long text and text with CRLF and LF | Content intact and responsive | Required | Automatable | Important |
| TXA-07 | Data | Always | Line breaks | Submit text with line breaks and surrounding spaces, view it back | Line breaks as decided, shown the same way | Required | Automatable | Critical |
| TXA-08 | Layout | Always | Unbroken string | Enter a very long string with no spaces | Wraps, no horizontal page overflow | Required | Automatable | Important |
| TXA-09 | Data | Inside a form | Retained text | Fail validation, then navigate back | Text still there | Required | Automatable | Critical |
| TXA-10 | Functional | Always | Undo and redo | Type, let it resize, undo and redo | History works | Required | Manual | Nice-to-have |
| TXA-11 | Data | Always | Composition and emoji | Compose with an IME, enter emoji and right-to-left text | Text preserved, caret correct | Required | Manual | Important |
| TXA-12 | Validation | Always | Required and error | Submit empty when required | Error associated with the field | Required | Automatable | Critical |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
