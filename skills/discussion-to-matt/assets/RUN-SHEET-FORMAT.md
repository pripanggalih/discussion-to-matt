# NN — <feature>

> Roadmap line NN · **UI** or **no UI**. Open a fresh session at the project root and run:
>
> ```
> /grill-with-docs @docs/foundation/run-sheets/NN-<slug>.md
> ```
>
> Nothing to copy, nothing to read first. The sheet tells the session what to do with itself.

A sheet has three parts and no others: the two agent-facing sections below, the **briefing**, and — on a **UI** sheet only — the design passes. The build chain is not one of them: `/grill-with-docs → /to-spec → /to-tickets → /implement` is identical on every sheet, the user knows it by heart, and an instruction repeated on every sheet is one they learn to skip past — taking the sheet's real content with it.

The whole file reaches the session as an attachment, so ordering is the sheet's job, not the user's: *Before grilling* runs first, the briefing is the material, everything else waits for its moment and says so. One rule binds what may live outside the briefing — **no second copy of the intent, the scope or the anchors**. That is the drift the briefing exists to prevent, and it is the only thing that can drift, because everything else here is an instruction rather than a restatement.

A sheet is **stateless**: it records no depth field and no progress. `ROADMAP.md` holds both.

## Before grilling

**Agent-facing, and the first thing to act on.** The user attached this file and typed nothing else; treat these steps as the opening instruction. Run them before the first question, and run them silently — the user is not asked to confirm document maintenance.

1. **Promote this sheet, if `ROADMAP.md` has this line at `brief`.** Read the code as it now stands — the packages this feature touches, the modules named in the anchors — then write the detailed sections below from what is actually there. Move this line's Depth to `detailed` and confirm no other line is still marked so.
2. **Reconcile foundation drift.** The previous feature left `ROADMAP.md` ticked and any new seam recorded, but nothing that needed comparing code against the foundation. You are reading the code anyway, so do it now: does `ARCHITECTURE.md` still describe this stack, does `CONVENTIONS.md`' reuse inventory still cite files that exist, does `DATA-MODEL.md` still match the schema? Patch what has moved. Anything that changed a project-wide decision is an ADR — raise it, and let `/domain-modeling` write it.
3. **Say what you changed, in two lines.** Then start grilling.

## Design system setup

**First UI sheet only.** Delete this section from every other sheet, and from every **no UI** sheet. It is one-time project setup, and a repeated instruction is one the user learns to skip.

This project has no `DESIGN.md` yet. Impeccable's `init` writes product truth and never visual direction, so the design system is born here, with the first interface:

```
npx impeccable install
/impeccable hooks on
/impeccable shape <feature>
```

`hooks on` wires the design detector into every edit for the life of the project — once, here. `shape` runs its own discovery interview and settles the visual world before any code is written.

## Briefing

Everything the grilling session needs, and the only part of this file that is *fact* rather than instruction. `/to-spec` later reads it as settled.

The detailed half exists only once this line is at `detailed` in `ROADMAP.md`. While it is a `brief`, delete that half entirely rather than leaving empty headings.

### Intent

What this feature makes possible and why it is worth building, in two or three sentences. Enough that the grilling session opens with the point rather than deriving it.

### Scope

**In:** the capabilities this feature delivers.

**Out:** what is deliberately excluded, and where it goes instead — a later roadmap line, or nowhere.

### Read first

Only what this feature needs. An agent that opens five irrelevant documents anchors on the wrong things.

- `docs/foundation/ARCHITECTURE.md` — stack and the scaffold/extend instruction
- `docs/foundation/CONVENTIONS.md` — reuse inventory and definition of done
- `docs/foundation/DATA-MODEL.md` — only if this feature touches data
- `docs/foundation/SEAMS.md` — only if a seam applies
- `DESIGN.md` — only if this feature has UI
- `docs/adr/<NNNN>-<slug>.md` — only where a specific ADR governs this feature

### Anchors

- **Conventions:** `<reuse target>`, `<pattern>`
- **Design:** `<component>`, `<named rule>`
- **Entities:** `<Entity>`, `<Entity>`
- **Seams:** `<seam>`. Prefer these; propose a new one only if none can serve.

### Open questions

The gaps left deliberately, for this session to close.

### Guardrail

The stack, architecture, conventions and domain language are settled in `docs/foundation/` and the glossary; the design direction, tokens and named rules are settled in `DESIGN.md` and `PRODUCT.md`. Do not re-litigate any of them. Grill only the open questions above, then continue.

<!-- ================= detailed only — delete this whole half while this line is a brief ================= -->

### Flows

The paths through this feature, happy and unhappy. What the user or caller does, and what must result. Behaviour, never implementation.

#### <Flow name>

1. <trigger or input>
2. <what must happen>
3. <observable outcome>

**When it goes wrong:** what the system must do, and which existing error state applies.

### Edge cases

- <case> → <required behaviour>

### Data effects

Which entities are created, read, updated or invalidated, and which constraints from `DATA-MODEL.md` this feature must uphold. Delete if the feature touches no data.

- **<Entity>:** created | read | updated | deleted — under what condition
- **Upholds:** <constraint from DATA-MODEL.md>

### Resolved questions

Each open question above, with its answer. Anything that turned out to be project-wide is an ADR instead — name it here and let `/domain-modeling` write it.
Filling the briefing:

- **Anchors are named, not linked.** Name the entities, seams, screens and reuse targets **by name**; the read-first list carries the paths. Naming them carries one vocabulary from here into the glossary and into the spec, and tells the agent which part of a long file matters. Never copy a file's content into the briefing.
- **Architecture and Conventions are always in the read-first list** — nothing downstream reads either file on its own. Drop `DESIGN.md` on a **no UI** sheet, and drop the entity and seam lines when the project has no data layer or no seam yet.
- **The detailed half adds no acceptance criteria and no contracts.** `/to-spec` writes the user stories, the implementation decisions and the testing decisions; `/to-tickets` writes the acceptance criteria and the blocking edges. Writing either here creates the second derivation the anti-drift rules exist to prevent.

  Flows, edge cases and data effects are the exception because nothing downstream owns them — they are *input* to `/to-spec`, the recon a session would otherwise have to do from scratch with a colder read of the code. Keep them at that level: what must happen and what must not, in the domain's own words. The moment one reads like a user story or an acceptance criterion, it has crossed into `/to-spec`'s work and belongs there instead.
- **Open questions earn their place.** Seeding known-unknowns is the point: a question here is worth more than a guess that reads like a decision. Delete the whole section if there are none; never leave a numbered blank.
- **No placeholders survive.** Every `<angle-bracket>` above is scaffolding and must be replaced or its line removed.
- **No implementation steps, at either depth.** Not an ordered edit list, not a function name, not pseudocode.

---

## Design passes

**UI sheets only.** Delete this section from every **no UI** sheet, which then carries no commands at all. These earn their place where the build chain does not: they are UI-only, they sit either side of the chain rather than in it, and the cost of forgetting one is a design system that rots quietly.

```
/impeccable shape <feature>       before /to-spec
```

Plans the UX before any code. Its output feeds the spec — it does not replace it.

```
/impeccable critique <feature>    after the last ticket, before merge
/impeccable audit <feature>
/impeccable polish <feature>
```

`critique` reviews hierarchy and clarity, `audit` covers accessibility, performance and responsiveness, `polish` aligns to the design system and checks shipping readiness. These are design passes — `/code-review` already covered standards and spec compliance per ticket.

Nothing to run during `/implement`: on a UI ticket the Impeccable detector hook fires on every edit.

## On finishing

Only what would be lost when this session's context goes. Everything that needs code compared against the foundation waits for the next sheet's *Before grilling*, which is reading the code anyway.

- Tick line NN in `docs/foundation/ROADMAP.md`.
- Record any seam this feature introduced in `SEAMS.md` — it should already be there from when the user confirmed it. Create the file if this was the first.
- If the feature added a reusable component, run `/impeccable extract` so it lands in `DESIGN.md` rather than only in the codebase.

Leave this sheet unchanged.
