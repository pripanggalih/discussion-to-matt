# Conventions

How code in this repo is written, and what already exists to reuse.

This is the one foundation file the pipeline reaches through `CLAUDE.md`/`AGENTS.md` as well as through a run sheet's read-first list, because `/implement` reads nothing on its own and `/to-tickets` sizes every ticket to a single fresh context window — so nothing downstream will find this file by accident.

Repo configuration — issue tracker, triage labels, domain doc layout — is not here. That is `docs/agents/`, written by `/setup-matt-pocock-skills`. Anything visual is `DESIGN.md`, written by `/impeccable init`.

Greenfield: write only *Naming and style* and *Definition of done*, from the chosen stack's defaults. The reuse inventory and layout describe code, so they wait for the walking skeleton to produce some.

## Reuse inventory

What already exists that new work should reach for instead of rebuilding — the difference between an agent extending your codebase and one growing a parallel codebase beside it.

UI components are not listed here. `DESIGN.md` holds them, its frontmatter is machine-readable, and Impeccable's detector enforces it — a second list would go stale and be ignored. Point at `DESIGN.md` in one row and stop.

| Thing | Where | Use it for |
| --- | --- | --- |

## Naming and style

Only what a formatter and linter cannot already enforce. If Prettier or ESLint settles it, say nothing — a rule the tooling already applies is a line you pay for and never use.

## File and directory layout

Where a new module, route, component or test file goes. State the pattern, and name one existing example of it.

## Testing conventions

Test file naming and placement, the runner and how to invoke a single file, fixture and factory patterns, what gets mocked and what never does.

Testing *philosophy* — what makes a test worth keeping — is `/tdd`'s, not this file's. Record only what is specific to this repo.

## Definition of done

What must be true before work is considered complete: types pass, tests pass, lint clean, the specific quality gates this project runs. Name the exact commands.

```
# typecheck
# test (single file)
# test (full suite)
# lint
```
