# Format: sections to add to root `PRODUCT.md`

One `PRODUCT.md`, at the repo root, with two contributors.

`/impeccable init` writes the **design brief** half: Register (brand or product), Users, Product Purpose, Brand Personality, Anti-references, Design Principles, Accessibility. Every later `/impeccable` command reads it.

This skill adds the **product scope** half — the sections below. Append them; never rewrite or reorder what is already there.

If `/impeccable init` has not run (a project with no interface), write these sections alone.

**Why the root and not `docs/`.** `/code-review` reaches for a PRD or spec file under `docs/`, `specs/` or `.scratch/` when it finds no issue reference. A project-level product file in that namespace would be mistaken for a feature spec, and one feature's diff reviewed against the whole of v1.

---

## Problem

The problem this project exists to solve, from the user's perspective. Who has it, how they cope today, and what that costs them.

If `/impeccable init` already wrote *Users*, do not restate them — reference them and stay on the problem.

## What v1 is

The scope of the first version, as capabilities rather than features. Something a user can do end to end.

## Non-goals

What this project deliberately does not do, and briefly why. Project-level only — a feature's own out-of-scope list lives in its spec.

Design anti-references are not non-goals. Those belong to Impeccable's *Anti-references* section, and duplicating them here splits one rule across two places.

## Success

How you will know v1 worked. Observable, and honest about how you would measure it.
