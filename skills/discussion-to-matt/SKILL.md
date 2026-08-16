---
name: discussion-to-matt
description: Establish a durable project foundation and one ordered, session-ready run sheet per feature — the layer the per-feature skills assume but never create. Run it at the start of a build, where it holds the grilling itself, or at the end of a design conversation to distil what was decided.
disable-model-invocation: true
---

Settle an open-ended design conversation into a **foundation** that governs every later feature, and an ordered set of **run sheets** that each drop you into the engineering skills already grounded.

Two ways in, one process. Called at the **start** of a build, this skill runs the design conversation itself — step 4 is a full grilling from zero. Called at the **end** of one, it opens from what that conversation settled and grills only the gaps. Either way the run ends the same: `docs/foundation/` written, and one run sheet per roadmap line.

**This skill completes the pipeline; it never stands in for a part of it.** Every engineering skill keeps its whole job. `/grill-with-docs` still holds the feature conversation, `/to-spec` still synthesises the spec, `/to-tickets`' granularity quiz is still its whole value, `/tdd` still makes the user confirm the seams, `/code-review` still reviews. What they lack is a starting position: a stack that was chosen, entities that have names, a seam registry to prefer from, and a definition of done with commands in it. That is the only gap this skill fills.

So the test for anything you are about to write is not "would this be useful downstream" — it is "does anything downstream already own this". Producing a downstream skill's output here does not save a step; it produces a second version that skill will contradict, with no way to tell which is authoritative.

Two rules bound what gets written. A fact belongs to the **foundation** if it stays true across features — [FOUNDATION-VS-SPEC.md](references/FOUNDATION-VS-SPEC.md) carries the per-file **charter** and the self-review. A fact may only be written once it can be written against something real — [DEPTH-AND-DRIFT.md](references/DEPTH-AND-DRIFT.md) carries the **depth ladder** and the promotion rule. Read both before writing anything.

**The user decides; you type.** Every document in this run is yours to write and to maintain. Put decisions to the user as questions in the chat, answerable in a word, and translate the answers into files yourself. Never ask them to review a file, edit a section, or keep a document up to date.

**Bold terms** are defined in [GLOSSARY.md](references/GLOSSARY.md).

## What this skill does not own

Three things have another owner. Write none of them; point at them.

- **The glossary and the ADRs** — `/domain-modeling` writes both, inline, during step 4.
- **`DESIGN.md`** — Impeccable's design system: tokens in YAML frontmatter, named rules, do's and don'ts. Its detector rules and its edit hook enforce what the file declares, which is why a prose copy here would be strictly worse. Note what Impeccable actually does and does not write — see step 1.
- **`docs/agents/`** — tracker, triage labels, domain doc layout, written by `/setup-matt-pocock-skills`.

## Process

### 1. Preflight

Preflight **prepares**; it does not block. Anything mechanical you run yourself, anything that needs a decision becomes a question, and anything that cannot be settled yet is recorded and carried forward.

**Repo configuration.** Read `docs/agents/issue-tracker.md` and `docs/agents/domain.md`. If either is missing, run `/setup-matt-pocock-skills` inline rather than stopping — it is prompt-driven, but its defaults are strong: the tracker is proposed from `git remote`, the domain layout defaults to single-context without asking, and the triage section is skipped entirely when the `triage` skill is not installed. In practice one or two questions, and they belong in the first round of step 4's frontier rather than in a separate interruption.

`domain.md` gives the domain doc layout, which decides where `/domain-modeling` keeps the glossary and the ADRs:

- **Single-context** — glossary at root `CONTEXT.md`, ADRs in `docs/adr/`.
- **Multi-context** — root `CONTEXT-MAP.md` pointing at a `CONTEXT.md` and `docs/adr/` under each `src/<context>/`, with system-wide decisions still in root `docs/adr/`. Each term belongs to the context that owns it, and `DATA-MODEL.md` gets one section per context.

**Product and design.** Skip this whole block for a backend, API or CLI.

Impeccable splits its work in a way that matters here, and getting it wrong costs a blocked run: `/impeccable init` captures durable product truth in root `PRODUCT.md` and **does not write `DESIGN.md`** — it is forbidden from even raising visual direction. A design system is created by a new-work request or recorded from existing code by `/impeccable document`.

So:

- **No `PRODUCT.md`** — have the user run `npx impeccable install` then `/impeccable init`. It writes the design brief half of the file this skill's step 5 appends to, and its Users and Purpose sections are good material for step 4.
- **`init` asks about the stack** when the project has no scaffold and the request implies building. The stack is `ARCHITECTURE.md`'s, and it needs the domain, entities and NFRs that only step 4 produces. Tell the user to answer **"delegated"** — Impeccable records that verbatim, which leaves the decision open for step 4 instead of pre-empting it with a thinner context.
- **Brownfield with existing UI and no `DESIGN.md`** — have them run `/impeccable document` to record the incumbent visual world before it gets extended blind.
- **Greenfield** — require nothing. The visual world is a feature-level decision; the first UI run sheet carries the instruction for it.

**Resuming.** If `docs/foundation/ROADMAP.md` already exists this is a **resumed** run. Re-read both rule files, top up any foundation file whose stack, entities or conventions no longer match the repo, and run the self-review over whatever you changed.

### 2. Orient

Preflight has passed, so the map is now accurate — nothing below is going to be retracted. Give it once, then stop.

Tell the user four things, in this order:

1. **The shape of the run** — the numbered steps below, named. Say where it ends: `docs/foundation/` written and one session-ready run sheet per feature. Say what it does not do: write code, write a spec, or open a ticket.
2. **Where they are asked to decide** — twice. Once on the foundation, before the roadmap is built; once on the roadmap order, before the run sheets are written. Both are hard stops. Both arrive as a handful of questions in the chat, answerable in a word — they are never asked to open a file.
3. **Which mode this run is in** — and what that changes:

   - **Cold start** — the conversation so far holds no design material. Nothing to distil; step 4 is the whole interview, from the problem statement up. This is the normal way in, not a degraded one.
   - **Distil** — a design conversation already ran above. Step 4 opens from what it settled and grills only what it left open, rather than re-asking what the user has already answered.
   - **Resumed** — `ROADMAP.md` existed. Say which lines are already ticked and what step 1 topped up, then continue at step 6.

4. **Whether this is a git repo**, if it is not. Ask once, here, whether to `git init` — it changes their directory permanently and fixes where the project's boundary sits, so it is theirs to decide, but it is one question and not a separate gate. On **no**, write everything as normal, skip every commit silently, and say once at the end that the foundation is uncommitted. Never reach a `git commit` that will fail.

Then wait for a go-ahead. A user who actually wanted `/to-spec` for one feature, or `/wayfinder` for work whose direction is not yet clear, finds out here at the cost of one message — rather than after a grilling session whose output does not fit.

### 3. Greenfield or brownfield

Which one you are in governs every step after.

**Greenfield** — no code. You help choose the stack, and `ARCHITECTURE.md` tells the pipeline to scaffold it. Roadmap item #1 is a **walking skeleton**. `CONVENTIONS.md` gets only its naming and definition-of-done sections, from the chosen stack's defaults; the reuse inventory and layout are filled in by the walking-skeleton run, once there is code to describe.

**Brownfield** — existing stack, scanned in **two passes**.

The **wide pass** runs here, before any roadmap exists. Its questions are structural — which modules exist, what calls what, where the boundaries fall — so reach for the codebase knowledge graph first and fall back to reading files only where it comes up empty. Cover the test setup, the two or three largest modules, and the build and lint config. Scan until every row of the reuse inventory and every seam cites a real file, and record the stack verbatim from the manifest and config — never a version you have not seen.

The **narrow pass** runs per roadmap line in step 7, once the roadmap exists and you know which packages a given feature touches. That is what makes a sheet's anchors cite real files. Attempting it here is what makes the scan circular: the roadmap it would scope itself by is four steps away.

Either way, have the user correct what you drafted — an inferred convention is worse than none, because the pipeline will follow it.

### 4. Grill the foundation

Run `/grilling`, using the `/domain-modeling` skill. Domain modeling sharpens the glossary and raises ADRs inline as terms resolve, in the layout step 1 read — which is why this skill writes neither.

Your additions are the themes and the stopping rule.

The themes, in rough dependency order: the problem and who has it; users and v1 scope; the stack; domain entities in business terms; **seams**; conventions and definition of done. Skip the entity theme when there is no data layer. Any question `/setup-matt-pocock-skills` left open in step 1 joins the first round's frontier.

On a **distil** run, open by putting back what the conversation above already settled, theme by theme, and have the user confirm it. What survives that pass is answered; grill the rest. Restating a decision the user made twenty messages ago is cheap, and inheriting a misremembered one is not.

On design: read `PRODUCT.md` and `DESIGN.md` and grill only where a *product* decision contradicts what is actually in them. Check, do not assume — `/impeccable init` writes product truth and never visual direction, so on a greenfield project the visual direction is genuinely unsettled and belongs to the first UI run sheet, not to this session.

**Stopping rule.** The **frontier** is empty when both hold:

1. Every theme above has an answer you could quote back, not merely a topic that came up.
2. Every section of every format file that applies to this project could be filled in without guessing.

The second is the one that bites. If `DATA-MODEL.md` still needs a guess, or `CONVENTIONS.md`' definition of done has no commands in it, the frontier is not empty however few questions remain — running out of questions is not the same as having the answers.

### 5. Write the foundation

`PRODUCT.md` lives at the repo root, shared with Impeccable. If `/impeccable init` wrote it, append the sections in [PRODUCT-FORMAT.md](assets/PRODUCT-FORMAT.md) and leave every existing section untouched; if there is no file, write those sections alone. If `init` recorded `## Stack` as *delegated*, replace that with a pointer to `ARCHITECTURE.md` rather than a second copy of the table.

Everything else goes in `docs/foundation/`, each from its format file, and nothing else:

| File | Format | Written when |
| --- | --- | --- |
| `ARCHITECTURE.md` | [ARCHITECTURE-FORMAT.md](assets/ARCHITECTURE-FORMAT.md) | always |
| `CONVENTIONS.md` | [CONVENTIONS-FORMAT.md](assets/CONVENTIONS-FORMAT.md) | always — partial on greenfield |
| `DATA-MODEL.md` | [DATA-MODEL-FORMAT.md](assets/DATA-MODEL-FORMAT.md) | the project has a data layer |
| `SEAMS.md` | [SEAMS-FORMAT.md](assets/SEAMS-FORMAT.md) | a scan or the session produced a seam |

Conditional files are born **lazily**. Never leave a placeholder: an unknown that blocks a roadmap line is raised as an ADR with `Status: open`, and one that blocks nothing is an open question in `ARCHITECTURE.md`, written as a question. [DEPTH-AND-DRIFT.md](references/DEPTH-AND-DRIFT.md) carries the rule.

Then point the pipeline at what it cannot find on its own. `/implement` reads nothing on its own and `/to-tickets` sizes every ticket to a fresh context window, so nothing downstream will discover these files by accident. Add to the `## Agent skills` block of whichever of `CLAUDE.md` or `AGENTS.md` `/setup-matt-pocock-skills` edited:

```markdown
### Project foundation

Conventions, reuse inventory and definition of done: `docs/foundation/CONVENTIONS.md`.
Design system — tokens, named rules, do's and don'ts: `DESIGN.md`.
```

Drop the second line for a project with no interface.

Run the self-review in [FOUNDATION-VS-SPEC.md](references/FOUNDATION-VS-SPEC.md), fix what it turns up inline, commit, and gate — this is the first of the two decision points step 2 promised.

**Put the gate as questions, not as reading.** Pick the three to five decisions that are hardest to correct later — the stack, the entity boundaries, one or two glossary terms the whole vocabulary hangs off — and ask each one as a question with your answer already in it, so it can be accepted in a word. Say where the files landed, in one line, so the user *can* open them; do not ask them to.

> "Foundation written to `docs/foundation/`, `PRODUCT.md` extended, glossary and ADRs at `<paths>`. Five decisions worth confirming before I build the roadmap — answer with a word each, or 'all good'.
> 1. Postgres via Drizzle, or …?
> 2. A booking belongs to one customer — never a group. Right?
> …"

### 6. Order the roadmap

Propose an ordered feature list, each item a slice that ships working software on its own. Greenfield opens with the walking skeleton. Lead with one line on why this order — dependencies, riskiest first, thinnest slice first.

**Sizing.** The unit is the **session**, and one roadmap line is one to three of them. That follows from the pipeline rather than from taste: `/to-tickets` sizes each ticket to a single fresh context window, and a line coarse enough to be worth a `/to-spec` session is normally several tickets. The test you can actually apply before any of that exists is **demoability** — can you name what this line makes possible in one sentence, from the user's perspective, without an "and"? If it needs the "and", split it. If it does not fill a sentence, merge it.

Rough tells that a line is too big: it touches three or more unrelated areas that could each ship on their own, or you cannot state its single demoable outcome without listing. Tells that two lines should be merged: one delivers nothing demoable alone, or the two always ship together and share the same acceptance surface.

Sequence by dependency first, then pull risk forward — a line that could invalidate the whole design is cheapest to discover early — and between two orders that both respect dependencies, prefer the one that ships a demoable slice soonest.

**Wide refactors are the exception.** A mechanical change whose blast radius fans across the codebase — rename a column, retype a shared symbol — cannot be a demoable slice, because a single edit breaks thousands of call sites at once. Sequence it as expand–contract across several lines instead: one line adds the new form beside the old so nothing breaks, then one line per batch of call sites migrated (sized by blast radius, each blocked by the expand, CI green throughout because the old form still exists), then one line deleting the old form once no caller remains, blocked by every migrate batch.

Two escapes, both worth naming out loud rather than leaving to be discovered:

- A line whose direction is not yet clear is not a small line — it is fog, and `/wayfinder` exists for exactly that: work too big for one agent session, charted as decision tickets and resolved one at a time until the way is visible. Send it there rather than writing a run sheet over a guess.
- If `/to-tickets` later breaks a line into far more tickets than its neighbours, that is the line telling you it was mis-cut. Go back and split the roadmap line; do not push on through.

Keep it coarse otherwise: one roadmap line is one run sheet is one `/to-spec` session. Finer than that is `/to-tickets`' job — including its own slicing quiz and its own expand–contract sequencing at ticket level. What you are doing here is the same judgement one level up, so that the line handed to `/to-spec` is worth a session; you are not pre-empting the ticket breakdown, and you write no tickets.

Resuming: extend `ROADMAP.md`, never regenerate it. Every existing checkbox and depth carries forward as it stands, because that file is the only record of what has shipped.

Present the list and wait — the second decision point, and again a question, not a document to review. Once the user approves the order, write `docs/foundation/ROADMAP.md` from [ROADMAP-FORMAT.md](assets/ROADMAP-FORMAT.md).

### 7. Write the run sheets

One `docs/foundation/run-sheets/NN-<slug>.md` per roadmap line, from [RUN-SHEET-FORMAT.md](assets/RUN-SHEET-FORMAT.md). Done when every line has one.

**Every sheet is written at `brief`.** On a greenfield project promote line 01 — the walking skeleton — to `detailed` immediately, since the code it describes is the code it will create. On brownfield promote line 01 against the code already there. Every other line stays `brief` until the session that builds it opens and promotes it. Never two at `detailed`. [DEPTH-AND-DRIFT.md](references/DEPTH-AND-DRIFT.md) carries the reasoning; `ROADMAP.md`' Depth column is the only place depth is recorded.

This is where the **narrow pass** of step 3's scan happens: for each line, look at the packages that line touches, so its anchors and its read-first list cite files that exist.

Mark each sheet **UI** or **no UI** — that decides whether the sheet carries the Impeccable design passes. A **no UI** sheet carries no commands at all: the build chain is identical on every sheet and the user works it from memory, so only the UI-only passes are worth writing down. The first UI sheet also carries the design-system setup block, once and never repeated.

Each sheet's briefing names its **anchors** — the entities, seams, screens and reuse targets that apply, by name. Naming them carries one vocabulary from run sheet to glossary to spec, and tells the agent which part of a long file matters. Link the files; never copy their content.

Commit the roadmap and the sheets, then tell the user how to work it: top to bottom, one sheet per feature, opening a fresh session and attaching the sheet — `/grill-with-docs @docs/foundation/run-sheets/NN-<slug>.md`, nothing to copy and nothing to read first. Everything about the documents from that point — deepening the next sheet, reconciling drift, moving the Depth column — is the agent's, triggered by that attachment.
