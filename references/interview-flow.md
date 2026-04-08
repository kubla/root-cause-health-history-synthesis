# Interview Flow

This skill behaves like a finite-state interviewer with memory, a plan, and a publishing pipeline.

## State-by-state guide

### `orient`

Objective: establish purpose, scope, and destination.

Capture:

- what the user wants from the history
- whether the scope is whole-case or focused
- who the audience is: clinician, AI, self, or multiple
- whether the user wants a draft, refined brief, or frozen snapshot
- whether prior notes or imports already exist

Good opening prompts:

- "What are the top one to three problems you most want this history to help clarify?"
- "Do you want a whole-case history or a focused history around one main cluster?"
- "Who is the immediate audience for this output?"
- "What would make this effort feel successful?"

### `story-skeleton`

Objective: build the trunk of the case before branching.

Capture:

- last-known-well
- what changed
- earliest symptoms
- major turning points
- current bottlenecks
- why this matters now

Prompt pattern:

- "Walk me from the last time you felt mostly well to where things are now."
- "What changed first, and what came after that?"
- "What were the biggest turning points rather than every detail?"

### `dominant-cluster`

Objective: deepen the most decision-relevant symptom cluster first.

Choose the first deep dive based on:

- relevance to top concern
- relevance to desired audience
- leverage for the causal map
- likely effect on treatment history interpretation

For the chosen cluster, capture:

- onset and timing
- severity and frequency
- pattern over time
- triggers and relievers
- functional impact
- linked events, exposures, and treatments

### `targeted-branches`

Objective: open only the branches that materially improve the case.

Good candidates:

- sleep and circadian
- GI and food response
- mood, anxiety, and cognition
- hormonal and reproductive
- environment and exposures
- infections and inflammatory episodes
- early life and adversity
- prior workup and clinician journey
- practical constraints

Read [branch-guides.md](branch-guides.md) before opening a branch.

### `evidence-integration`

Objective: use imported evidence to sharpen the case rather than duplicate it.

When imports exist:

1. read the capsule
2. map it onto the timeline
3. link it to symptom clusters
4. update candidate causal factors
5. retire answered questions
6. add only new questions that create real leverage

Read [evidence-integration.md](evidence-integration.md).

### `gap-fill`

Objective: ask only the highest-value unanswered questions.

Look for:

- timeline holes
- poorly defined clusters
- confusing treatment-response sequences
- missing family or exposure context
- contradictions with meaningful downstream impact

### `synthesis-ready`

Objective: test whether the case is already useful enough to publish.

The case is ready for draft artifacts when:

- the story trunk is coherent
- the major clusters are clear
- the strongest candidate causal factors are visible
- the practical constraints are explicit
- the next open questions are narrower than the value assembled

### `snapshot`

Objective: freeze an immutable version for a focus and audience.

Read [snapshot-policy.md](snapshot-policy.md) and [output-contract.md](output-contract.md).

### `resume`

Objective: continue without re-interviewing old ground.

On resume:

1. read `CASE.md`
2. read `PLAN.md`
3. read `EVIDENCE.md` if unresolved evidence issues exist
4. read `OUTPUT.md` if draft work already exists
5. summarize the current case state before asking the next question

## Checkpoint summary pattern

Use checkpoint summaries whenever the story turns or enough facts have accumulated to re-steer the interview.

Checkpoint structure:

1. one-line case summary so far
2. current narrative spine
3. dominant clusters identified
4. strongest candidate causal factors
5. unresolved tensions or missing facts
6. next best question or next branch

Checkpoint summaries should sharpen the plan, not just repeat facts.

## Question scoring rubric

Score candidate questions on a 0 to 3 scale for:

- impact on causal map
- timeline value
- output value
- uncertainty reduction
- relevance to top concern
- user burden

Formula:

```text
priority =
  (impact_on_causal_map * 3) +
  (timeline_value * 2) +
  (output_value * 2) +
  (uncertainty_reduction * 2) +
  (relevance_to_top_concern * 3) -
  (user_burden * 2)
```

Prefer one high-yield question over three mediocre ones.

## Resume logic

If the user returns with new information:

- preserve existing structure
- integrate the new information into the timeline and clusters
- update contradictions if old understanding changed
- adjust the plan before asking more questions
- create a new snapshot only when the update materially changes the case or the user wants a frozen version
