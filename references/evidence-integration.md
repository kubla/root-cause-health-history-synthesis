# Evidence Integration

This skill integrates concise evidence capsules produced by other skills or workflows. It does not treat raw ingestion as the main job.

## Evidence capsule contract

Expected location:

- `.casework/<case-id>/imports/*.md`

Preferred structure:

```markdown
# Evidence Capsule

- id:
- title:
- source_skill:
- source_kind:
- period:
- key_facts:
- provenance:
- confidence:
- structural_or_dynamic:
- likely_relevance:
- questions_raised:
```

Common `source_kind` values:

- `lab-summary`
- `record-summary`
- `imaging-summary`
- `wearable-trend-summary`
- `medication-reconciliation`
- `questionnaire-result`

## Integration workflow

For each capsule:

1. identify what period of the story it belongs to
2. map it onto the timeline
3. link it to one or more symptom clusters
4. update causal factors if the evidence materially changes them
5. retire questions already answered by the capsule
6. open new questions only if they create meaningful leverage

Imported evidence should reduce interview burden, not create duplication.

## Provenance rules

- Keep the capsule visibly sourced in `EVIDENCE.md`.
- Distinguish sourced facts from inference.
- Preserve the capsule title, source, period, and confidence.
- If the capsule changes the case materially, say exactly how.
- If the capsule conflicts with prior self-report or another source, preserve the contradiction rather than silently normalizing it away.

## Updating `EVIDENCE.md`

Maintain these sections:

- artifact inventory
- imported evidence capsules
- evidence that changed the case
- contradictions and tensions
- questions retired by evidence
- questions opened by evidence

Good ledger language:

- "Capsule answered whether the onset preceded the move."
- "Capsule retired the question of whether ferritin had ever been low."
- "Capsule opened a new question about whether symptoms track with menstrual phase."

## Updating the case model

When evidence changes the case:

- add the fact to `CASE.md` if it belongs in compressed truth
- update `PLAN.md` to reflect retired and newly opened questions
- update `OUTPUT.md` if the draft artifact now has stronger support
- carry the capsule into `case-object.json` with provenance intact

## What not to do

- do not paste raw documents into `EVIDENCE.md`
- do not erase uncertainty just because something is written down
- do not keep asking the user questions the capsule already answers
- do not convert weak evidence into strong causal claims
