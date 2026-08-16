# Data model

Entities and how they relate, in business terms.

**This file is not the glossary.** What an entity *means* lives in the glossary — root `CONTEXT.md`, or the context-local one in a multi-context repo — written there once by `/domain-modeling`. Here you record structure: which entities exist, what they hold, and how they connect. If you find yourself defining a word, you are in the wrong file.

In a multi-context repo, give the file one section per context, matching the contexts `CONTEXT-MAP.md` names.

## Entities

One section each, under the exact term the glossary uses.

### <Entity>

What it holds — the fields that matter to the domain, not every column. Types only where the type is itself a decision (money, timezone-bearing dates, enums).

Lifecycle: how one comes into existence, what states it moves through, when it ends. Skip if it is created and never changes.

## Relationships

Stated as sentences, because a sentence forces the cardinality to be explicit:

> A booking belongs to one customer and covers many rooms.
> A room belongs to one property and appears in many bookings.

Then the constraints that are not obvious from the sentences — what cascades on delete, what must be unique, what may never be null.

## Diagram

An ERD in Mermaid, once there is more than a handful of entities.

```mermaid
erDiagram
```

## Deliberate omissions

Data the project consciously does not store, and why. Usually privacy, retention, or "it belongs to the upstream system". Worth writing down — otherwise every few months someone proposes adding it back.
