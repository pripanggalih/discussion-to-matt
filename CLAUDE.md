# Contributing to discussion-to-matt

This repository is a **skill**, not an application. It ships prose that shapes how an AI coding agent behaves. Treat the words as the product.

## What lives here

```
.claude-plugin/                 plugin + marketplace manifests
skills/discussion-to-matt/
├── SKILL.md                    the process — seven steps, start to run sheets
├── references/                 what the skill reads to decide
│   ├── FOUNDATION-VS-SPEC.md   per-file charters, anti-drift rules, the self-review
│   ├── DEPTH-AND-DRIFT.md      the depth ladder, promotion, the two axes
│   └── GLOSSARY.md             the vocabulary SKILL.md runs on
└── assets/                     the formats the skill writes from
    ├── ARCHITECTURE-FORMAT.md  CONVENTIONS-FORMAT.md  DATA-MODEL-FORMAT.md
    ├── PRODUCT-FORMAT.md       SEAMS-FORMAT.md
    └── ROADMAP-FORMAT.md       RUN-SHEET-FORMAT.md
README.md                       English (default) · README.id.md  Indonesian
NOTICE.md                       attribution, and where this skill deliberately diverges
```

## The rules that keep this repo honest

1. **It completes Matt's set; it never replaces a part of it.** Before adding anything to a foundation file or a run sheet, ask which downstream skill already owns that output. If one does, point at it — `/to-spec` owns the spec, `/to-tickets` the tickets and acceptance criteria, `/tdd` the seams under test, `/domain-modeling` the glossary and the ADRs, `/impeccable` everything visual. A second version is worse than nothing, because when the two disagree there is no way to tell which is authoritative.

2. **Verify against the source, never from memory.** Every claim this repo makes about another skill's behaviour is checkable — the skills are installed, and their `SKILL.md` is the authority. Three defects in the pre-0.1.0 text came from a plausible assumption about a neighbouring skill that turned out to be wrong. Read the file.

3. **One fact, one home.** The charter table in `FOUNDATION-VS-SPEC.md` is binding. A fact that lands in two files is a defect the moment one copy is corrected.

4. **Where goes in `FOUNDATION-VS-SPEC.md`, when goes in `DEPTH-AND-DRIFT.md`.** Keep the two questions separate; a rule about timing does not belong in the charter table and a rule about ownership does not belong in the depth ladder.

5. **Every link resolves.** `SKILL.md` reaches `references/` and `assets/` by relative path, and the files cross-link each other. Check them after any move:

   ```bash
   grep -rno '](\.\{0,2\}[^)]*\.md)' skills/ | while IFS= read -r hit; do
     f=${hit%%:*}; rest=${hit#*:}; link=${rest#*]}; link=${link#(}; link=${link%)}
     [ -e "$(dirname "$f")/$link" ] || echo "BROKEN $hit"
   done
   ```

6. **The user decides; the agent types.** Anything that asks the user to open, review, or maintain a document is a bug in this skill's premise. Decisions go to the chat as questions answerable in a word.

7. **Attribution stays honest.** `NOTICE.md` names what is depended on, what is vendored, and where this skill diverges from what it adapted — with the reason for the divergence, not just the fact of it.

## Releasing

Bump `version` in `.claude-plugin/plugin.json`, write the entry in `CHANGELOG.md`, tag `vX.Y.Z`. Installed with `npx skills add pripanggalih/discussion-to-matt`.
