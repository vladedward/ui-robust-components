# ui-robust-components

Agent skills (`SKILL.md` format) that tell an AI coding agent what to build, and what to test, for every common front-end element: dropdowns, form fields, dialogs, tabs, navigation and more.

When an agent is asked for a dropdown, it already knows the standard states, keyboard interaction, accessibility requirements and edge cases (empty list, very long text, async loading, a preselected value that no longer exists, focus return on Escape), without you spelling them out each time.

## Install

```sh
npx skills add vladedward/ui-robust-components
```

## Skills

| Skill | Scope | Status |
|---|---|---|
| [`ui-component-specs`](skills/ui-component-specs/SKILL.md) | One reference per component, with build requirements and test cases | Draft: 49 component references plus 17 variants folded into their parent references |
| `accessibility` | Cross-cutting accessibility rules | Planned |
| `seo` | Page-level SEO concerns | Planned |

## How it works

- Generic and framework-agnostic: references say what must exist and what is observable, never how a library achieves it.
- Progressive disclosure: the agent loads only the reference for the component it is working on.
- Every capability has an ID (for example `DD-07`) linked to a generic test case, so missing coverage is visible and an agent can be told "cover all IDs".
- Works on top of component libraries (Angular Material, shadcn, Radix, MUI): the library provides the implementation, the skill provides the checklist to verify against.

## Roadmap

The component catalog, priorities and writing order are in [`docs/catalog.md`](docs/catalog.md). Contribution rules and the reference template are in [`CONTRIBUTING.md`](CONTRIBUTING.md).

## License

MIT
