# Root Cause Health History Synthesis

This repository contains a reusable agent skill for building unusually strong, longitudinal health histories that are actually useful for root-cause analysis.

Its mission is simple:

Turn scattered memory, partial records, and evolving understanding into one living case representation that can be resumed over time, rendered for different audiences, and frozen into versioned snapshots when it is strong enough to share.

Most medical-history workflows fail in one of two ways. They either become a bloated intake form that loses the person’s story, or they stay conversational but never harden into artifacts another clinician or AI system can reliably use. This skill is designed to close that gap.

## License

This repository is licensed under Apache License 2.0. That keeps the project broadly reusable while also giving downstream users an explicit patent grant and clear redistribution terms.

## What This Skill Is For

Use this skill when the goal is to build or refine:

- a comprehensive health history from scratch
- a root-cause-oriented case summary
- a clinician-grade pre-visit brief
- a structured AI-ready case handoff
- a longitudinal synthesis that spans multiple sessions
- a focused version of the same case for fatigue, GI, sleep, hormonal, cognitive, pain, immune, or other dominant clusters
- a versioned snapshot that preserves what was believed at a moment in time

## Core Idea

This skill takes a different stance from a broad intake or multimodal-ingestion workflow.

It is not trying to be the universal front door for every health artifact. Instead, it acts like a disciplined longitudinal interviewer with memory, a live plan, and a publishing pipeline. It keeps one canonical case, updates it after every meaningful turn, and decides the next best question based on leverage rather than checklist order.

That leads to a few strong opinions:

- Narrative before taxonomy. Build the trunk of the story before spreading into branches.
- One canonical case, many renderings. Clinician and AI outputs should come from the same underlying case model.
- Questions should earn their place. Ask the next question that most improves the timeline, causal map, or downstream artifact.
- Resumability matters. Every meaningful interaction should leave behind compact case memory.
- Versioning matters. New understanding should extend the case without erasing prior states.
- Evidence should stay sourced. Imported evidence is integrated explicitly, not laundered into anonymous truth.

## What It Produces

The skill is designed to maintain live case files and publish durable outputs.

Live case files:

- `CASE.md`: compact, stable case truth
- `PLAN.md`: tactical interview brain
- `EVIDENCE.md`: sourced evidence ledger
- `OUTPUT.md`: working draft of deliverables

Published artifacts:

- `history-master.md`
- `clinician-brief.md`
- `ai-brief.md`
- `causal-map.md`
- `case-object.json`

It also supports immutable snapshots with lineage, so the same case can generate baseline, milestone, focus-specific, and handoff-specific versions over time.

## Why This Approach Matters

Root-cause-oriented history work is not just data collection. It is compression, sequencing, and judgment.

The quality bar is not “did we ask everything?” The quality bar is “can we now tell the story from last-known-well to current state, identify the major clusters and turning points, preserve uncertainty honestly, and hand the case to a clinician or AI without forcing them to reconstruct the patient from fragments?”

This skill is built around that bar.

## Use Cases

- A patient wants to prepare for a first visit with an internist, gastroenterologist, endocrinologist, sleep specialist, psychiatrist, or functional-medicine clinician.
- A user has a complex chronic history and wants to turn years of recollection into a coherent timeline with symptom clusters and treatment-response patterns.
- A case has already been partially captured, and the user wants to resume from prior notes instead of starting over.
- Another skill has already summarized labs, records, wearable data, or questionnaires, and those evidence capsules now need to be integrated into one canonical case.
- A user wants one whole-case history plus separate focused snapshots for fatigue, GI symptoms, or specialist handoff.
- A user wants an AI consultation brief that preserves provenance, contradictions, open questions, and a machine-legible case object.

## Repository Layout

```text
root-cause-health-history-synthesis/
├── SKILL.md
├── README.md
├── LICENSE.txt
├── agents/
│   └── openai.yaml
├── references/
│   ├── interview-flow.md
│   ├── branch-guides.md
│   ├── instrument-registry.md
│   ├── evidence-integration.md
│   ├── synthesis-rules.md
│   ├── snapshot-policy.md
│   └── output-contract.md
├── assets/
│   ├── CASE.template.md
│   ├── PLAN.template.md
│   ├── EVIDENCE.template.md
│   ├── OUTPUT.template.md
│   ├── clinician-brief.template.md
│   ├── ai-brief.template.md
│   ├── snapshot-manifest.template.md
│   └── case-object.schema.json
└── evals/
    └── evals.json
```

## Live Case Workspace

The skill expects case-specific work to live outside the reusable skill package in a workspace such as:

```text
.casework/<case-id>/
├── CASE.md
├── PLAN.md
├── EVIDENCE.md
├── OUTPUT.md
├── imports/
│   └── *.md
└── snapshots/
    ├── manifest.md
    └── <snapshot-id>/
        ├── history-master.md
        ├── clinician-brief.md
        ├── ai-brief.md
        ├── causal-map.md
        └── case-object.json
```

## Using The Skill

Invoke it when the job is to construct, refine, resume, or snapshot a complex health history:

`Use $root-cause-health-history-synthesis to build or resume a longitudinal health history, keep the case files updated, and publish clinician and AI briefs when the case is strong enough.`

## Safety Note

This skill is for structured history-building and synthesis, not emergency triage or diagnosis. Urgent symptoms, self-harm risk, or other emergency situations should interrupt the normal workflow and be escalated immediately to appropriate care.
