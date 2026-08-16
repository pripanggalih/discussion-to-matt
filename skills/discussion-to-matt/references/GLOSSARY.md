# Glossary

The vocabulary `SKILL.md` runs on. **Bold terms** inside a definition are themselves defined here; find them by their heading.

## foundation

The durable layer: what stays true across every feature of the project. Lives in `docs/foundation/`.

The glossary and the ADRs are *not* part of it — `/domain-modeling` owns those and writes them during the grilling session.

_Avoid_: docs, blueprint, constitution, base docs.

## charter

The remit of a single foundation file: what it may hold, and what belongs to a neighbour. Charters are what stop the foundation collapsing into one undifferentiated design doc, so each fact has exactly one home and changing it is a one-place edit.

Full table in [FOUNDATION-VS-SPEC.md](FOUNDATION-VS-SPEC.md).

_Avoid_: scope, remit, boundary, purpose.

## seam

The public boundary a test observes behaviour through, without reaching inside. `/tdd` forbids writing a test at a seam the user has not confirmed, and `/to-spec` prefers an existing seam to a new one and the highest available seam to a lower one — the ideal count across a codebase is one.

_Avoid_: boundary, interface, test point, integration point.

## seam registry

`SEAMS.md`: the durable inventory of the project's seams. It exists because "prefer existing seams, keep their number low" is unenforceable without a list — a session without one invents seams blind and the count creeps.

_Avoid_: seam list, seam inventory, test map.

## run sheet

One file per roadmap line, holding the ordered commands that take that feature from grounded conversation to merged code.

A run sheet is not a prompt. Every skill it names is user-invoked, so nothing triggers itself from a natural-language opener — the sheet tells *you* what to type. It is also **stateless**: progress and **depth** live only in `ROADMAP.md`, so a sheet never records having been run.

What it *does* carry, outside its briefing, is instruction: the **promotion** block the opening agent acts on, and — on the first UI sheet only — the design-system setup commands. Neither is a restatement of anything, which is why neither can drift.

_Avoid_: kickoff prompt, playbook, checklist, recipe.

## stateless

Of a run sheet: carrying no record of its own execution or its own **depth**. A checkbox in a run sheet is a second place progress lives, and the two disagree the first time one is updated alone. A depth field is the same failure wearing another name — which is why depth is a column in `ROADMAP.md` and the sheet says it only by whether its detailed sections are there.

_Avoid_: read-only, immutable, static.

## depth

How much of a run sheet has been written: `brief` or `detailed`. A brief holds intent, scope, anchors, read-first and open questions — enough to judge order and dependency, and no more, because no more is knowable yet. Detailed adds flows, edge cases and data effects, written against code that exists.

Recorded once, in `ROADMAP.md`' Depth column. Exactly one line may sit at `detailed`: two means someone is planning ahead.

_Avoid_: level, stage, maturity, fidelity.

## promotion

Deepening a run sheet from `brief` to `detailed` against the code as it now stands. It happens at the *start* of the session that will build the feature, not the end of the one before, because that is the moment the code is most current — and because the user has already done the only thing it needs, which is attach the sheet.

Promotion is the agent's work, like every other document change in this skill. The user answers questions; they never edit a file.

_Avoid_: expansion, deepening, upgrade, refinement.

## anchor

A foundation element named explicitly in a run sheet because it bears on that feature — an entity, a seam, a screen, a reuse target, the architecture.

Anchors do the work links cannot. A link tells the agent where to look; an anchor tells it which part matters, and repeating the same name across run sheet, glossary and spec is what keeps one vocabulary running through the project.

_Avoid_: reference, context, pointer, touchpoint.

## frontier

The set of items whose prerequisites are all settled — the ones that can be worked *now*, without guessing at outcomes not yet known.

In `/grilling` those items are decisions: the questions answerable this round, asked as one numbered batch with a recommendation each, after which the answers reshape the tree and the frontier moves outward. In `/to-tickets` they are tickets: those whose blocking edges are all closed.

_Avoid_: next up, ready set, unblocked list, queue.

## walking skeleton

The first roadmap item on a greenfield project: setup plus one thin slice running end to end through every layer the project has. Thin enough to build fast, complete enough to prove the stack choice before any feature is built on top of it.

_Avoid_: MVP, spike, proof of concept, hello world.

## lazily

Of a file: created only once there is something real to put in it. An empty section is an open invitation for the next session to fill it with plausible noise, which then reads as a decision nobody made.

_Avoid_: on demand, as needed, optionally, conditionally.
