# discussion-to-matt

[![license](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![skills](https://img.shields.io/badge/skills-1-informational)](#what-it-writes)

> **[Bahasa Indonesia →](README.id.md)**

One skill: the layer [mattpocock/skills](https://github.com/mattpocock/skills) assumes but never creates.

Matt's engineering skills are excellent per feature. `/to-spec` turns a conversation into a spec, `/to-tickets` cuts it into tracer bullets, `/implement` builds them, `/code-review` checks them. Every one of them opens mid-air: they assume a stack has been chosen, entities have names, seams exist, and "done" means something specific in this repo. Nothing in the set establishes that.

`discussion-to-matt` establishes it once, then hands each feature down the pipeline already grounded.

## What it writes

```
PRODUCT.md                              problem, v1 scope, non-goals, success  (root, shared with impeccable)
docs/foundation/
├── ARCHITECTURE.md                     stack + versions, structure, NFRs, scaffold-or-extend
├── CONVENTIONS.md                      reuse inventory, layout, testing, definition of done
├── DATA-MODEL.md                       entities and relationships          (only if there is data)
├── SEAMS.md                            the seam registry                   (only once there is a seam)
├── ROADMAP.md                          ordered features — the only place progress and depth live
└── run-sheets/NN-<slug>.md             one per roadmap line, attach and go
```

The glossary and the ADRs are **not** written here — `/domain-modeling` writes those inline during the interrogation, and a copy would diverge the moment one side was updated alone. `DESIGN.md` belongs to [impeccable](https://github.com/pbakaus/impeccable).

## The flow

```
a free-form idea  (or a repo you inherited)
  → /discussion-to-matt      interrogate it, write the foundation, order the roadmap,
                             write one run sheet per line
  → per roadmap line, top to bottom, one fresh session each:
      /grill-with-docs @docs/foundation/run-sheets/NN-<slug>.md
      /impeccable shape      (UI only)
      /to-spec  →  /to-tickets  →  /implement
      /impeccable critique · audit · polish   (UI only)
  → next line
```

## What makes it different from writing the docs by hand

**The interrogation has a floor.** It stops when every theme has an answer you could quote back *and* every section of every applicable format could be filled without guessing — not when the questions run out. Running out of questions is not the same as having the answers.

**Detail is written late, on purpose.** Every run sheet starts as a brief. Only the line about to be built is promoted to detailed, against the code that exists by then. A run sheet written today for line 07 describes a codebase six sessions away, and `/to-spec` will read it as settled fact.

**Promotion is the agent's job, not yours.** It fires when you attach the sheet to the next session — nothing to read first, nothing to copy, no checkbox to tick by hand. You answer questions in the chat; the agent writes every file.

**One home per fact.** Each file has a charter, and the self-review checks placeholders with a real `grep`, traces every capability through to a run-sheet anchor that exists, and finishes by re-reading run sheet 01 as an agent that did not witness the conversation.

## Install

With the [vercel-labs `skills`](https://www.skills.sh) CLI:

```bash
npx skills add pripanggalih/discussion-to-matt
```

This skill is a foundation *for* Matt's set — install that too, and run its setup once per repo:

```bash
npx skills add mattpocock/skills
/setup-matt-pocock-skills
```

For a project with an interface, [impeccable](https://github.com/pbakaus/impeccable) as well:

```bash
npx impeccable install
```

If setup has not run, `/discussion-to-matt` runs it for you rather than stopping.

## Use

```
/discussion-to-matt
```

Run it at the **start** of a build and it holds the whole design conversation. Run it at the **end** of one and it opens from what that conversation settled, confirms it theme by theme, and interrogates only the gaps. Run it again later and it resumes: existing checkboxes carry forward, drifted files are topped up, the roadmap is extended and never regenerated.

Greenfield, brownfield, or resumed — it picks the mode itself and tells you which one it is before it asks anything.

## What it does not do

- No code, no spec, no tickets, no plan. Those have owners downstream, and a second version written here is one they will contradict.
- No acceptance criteria and no contracts in a run sheet, for the same reason.
- No session hooks. Every command in a run sheet is one you type.

## License & attribution

MIT ([`LICENSE`](LICENSE)). This skill stands on work it does not own — honest attribution in [`NOTICE.md`](NOTICE.md).
