---
component: Search input
id-prefix: SRC
status: draft
---

# Search input

> Builds on `text-input.md`. A search that offers suggestions to pick from is a combobox (`combobox.md`).

## 1. When to use it vs alternatives

- **Search input**: free text that returns a list of results or a results page.
- **Combobox** (`CMB`): choosing a value for a field from suggestions.
- **Filters**: narrowing a visible list by known attributes.
- **Command palette** (`CMD`): searching actions.

## 2. Anatomy and variants

Parts: label or accessible name, input, submit action, optional clear action, optional suggestions or recent searches, results area.

Variants that change which capabilities apply:

- Search on submit vs search as the user types
- With vs without suggestions and recent searches
- Results on the same page vs a results page
- With the query reflected in the URL

## 3. States

Empty, typing, searching, results, no results, error, disabled.

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Enter | Runs the search |
| Escape | Clears the text where the pattern defines it, or closes the suggestions |
| ArrowDown / ArrowUp | Moves through suggestions, when present |

## 5. Component-specific accessibility

- The control is identified as a search, and has an accessible name even without visible text.
- The number of results, or the lack of results, is announced after a search.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| SRC-01 | A named search control that runs by keyboard and by its submit action | Always | Required | Application's job |
| SRC-02 | The text can be cleared in one step, and focus returns to the input | Has text | If applicable | Application's job |
| SRC-03 | Search as you type is delayed, ignores outdated responses and does not run for every keystroke | Search as you type | Required | Application's job |
| SRC-04 | No results has a message that echoes the query safely and suggests what to do | Always | Required | Application's job |
| SRC-05 | An empty or whitespace-only query is handled | Always | Required | Application's job |
| SRC-06 | Special characters, markup, very long queries and diacritics are handled and matched as defined | Always | Required | Application's job |
| SRC-07 | Suggestions and recent searches are keyboard operable, can be removed, and respect privacy | Suggestions or recent searches | If applicable | Application's job |
| SRC-08 | The result count is announced, and focus and scroll after a search are logical | Always | Required | Application's job |
| SRC-09 | The query is in the URL and is restored by reload, back and shared links | Query in the URL | If applicable | Application's job |
| SRC-10 | Loading and error states exist, with retry | Always | Required | Application's job |
| SRC-11 | On mobile the keyboard offers a search action, with the right input mode | Always | Required | Application's job |
| SRC-12 | Matching is case and diacritic tolerant as decided | Always | Required | Application's job |

## 7. Anti-patterns

- A request per keystroke with no delay or cancellation.
- Printing the raw query into the page unescaped.
- A search field with only a placeholder and no accessible name.
- "No results" with no suggestion.
- Results that replace each other out of order.
- A clear button that moves focus away.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| SRC-01 | Keyboard | Always | Run search | Search by Enter and by the submit action | Same results, control named as a search | Required | Automatable | Critical |
| SRC-02 | Functional | Has text | Clear | Trigger the clear action | Empty, focus in the input | If applicable | Automatable | Important |
| SRC-03 | Data | Search as you type | Delay and stale results | Type quickly, delay an early response | One delayed request, latest results only | Required | Automatable | Critical |
| SRC-04 | States | Always | No results | Search for text that matches nothing, including markup characters | Message shown, query displayed safely | Required | Automatable | Critical |
| SRC-05 | Validation | Always | Empty query | Search empty and with only spaces | Handled as decided, no error page | Required | Automatable | Important |
| SRC-06 | Data | Always | Special characters | Search quotes, markup, a very long string, diacritics | No error, safe, correct matching | Required | Automatable | Important |
| SRC-07 | Keyboard | Suggestions or recent searches | Suggestions and recents | Use and remove entries by keyboard | Operable, removal works | If applicable | Automatable | Important |
| SRC-08 | Accessibility | Always | Result announcement | Search with a screen reader | Count or "no results" announced, focus logical | Required | Manual | Critical |
| SRC-09 | Functional | Query in the URL | URL state | Search, reload, go back, share the link | Same query and results | If applicable | Automatable | Important |
| SRC-10 | States | Always | Loading and error | Search slowly and with a failure | Loading shown, error with retry | Required | Automatable | Important |
| SRC-11 | Functional | Always | Mobile keyboard | Use a real device | Search action key and right keyboard | Required | Manual | Nice-to-have |
| SRC-12 | Data | Always | Case and diacritics | Search in different case and without diacritics | Matches as decided | Required | Automatable | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
