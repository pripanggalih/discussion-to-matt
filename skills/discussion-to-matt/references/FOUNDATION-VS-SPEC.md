# Charters: foundation vs. spec

Read before writing the foundation. The self-review at the bottom is the one `SKILL.md` sends you back for once the files are written.

This file answers **where** a fact goes. [DEPTH-AND-DRIFT.md](DEPTH-AND-DRIFT.md) answers **when** it may be written. Both bind.

## The test

A fact belongs to the **foundation** if it stays true across features. It belongs to a spec if the feature that needs it settles it once and never revisits it.

Not importance — *lifetime*. "Postgres, via Drizzle" is foundation. "The booking form rejects a check-out before check-in" is spec, and no less important for that.

## Per-file charter

*(lazy)* marks a file written only when the project earns it; absent is correct, empty is not.

| File | Holds | Never holds |
| --- | --- | --- |
| `PRODUCT.md` *(root, shared)* | Problem, v1 scope, project non-goals, success measure — appended below Impeccable's design brief | Feature requirements, user stories, design anti-references, a second copy of the stack |
| `ARCHITECTURE.md` | Stack with versions, module structure, NFRs, scaffold/extend instruction, non-blocking open questions, links to the governing ADRs | Feature designs, file paths, code |
| `CONVENTIONS.md` | Reuse inventory, naming and style beyond what tooling enforces, file layout, testing conventions, definition of done | Testing philosophy (`/tdd` owns it), tracker config (`docs/agents/`), anything visual (`DESIGN.md`) |
| `DATA-MODEL.md` *(lazy)* | Entities, fields, lifecycle, relationships, constraints, ERD, deliberate omissions | What a term *means* — the glossary owns that |
| `SEAMS.md` *(lazy)* | The seam inventory, height, prior art, rejected boundaries | Which seams a given feature tests |
| `ROADMAP.md` | Ordered features, dependencies, depth, checkbox status, deferred ideas | Tickets, estimates, feature detail |
| `run-sheets/NN-*.md` | Intent, scope, anchors, read-first, open questions, the command sequence — plus flows, edge cases and data effects once promoted | Spec, tickets, acceptance criteria, contracts, plan, progress state, its own depth |

Written by others and only pointed at: the glossary and ADRs (`/domain-modeling`), `DESIGN.md` and the design half of `PRODUCT.md` (`/impeccable`), `docs/agents/` (`/setup-matt-pocock-skills`).

**`PRODUCT.md`, not `PRD.md`, and at the root.** In this ecosystem a PRD *is* a spec — `/to-spec` says so outright — and `/code-review` reaches for a PRD or spec file under `docs/`, `specs/` or `.scratch/` when it finds no issue reference. Keeping the project-level file at the root, outside that namespace, removes the ambiguity entirely.

## Overlaps to watch

**`ARCHITECTURE.md` and the ADRs** both describe choices. The ADR carries the *why* — the alternatives, the trade-off. Architecture carries the *what*, and links the ADR.

**`ARCHITECTURE.md` and `PRODUCT.md`.** `/impeccable init` will ask about the stack on a project with no scaffold and record the answer under `## Stack`. The stack is Architecture's; step 1 has the user answer *delegated* so no second copy is ever born.

**`CONVENTIONS.md` and `DESIGN.md`** both list reusable things. UI components go to `DESIGN.md`, where the frontmatter is machine-readable and the detector enforces it; conventions carries one row pointing there.

**`ROADMAP.md` and the run sheets** both name features. The roadmap holds order, depth and status; the sheet holds substance. A checkbox or a depth field in a run sheet is the drift you are guarding against.

## Anti-drift rules

**No spec, no tickets, no plan.** `/to-spec` and `/to-tickets` derive those from a feature-level conversation. A version written here is derived from generalities, and when the real skill runs the two disagree with no way to tell which is authoritative. This is also why a promoted run sheet gains flows and edge cases but never acceptance criteria or contracts.

**The glossary and the ADRs are not yours.** `/domain-modeling` writes them during the grilling session, in its own formats. A copy under `docs/foundation/` diverges the first time a later session updates only the original.

**Foundation stays durable.** A foundation file describing how one feature behaves is content in the wrong place — it belongs to the spec that feature's session will produce.

**Progress lives in one file.** `ROADMAP.md` holds the checkbox and the depth. Nothing else records either.

## Self-review

Run after writing, fix inline, then gate. Fix what it turns up; do not report it to the user as a findings list.

1. **Placeholders.** Run the search, do not eyeball it:

   ```bash
   grep -rniE 'TBD|TODO|to be determined|<[a-z-]+>|\betc\.' docs/foundation/ PRODUCT.md
   ```

   Every hit is either scaffolding that must be replaced, an angle-bracket placeholder that must be filled or its line removed, or a genuine unknown — and a genuine unknown becomes an ADR with `Status: open` if it blocks a roadmap line, or an open question in `ARCHITECTURE.md` if it blocks nothing. Report the command's final state as clean; if it is not clean, you are not finished.
2. **Cross-file consistency** — entities named in `PRODUCT.md` exist in `DATA-MODEL.md`; the stack in `ARCHITECTURE.md` matches the ADRs it links, version for version; every reuse target named in a run sheet exists in the `CONVENTIONS.md` inventory; nothing appended to `PRODUCT.md` contradicts the design brief above it.
3. **Charter** — nothing in a file falls outside its remit per the table above. Move what leaked; do not copy it.
4. **Lazy files** — every conditional file that exists has real content, and none was created merely to look complete.
5. **Scope** — one coherent project, or several that need splitting? If the session produced independent subsystems with separate users and separate data, say so before the roadmap hardens it.

Three more once the roadmap and run sheets exist:

6. **Coverage** — one run sheet per roadmap line, each naming its anchors, and every sheet's read-first list including `ARCHITECTURE.md` and `CONVENTIONS.md`.
7. **Traceability** — follow each chain end to end and fix any break:

   ```
   PRODUCT.md capability  →  ROADMAP.md line  →  run sheet  →  anchors
                                                                 ↓
                                            entity / seam / reuse target that actually exists
   ```

   An orphan in either direction is a defect: a capability with no roadmap line was dropped silently, and a roadmap line with no capability behind it was invented.
8. **Depth and progress** — exactly one line at `detailed`, no run sheet carrying a depth field or a checkbox, and a resumed run preserved every box that was already ticked.

Then one last read, as someone else:

9. **The stranger test** — re-read run sheet 01 as an agent that did not witness this conversation. Could it start work without asking anything? Every question it would have to ask is either a missing section or an open question you failed to record.
