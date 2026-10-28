# Contributing

## What belongs here

Generic, framework-agnostic references that say what a UI component must support and how to verify it.

Out of scope: project-specific content (naming conventions, test framework setup, Playwright or Testing Library config, design tokens, selectors) and implementation code. These belong in each project's own agent instructions.

## Repository layout

```
skills/
  <skill-name>/
    SKILL.md            router, frontmatter with name and description
    references/
      <component>.md    one file per component
docs/
  catalog.md            component catalog, priorities, writing order
```

One folder per skill under `skills/`. Split skills by when an agent needs the information, not by taxonomy. Testing is not a separate skill: each reference holds its own test cases.

## Core writing principle: capabilities, not mechanisms

State what must exist and what is observable afterwards. Never state how a given library achieves it.

- Describe intent and end state, not UI steps. Not "click the clear icon", but "trigger the reset action" and "no value is selected, the placeholder is shown, the form value is empty".
- Use neutral verbs: open, close, select an option, trigger the reset action, move focus. Avoid "click", icon names, selectors and component names.
- Expected results must be verifiable without knowing the implementation: final state, form value, focus position, announcements.
- If a library does not provide a capability, the reference only says it must exist.

## Writing a reference

1. Copy `skills/ui-component-specs/references/_template.md` to `references/<component>.md`.
2. Keep the nine sections in order.
3. Give every capability an ID with the component prefix from `docs/catalog.md` (for example `DD-07`). Every testable ID has at least one test case in section 8.
4. Set **Applies when**, **Obligation**, **Owner**, **Verification** and **Priority** on every row.
5. Draft from the sources below, then review manually.
6. Add the component to the alphabetical index in `SKILL.md` with its status. A variant of an existing component is added as rows in its parent reference, plus one index row that points to it.

### Obligation levels

- **Required**: every instance of the component.
- **If applicable**: depends on the variant.
- **Optional**: enhancements.

### Status values

`draft`, `stable`, `deprecated`, set in the reference frontmatter and in the `SKILL.md` index.

## Sources

W3C ARIA Authoring Practices Guide, Open UI, React Aria, Radix, Headless UI, GOV.UK Design System, Baymard Institute, Nielsen Norman Group, Component.gallery, WCAG 2.2, Deque axe rules, Inclusive Components, and articles by Adrian Roselli and Sara Soueidan.

## Growing the catalog

Every missed edge case found in practice gets added: a new ID, a capability row and a test case.

## Before publishing

Test each reference on a real task (for example "build a dropdown") and confirm the agent follows the edge cases.
