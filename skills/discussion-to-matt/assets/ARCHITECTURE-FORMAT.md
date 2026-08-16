# Architecture

The durable technical shape of the project. A choice that is hard to reverse, surprising, *and* the result of a real trade-off gets an ADR — this file describes the shape and links it. Everything else that is simply true about the stack is recorded here and nowhere else.

Greenfield: this file instructs the pipeline to **scaffold**. Brownfield: it records what already exists and instructs the pipeline to **extend**.

## Stack

Language, runtime, framework, package manager, database, ORM, auth, test runner — each with its version. Brownfield: read every version from the repo. Never write a version you have not seen.

| Concern | Choice | Version | Notes |
| --- | --- | --- | --- |

## Structure

Where code lives and why the boundaries fall where they do. Name the modules and what each one owns.

Aim for **deep modules** — a lot of behaviour behind a small interface. A module whose interface is nearly as wide as its implementation is not earning its boundary.

## Non-functional requirements

Only the ones that will actually change a design decision: expected scale, latency budget, offline behaviour, data residency, security posture. An NFR nobody will ever check is noise — cut it.

## Scaffold / extend instruction

One paragraph the pipeline can act on. Greenfield: what to generate and in what order. Brownfield: which existing patterns to follow and what must not be disturbed.

## Open questions

Decisions the foundation session could not settle **and that block no roadmap line**, written as questions with the constraint that will settle them. This is the only place in the foundation where "not yet known" is allowed to appear.

An unknown that *does* block a roadmap line does not belong here. It becomes an ADR with `Status: open`, naming what is not known, the options on the table, and the line it holds up — raised during the grilling session and written by `/domain-modeling`, in the layout `docs/agents/domain.md` gives. A blocking unknown almost always passes that skill's three tests, because a decision that stalls a feature is rarely trivial. Link it from *Decision records* below. See [DEPTH-AND-DRIFT.md](../references/DEPTH-AND-DRIFT.md).

## Decision records

Link each ADR that governs this architecture, one line each on what it decided.
