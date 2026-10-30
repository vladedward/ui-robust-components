---
component: Empty state and error state
id-prefix: EMP
status: draft
---

# Empty state and error state

> Used by lists, tables, dropdowns, search and dashboards. Component-specific empty messages (for example the dropdown "no options") are in those references; this one defines the shared behavior.

## 1. When to use it vs alternatives

- **Empty state**: a region that has nothing to show yet, or nothing that matches.
- **Error state**: a region that could not load or failed.
- **Alert** (`ALR`): a message about the page that sits above content that is still shown.
- **Loading indicator** (`PRG`): while the answer is not known yet.

## 2. Anatomy and variants

Parts: message, optional illustration, optional explanation, optional primary action, optional secondary action.

Kinds that need different content:

- First use (nothing created yet)
- No results (a search or filter matched nothing)
- Cleared or completed (nothing left to do)
- No permission
- Not found
- Error (failed to load), including partial failure
- Offline

## 3. States

Per kind as above. In every case: not shown while loading.

## 4. Behavior and keyboard interaction

The state replaces the content in the same region. Its action is reachable by keyboard. When the user's own action empties the region, focus is placed deliberately.

## 5. Component-specific accessibility

- The message is text, and illustrations are decorative.
- A change to the empty state is announced when it follows a user action.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| EMP-01 | Each kind has its own message: first use, no results, error, no permission, not found are never the same | Always | Required | Application's job |
| EMP-02 | The message says why and offers a next step where there is one | Always | Required | Application's job |
| EMP-03 | The action works by keyboard, and focus is placed deliberately after the user empties the region | Always | Required | Application's job |
| EMP-04 | A partial failure shows what loaded together with an error and retry for the part that failed | Several data sources | If applicable | Application's job |
| EMP-05 | Retry keeps the user's context, shows loading, and avoids loops with automatic repeats | Error state | If applicable | Application's job |
| EMP-06 | The empty state is not shown while data is loading | Async data | Required | Application's job |
| EMP-07 | A change to the empty state caused by the user is announced | Content removed by user | Required | Application's job |
| EMP-08 | Illustrations are decorative and do not carry meaning | Illustration present | Required | Application's job |
| EMP-09 | Loss of connection is shown with what still works and what is retried | Offline | If applicable | Application's job |
| EMP-10 | Long and translated messages fit | Always | Required | Application's job |

## 7. Anti-patterns

- "No data" with no cause and no next step.
- The same message for no results and for a failed request.
- Flashing the empty state before the data arrives.
- Replacing partly valid content with one error for everything.
- Focus lost when the last item is removed.
- A retry button that triggers a request storm.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| EMP-01 | States | Always | Distinct kinds | Produce each kind | Different, accurate messages | Required | Automatable | Critical |
| EMP-02 | States | Always | Cause and next step | Review each message | States why and offers an action where relevant | Required | Manual | Important |
| EMP-03 | Keyboard | Always | Action and focus | Use the action by keyboard, remove the last item | Action works, focus placed deliberately | Required | Automatable | Critical |
| EMP-04 | Data | Several data sources | Partial failure | Fail one source of several | Loaded part shown, failed part has error and retry | If applicable | Automatable | Critical |
| EMP-05 | Data | Error state | Retry | Retry successfully and unsuccessfully, repeatedly | Context kept, loading shown, no loop | If applicable | Automatable | Important |
| EMP-06 | States | Async data | Not while loading | Load slowly | Loading shown first, never the empty state | Required | Automatable | Critical |
| EMP-07 | Accessibility | Content removed by user | Announcement | Remove the last item with a screen reader | New state announced | Required | Manual | Important |
| EMP-08 | Accessibility | Illustration present | Decorative image | Inspect the illustration | Hidden from assistive technology | Required | Automatable | Nice-to-have |
| EMP-09 | States | Offline | Offline | Go offline and back | State shown, recovery handled | If applicable | Automatable | Important |
| EMP-10 | Layout | Always | Long messages | Use a longer language and narrow viewport | Fits | Required | Automatable | Nice-to-have |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
