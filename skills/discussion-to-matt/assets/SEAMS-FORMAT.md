# Seam registry

The project's testing seams — the public boundaries tests observe behaviour through.

This file exists so "prefer an existing seam, use the highest one available, keep the count as low as possible" is enforceable. Without a list, every session invents seams blind and the count creeps.

Nothing reads this file automatically. It reaches `/to-spec` and `/tdd` because each run sheet hands it over as an anchor, so a feature whose sheet omits it gets no benefit from it.

Listing a seam here does not pre-agree it. `/tdd` still requires the user to confirm the seams for each feature before a test is written at one.

## Registry

| Seam | What it exposes | Height | Test location | Prior art |
| --- | --- | --- | --- | --- |

**Height** — how far up the stack the seam sits. A seam at the HTTP boundary or a top-level module interface is high; one at a repository or an internal helper is low. High seams survive refactors; prefer them.

**Prior art** — an existing test file at this seam, so the next feature copies a real pattern instead of inventing one.

## Not seams

Boundaries that look testable but are deliberately not tested directly, and what covers them instead. This list stops the same rejected boundary being proposed every few weeks.

## Adding a seam

A new seam needs a reason no existing seam could serve, and it goes in at the highest point that works. Record it here the moment the user confirms it, not after the feature ships.
