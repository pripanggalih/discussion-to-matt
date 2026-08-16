# Changelog

All notable changes to this project are documented here. Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.0] — unreleased

First packaged release. The skill existed before this as loose files; this version is the first one installable with `npx skills add`.

### Added

- **Repository layout** for distribution: `skills/discussion-to-matt/` with `references/` and `assets/`, plus plugin and marketplace manifests, MIT license, and `NOTICE.md` attribution.
- **`references/DEPTH-AND-DRIFT.md`** — the depth ladder (`brief` / `detailed`, exactly one detailed at a time), the durability and what/how axes, the placeholder ban, the two-places-only rule for the stack, and the inclusion test for documents.
- **Depth column in `ROADMAP.md`**, which is now a table and carries an order rationale and a "how this roadmap is worked" section.
- **Promotion at the start of a session.** A run sheet's *Before grilling* block tells the opening agent to deepen the sheet against current code, reconcile foundation drift, and move the Depth column — triggered by the user pasting the briefing block, with no document for them to maintain.
- **Read-first list** in every briefing block, naming only the documents that bear on that feature.
- **Design-system setup block** on the first UI run sheet only: `npx impeccable install`, `/impeccable hooks on`, `/impeccable shape`.
- **Roadmap sizing rails** — demoability as the gate test, too-big and too-small tells, order by dependency then risk then thinnest-slice, an explicit `/wayfinder` escape for work still in fog, and expand–contract sequencing for wide refactors.
- **Executable self-review** — a real `grep` for placeholders, a traceability chain from capability through roadmap line to a run-sheet anchor that exists, and a stranger test over run sheet 01.
- **Glossary terms** `depth` and `promotion`.

### Changed

- **Preflight prepares instead of blocking.** `/setup-matt-pocock-skills` is run inline when its output is missing, and its questions join the first grilling round.
- **Grilling has a stopping floor** — every theme answered *and* every applicable format section fillable without guessing, rather than "the frontier is empty".
- **Both gates are questions, not documents.** Three to five hard-to-reverse decisions asked in the chat, answerable in a word. The user is never asked to review or edit a file.
- **Brownfield scan is two passes** — a wide pass in step 3 that no longer waits on a roadmap that does not exist yet, and a narrow per-line pass while writing run sheets. The wide pass reaches for the codebase knowledge graph before reading files.
- **Unknowns that block a roadmap line** become ADRs with `Status: open` naming the blocked line; only non-blocking unknowns stay as open questions in `ARCHITECTURE.md`.
- **The "everything inside the block" rule** is now "no second copy of intent, scope or anchors outside the block", which is the drift it was always guarding against.
- **`On finishing` shrank** to what would be lost with the session's context — tick the roadmap, record the seam, extract the component. Drift reconciliation moved to the next session's opening.
- **A run sheet promoted to `detailed`** gains flows, edge cases and data effects — never acceptance criteria or contracts, which belong to `/to-spec` and `/to-tickets`.

### Fixed

- **The `DESIGN.md` preflight blocked on a file it could never produce.** `/impeccable init` writes `PRODUCT.md` and is forbidden from raising visual direction; `DESIGN.md` comes from a new-work request or `/impeccable document`. Preflight now checks `PRODUCT.md`, suggests `/impeccable document` for brownfield UI, and leaves the greenfield visual world to the first UI run sheet.
- **Stack ownership collision.** `/impeccable init` asks about the stack on an unscaffolded project; preflight now has the user answer *delegated* so `ARCHITECTURE.md` stays the only owner.
- **Misattributed context behaviour** — the fresh-context-window-per-ticket rule is `/to-tickets`', not `/implement`'s.
- **Greenfield with no git repo** no longer walks into a failing `git commit`; step 2 asks once whether to `git init` and silently skips every commit if the answer is no.
