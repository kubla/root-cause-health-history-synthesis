# Output Contract

This skill produces one canonical master history and several audience-specific transforms of that same case.

## Required artifacts

1. `history-master.md`
2. `clinician-brief.md`
3. `ai-brief.md`
4. `causal-map.md`
5. `case-object.json`

## `history-master.md`

Purpose: the full high-signal narrative and structural record.

Required sections:

- one-line case summary
- top concerns
- goals
- narrative spine
- timeline
- symptom clusters
- past medical history
- medications and supplements
- family patterning
- lifestyle
- exposures
- prior workup
- treatment response table
- imported evidence summary
- causal map
- contradictions
- unresolved questions
- practical constraints
- provenance notes

Style rules:

- lead with the story, not background noise
- keep section headers stable
- preserve uncertainty visibly
- keep evidence sources legible

## `clinician-brief.md`

Purpose: concise, skimmable, timeline-forward handoff.

Recommended sections:

- one-line case summary
- top concerns
- timeline with turning points
- major symptom clusters
- notable PMH, medications, family history, and exposures
- treatment response history
- prior workup already done
- strongest current causal hypotheses
- biggest remaining questions
- practical constraints

Style rules:

- optimize for fast reading
- prefer bullets and short paragraphs over dense prose
- keep hypotheses cautious and clearly marked

## `ai-brief.md`

Purpose: provenance-aware, structured input for downstream reasoning.

Recommended sections:

- case summary
- explicit goals for the AI
- machine-legible timeline
- symptom clusters with linked evidence
- imported evidence digest
- causal map with confidence labels
- contradictions
- unresolved questions
- suggested reasoning prompts

Style rules:

- make structure explicit
- preserve contradictions and uncertainty
- include provenance where it affects reasoning quality

## `causal-map.md`

Purpose: stand-alone representation of candidate drivers and maintainers.

Use a table with these columns:

| Factor | Type | Period | Linked symptoms | Evidence | Confidence | Modifiability | Notes |
|---|---|---|---|---|---|---|---|

Allowed factor types:

- antecedent
- trigger
- mediator
- perpetuator
- protective factor

## `case-object.json`

Purpose: machine-readable canonical case representation.

Required top-level fields:

- `case_id`
- `current_stage`
- `one_line_summary`
- `top_concerns`
- `goals`
- `timeline`
- `turning_points`
- `symptom_clusters`
- `past_medical_history`
- `medications`
- `supplements`
- `family_history`
- `lifestyle`
- `exposures`
- `treatment_responses`
- `imported_evidence`
- `causal_map`
- `contradictions`
- `missing_information`
- `practical_constraints`
- `audience_renderings`
- `snapshot_lineage`

Schema conventions:

- arrays for repeatable facts
- objects when fields need labels and provenance
- preserve source and confidence when known
- keep timeline elements and cluster objects consistent across snapshots
