# Depth and drift

Read before writing any run sheet. It governs *when* a fact gets written, which is a different question from *where* — that one belongs to [FOUNDATION-VS-SPEC.md](FOUNDATION-VS-SPEC.md).

## Why timing needs its own rule

This skill has a downstream pipeline, and that pipeline is a real safety net for one failure: it stops the foundation swallowing the spec, because `/to-spec` and `/to-tickets` will derive those anyway. The anti-drift rules already cover it.

It is no safety net at all for the other failure. A run sheet written today for roadmap line 07 describes a codebase that will not exist for six sessions. Nothing downstream corrects it, because `/to-spec` reads that sheet's briefing **as settled fact** — the briefing is what the grilling session is handed, and a guess handed to that session is indistinguishable from a decision.

So the foundation is bounded by charter, and the run sheets are bounded by depth.

## The two axes

Every candidate sentence sits somewhere on two axes. Both have a hard boundary.

### Axis 1 — durability: is this still true in three features' time?

| Durable → write it now | Volatile → leave it to the session that needs it |
| --- | --- |
| The stack and its versions | Which library call an endpoint uses |
| Entities and their relationships | One screen's exact field list |
| Naming and file conventions | One module's internal helper names |
| Definition of done, the quality gates | One feature's specific test cases |
| A seam and its height | Which seams one feature tests |
| A decision and its trade-off | The order in which files get edited |

### Axis 2 — the what/how cut line

The foundation and its run sheets state **what must be true when the work is done**. Neither states **how to get there**.

**In bounds:** goals, scope, non-goals, invariants, states and transitions, constraints, quality gates, the shape and meaning of an interface.

**Out of bounds:** ordered implementation steps, task breakdowns, function and variable names, code and pseudocode, file-by-file edit lists, effort estimates and timelines.

The reliable tell: if a sentence would need rewriting because the agent chose a different but equally valid implementation, it is out of bounds.

## The depth ladder

Every roadmap line has a **depth**, recorded in the Depth column of `ROADMAP.md` and nowhere else. A run sheet is **stateless** — it never carries a field announcing its own depth, because the presence or absence of its detailed sections already says so, and a field can disagree with the sections while a section cannot disagree with itself.

### `brief` — every line, from the moment the roadmap is approved

Intent, scope, anchors, open questions, read-first. This is what [RUN-SHEET-FORMAT.md](../assets/RUN-SHEET-FORMAT.md) calls the briefing, and it is short on purpose: enough to judge order, dependency and scope, and nothing more, because nothing more is knowable yet.

### `detailed` — only the line about to be built

Adds flows and scenarios including the unhappy paths, edge cases with the behaviour each one requires, and data effects — which entities are read, written or invalidated, and which constraints from `DATA-MODEL.md` the feature must uphold.

It adds **no acceptance criteria and no contracts**. Both have owners downstream: `/to-spec` writes the user stories and the implementation decisions, `/to-tickets` writes the acceptance criteria. A copy here is the second derivation the anti-drift rules exist to prevent. Flows, edge cases and data effects have no such owner — they are material `/to-spec` derives *from*, which is why writing them sharpens the session rather than competing with it.

Still no implementation steps. `detailed` deepens what must be true, never how.

### Exactly one at a time

Only one roadmap line may sit at `detailed`. Two means someone is planning ahead against code that does not exist, which is the failure this whole file prevents.

## Promotion is the agent's job, at the start of the session

Detail written against real code is right; detail written against an imagined future is a guess that has to be unlearned. So promotion happens at the latest possible moment — when the session that will build the feature opens, not when the previous one closes.

The mechanism costs the user nothing. Opening a run sheet is already an action they take; the sheet's promotion block tells the agent to read the code as it now stands, deepen this sheet from brief to detailed, reconcile any foundation drift, and move the Depth column. The user reviews decisions in chat, and never edits a document.

This is also why the previous session's *On finishing* is short. Anything that needs comparing code against the foundation waits for the next session, which is reading the code anyway. Only what lives solely in the closing session's context — the seams it confirmed, the components it produced — must be written before that context is gone.

## Placeholders are forbidden

"TBD" in a foundation document is worse than an omission, because an agent reads a document as settled fact and a human skims past the marker.

An unknown takes one of two forms:

- **It blocks a roadmap line.** It becomes an ADR with `Status: open`, stating what is not known, the options on the table, and which line it blocks. Raise it during the grilling session; `/domain-modeling` writes it, in its own format, in the layout `docs/agents/domain.md` names. A blocking unknown almost always passes that skill's three tests — hard to reverse, surprising without context, a real trade-off — because a decision that holds up a feature is rarely trivial.
- **It blocks nothing.** It stays an open question in `ARCHITECTURE.md`, written as a question with the constraint that will settle it. That file is the only place in the foundation where "not yet known" may appear.

## The stack lives in exactly two places

The table in `ARCHITECTURE.md`, and the ADR that governs it. Never transcribed into a run sheet — a sheet links `ARCHITECTURE.md` instead. Every copy is a place a version number goes stale on its own.

Never hardcode a stack the user did not choose or the repo does not contain.

## The inclusion test for documents

**Will this file be reopened while writing code?**

- Yes, regularly → it earns a file of its own.
- Yes, but rarely, and it is small → fold it into the nearest file whose charter covers it.
- No → cut it. A document written, read once and archived is a cost with no return.

This is why conditional files are born **lazily**: `DATA-MODEL.md` only once there is data, `SEAMS.md` only once there is a seam.
