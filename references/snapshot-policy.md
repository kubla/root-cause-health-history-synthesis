# Snapshot Policy

Snapshots are immutable frozen renders of the case at a moment in time. They preserve lineage while the live case continues to evolve.

## Snapshot types

- baseline snapshot
- milestone snapshot
- focus snapshot
- handoff snapshot

## Snapshot metadata

Every snapshot should capture:

- `snapshot_id`
- `case_id`
- `created_at`
- `parent_snapshot`
- `focus`
- `audience`
- `basis`
- `summary_of_changes`
- `open_questions`
- `confidence_note`

## When to freeze a snapshot

Create a snapshot when:

- the user explicitly asks for one
- the case reaches `snapshot-ready`
- a new audience needs a frozen handoff
- a major shift in understanding changes the case materially
- a focused version of the same case is needed without mutating prior outputs

## Lineage rules

- Preserve old snapshots.
- Never overwrite an earlier snapshot.
- Record parentage when a new snapshot descends from an earlier one.
- Keep the live case mutable and the snapshot immutable.
- Show lineage both in `snapshots/manifest.md` and in `case-object.json`.

## Delta-note rules

When a parent snapshot exists, include a short delta note that answers:

- what changed
- what stayed stable
- what is still unresolved

Keep the delta note short and specific.

## Snapshot workflow

1. confirm the target focus and audience
2. finalize the relevant sections in `OUTPUT.md`
3. create a new snapshot folder under `snapshots/`
4. write immutable artifacts into that folder
5. update `snapshots/manifest.md`
6. append lineage in the machine-readable case object

## Naming guidance

Use stable, sortable snapshot identifiers such as:

`2026-04-07-baseline-clinician`

or

`2026-04-21-fatigue-ai-milestone`

The exact naming scheme can vary, but it should preserve order, focus, and audience.
