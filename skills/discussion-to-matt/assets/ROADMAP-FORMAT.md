# Roadmap

Ordered features, and the only place progress lives. One read answers three questions: where am I, what is next, and how deep is the next sheet.

**Order rationale:** one or two sentences on why this order — dependencies, riskiest first, thinnest slice first. Greenfield: why the walking skeleton comes first.

**Granularity:** one line here is one run sheet is one `/to-spec` session, and one to three build sessions. The test is demoability — one sentence, from the user's perspective, with no "and" in it. Anything finer is `/to-tickets`' job; anything whose direction is still fog is `/wayfinder`'s.

## Build order

| # | Done | Feature | What it makes possible | Depends on | Depth | Run sheet |
| - | ---- | ------- | ---------------------- | ---------- | ----- | --------- |
| 01 | [ ] | <feature> | <one line, from the user's perspective> | — | detailed | `run-sheets/01-<slug>.md` |
| 02 | [ ] | <feature> | <one line> | 01 | brief | `run-sheets/02-<slug>.md` |
| 03 | [ ] | <feature> | <one line> | 01 | brief | `run-sheets/03-<slug>.md` |

Tick a box when the feature is merged, not when its tickets are written.

**Depth** is `brief` or `detailed`, and this column is the only place it is recorded — a run sheet is **stateless** and never carries a field announcing its own depth. Exactly one line may be `detailed`: the next unbuilt one. Everything else stays `brief` until the session that builds it opens, promotes it against the code that exists by then, and moves this column. See [DEPTH-AND-DRIFT.md](../references/DEPTH-AND-DRIFT.md).

## Dependencies

Only where the order is not obvious from the numbering — a feature blocked by something two steps back, or two that could genuinely run in parallel.

## Not on the roadmap yet

Ideas raised in the foundation session and consciously deferred, one line each on why, and what would bring them back. Keeps them from being re-proposed as though new, and keeps them out of the scope of everything above. Anything cut permanently belongs in `PRODUCT.md`' non-goals instead.

## How this roadmap is worked

1. Take the lowest-numbered unticked line.
2. Open a fresh session at the project root, run `/grill-with-docs`, and paste that sheet's briefing block.
3. The session promotes the sheet to `detailed` before it grills, reconciles any foundation drift, and updates this table. Nothing here is the user's to edit.
4. Work the sheet's commands in order.
5. On merge, the sheet's *On finishing* ticks the box here.
