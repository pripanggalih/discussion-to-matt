# NOTICE — attribution

`discussion-to-matt` is a foundation layer built to sit on top of other people's work. Part of its value is **not original**: it depends on one project, adapts prose from a second, and reuses the author's own prior work from a third. This file credits them honestly.

---

## What was taken from where

| Block in `discussion-to-matt` | Source | License | Relationship |
| --- | --- | --- | --- |
| The whole downstream pipeline it feeds — `/grill-with-docs`, `/to-spec`, `/to-tickets`, `/implement`, `/code-review`, `/tdd`, `/domain-modeling`, `/setup-matt-pocock-skills`, `/wayfinder` | [mattpocock/skills](https://github.com/mattpocock/skills) | MIT | **depended** — invoked, never copied |
| The `/grilling` frontier-and-rounds mechanic that step 4 runs | [mattpocock/skills](https://github.com/mattpocock/skills) — `grilling` | MIT | **depended** — invoked by name |
| Roadmap sizing: the vertical-slice test, the too-big / too-small tells, and the expand–contract treatment of wide refactors | [mattpocock/skills](https://github.com/mattpocock/skills) — `to-tickets`, via [pripanggalih/ajian](https://github.com/pripanggalih/ajian) — `references/roadmap-sizing.md` | MIT | **vendored** (adapted) |
| The depth ladder, the durability and what/how axes, the placeholder ban, and the inclusion test — `references/DEPTH-AND-DRIFT.md` | [pripanggalih/ajian](https://github.com/pripanggalih/ajian) — `ajian-blueprint`, and its predecessor `discussion-to-blueprint` | MIT | **author's own prior work**, adapted |
| The traceability chain and the stranger test in the self-review | [pripanggalih/ajian](https://github.com/pripanggalih/ajian) — `references/doc-charters.md` | MIT | **author's own prior work**, adapted |
| `DESIGN.md`, the design half of `PRODUCT.md`, and every `/impeccable` pass a run sheet names | [impeccable](https://github.com/pbakaus/impeccable) | Apache-2.0 | **depended** — invoked via `npx impeccable` / `/impeccable`, not copied |

The charter machinery (the per-file remit table, the anti-drift rules, the run sheet and its briefing block, the seam registry) is this project's own.

## Where it deliberately diverges

**Roadmap sizing.** `ajian` sizes one roadmap line to exactly one build session, and says why in its own note: it has no downstream ticketing layer, so the sizing wisdom has to live at the roadmap gate. `discussion-to-matt` does have one — `/to-tickets` cuts each line into tickets that are themselves each sized to a fresh context window — so a line here is one to three sessions, and the test applied at the gate is demoability rather than session count.

**Where detail is added.** `ajian` promotes a work order from brief to detailed at the end of the previous feature. This skill promotes at the start of the next session instead, triggered by the user pasting the briefing block: the code is more current, and it costs the user nothing they were not already doing.

**Depth is recorded once.** `ajian` carries a `Depth:` field in the work order and a Depth column in the roadmap. This skill keeps the column and drops the field, because its own glossary forbids a run sheet from recording anything about its own execution.

## Reproduced licenses

### mattpocock/skills — MIT

```
MIT License

Copyright (c) Matt Pocock

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

### impeccable — Apache-2.0

`impeccable` is depended on, not vendored: this repository contains none of its text or code. Its full license ships with the tool and is available at <https://github.com/pbakaus/impeccable>.
