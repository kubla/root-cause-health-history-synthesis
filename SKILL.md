---
name: root-cause-health-history-synthesis
description: Interviews a person over one or more sessions to build a longitudinal, causally useful health history and produce structured outputs for clinicians and AI systems. Use when the task is to construct, refine, resume, or snapshot an extraordinary medical history for root-cause analysis, pre-visit preparation, or downstream AI consultation.
license: Apache-2.0. LICENSE.txt has complete terms.
compatibility: Designed for skills-compatible agents that support SKILL.md frontmatter, markdown references, file reads and writes, and progressive disclosure.
metadata:
  version: "1.0"
  category: "health-history"
  primary_outputs: "history-master.md clinician-brief.md ai-brief.md causal-map.md case-object.json"
  case_memory_files: "CASE.md PLAN.md EVIDENCE.md OUTPUT.md"
  supports_snapshots: "true"
  supports_resume: "true"
---

# Root Cause Health History Synthesis

Build an unusually strong, longitudinal health history that supports root-cause analysis without drifting into infinite intake.

## When to use this skill

Use this skill when the user wants any of the following:

- a comprehensive health history from scratch
- a root-cause-oriented case history
- a clinician-grade pre-visit brief
- a structured case for AI consultation
- a longitudinal synthesis across multiple sessions
- a focused history centered on fatigue, GI, sleep, cognition, hormones, pain, immune issues, or similar themes
- a versioned snapshot of the case at a moment in time
- a revision that preserves earlier versions while extending the live case

Do not use this skill for narrow one-off medical questions that do not require case construction or synthesis.

## Safety

This skill is for history-building, synthesis, and handoff. It is not a diagnosis engine.

If the user reports emergency symptoms, self-harm risk, severe bleeding, neurological emergency signs, or other urgent concerns, stop the usual intake flow and direct urgent care immediately.

## Operating stance

Keep these principles active throughout the workflow:

1. Narrative before taxonomy.
2. Build the trunk before the branches.
3. Let the case teach the plan.
4. Ask the next best question, not the next checklist item.
5. Maintain one canonical case and generate multiple renderings from it.
6. Update case memory after every substantive turn.
7. Preserve older versions through snapshots instead of overwriting history.
8. Keep imported evidence visibly sourced.
9. Favor useful publishable artifacts over perfect completeness.

## Required live case files

Maintain the live case in `.casework/<case-id>/`.

- `CASE.md`: stable compressed truth about the case
- `PLAN.md`: interview state, uncertainties, and next questions
- `EVIDENCE.md`: evidence capsules, provenance, tensions, retired questions
- `OUTPUT.md`: working drafts of summaries and artifacts

If the case folder exists but a required file is missing, create it from the matching template in `assets/`.

## Activation sequence

When this skill activates:

1. Read `.casework/<case-id>/CASE.md` if it exists.
2. Read `.casework/<case-id>/PLAN.md` if it exists.
3. Read `.casework/<case-id>/EVIDENCE.md` if imported evidence exists or unresolved evidence issues remain.
4. Read `.casework/<case-id>/OUTPUT.md` if there is an in-progress draft.
5. Read [references/interview-flow.md](references/interview-flow.md).
6. Read only the additional reference files needed for the current phase.

Use progressive disclosure aggressively. Do not load every branch guide or reference file unless the case needs it.

## Finite-state workflow

Work through these states as needed:

- `orient`
- `story-skeleton`
- `dominant-cluster`
- `targeted-branches`
- `evidence-integration`
- `gap-fill`
- `synthesis-ready`
- `snapshot`
- `resume`

Default sequence:

1. Clarify the user’s purpose, desired audience, and desired output state.
2. Build the story trunk from last-known-well to current bottlenecks.
3. Deepen the dominant symptom cluster first.
4. Expand into targeted branches only when they materially improve the timeline, causal map, or handoff artifact.
5. Integrate imported evidence capsules from `imports/` when available.
6. Draft outputs as soon as the case is coherent enough to be useful.
7. Freeze snapshots when requested or when the case is strong enough to preserve.

## Turn loop

After each substantive turn:

1. Update `CASE.md`.
2. Update `PLAN.md`.
3. Update `EVIDENCE.md` if evidence changed the case.
4. Update `OUTPUT.md` if any section is stable enough to draft.
5. Decide whether the case has reached the next completion level.

Before asking a new question:

- inspect `CASE.md` and `PLAN.md`
- retire questions already answered
- prefer 1 to 3 high-leverage questions
- re-score the plan instead of blindly continuing a checklist

## Question selection

Use a simple leverage score for candidate questions:

```text
priority =
  (impact_on_causal_map * 3) +
  (timeline_value * 2) +
  (output_value * 2) +
  (uncertainty_reduction * 2) +
  (relevance_to_top_concern * 3) -
  (user_burden * 2)
```

Score each factor from 0 to 3. Ask the best 1 to 3 questions, then re-score after the answer.

The job is to ask the next best question, not to perform a giant intake dump.

## Trunk-first rule

Establish these early and keep them visible near the top of `CASE.md`:

- last-known-well
- what changed
- first symptoms
- major turning points
- current state
- why-now hypotheses

Do not let the case fragment into unconnected symptom details before the trunk exists.

## Symptom-cluster method

Store symptoms as clusters rather than as a flat list. Each cluster should capture:

- label
- onset
- current severity
- frequency
- pattern
- triggers
- relievers
- functional impact
- linked events
- linked treatments
- linked evidence capsules

Use [references/branch-guides.md](references/branch-guides.md) when a branch requires deeper questioning.

## Instruments and evidence

Use instruments only as targeted probes when they add signal. See [references/instrument-registry.md](references/instrument-registry.md).

When imported evidence capsules exist in `imports/`, integrate them using [references/evidence-integration.md](references/evidence-integration.md). Preserve provenance and visibly distinguish sourced facts from inference.

## Synthesis and publishing

Use [references/synthesis-rules.md](references/synthesis-rules.md) while compressing the case and drafting outputs.

When the case is coherent enough to publish, produce:

1. `history-master.md`
2. `clinician-brief.md`
3. `ai-brief.md`
4. `causal-map.md`
5. `case-object.json`

Use detailed formatting rules from [references/output-contract.md](references/output-contract.md).

## Snapshots and resume

Versioning is first-class. Use [references/snapshot-policy.md](references/snapshot-policy.md).

When a snapshot is requested or the case is snapshot-ready:

1. finalize the relevant draft sections in `OUTPUT.md`
2. create a new snapshot folder
3. write immutable artifacts
4. update `snapshots/manifest.md`
5. record parentage and a short delta note when there is a parent snapshot

When resuming, start by reading the live case files before asking new questions.

## Completion levels

Judge the case using these levels:

- `draft`
- `strong`
- `snapshot-ready`
- `mature`

Release artifacts once all of the following are true:

- a credible one-line summary exists
- the narrative spine from last-known-well to now is present
- the major symptom clusters are clear enough to reason over
- enough background exists to interpret those clusters
- treatment response history reduces confusion instead of adding it
- practical constraints are realistic
- remaining questions are narrower than the value already assembled

Useful finished artifacts beat waiting for perfect completeness.
