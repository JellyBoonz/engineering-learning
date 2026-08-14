# Competency model

Use this reference to create, update, or summarize a granular model. Track only competencies relevant to current or anticipated work.

## Contents

- Principles
- Decomposition schema
- Levels
- Evidence dimensions
- Confidence and recency
- Update rules
- Durable record template
- Example decomposition

## Principles

- Model capability, not identity.
- Scope every claim to a technology, context, and class of task.
- Decompose until evidence is observable in normal repository work.
- Store evidence and assistance, not just a label.
- Distinguish recognition from independent performance.
- Treat transfer and retention as required evidence for durable strength.
- Allow uneven profiles: explanation may be strong while debugging is developing.

## Decomposition schema

Represent each competency as a path:

`domain / system or technology / capability / context or boundary`

Useful capability facets:

1. **Vocabulary and recognition** — identify constructs and relevant signals.
2. **Mental model** — explain mechanism and predict behavior.
3. **Implementation** — produce a correct solution under ordinary constraints.
4. **Debugging** — localize failures, form hypotheses, and interpret evidence.
5. **Tradeoffs** — compare alternatives and identify boundaries or failure modes.
6. **Operations** — observe, deploy, mitigate, and recover safely.
7. **Transfer** — apply the governing principle in a changed context.

Do not create every facet automatically. Create the smallest set that captures observed differences.

Bad: `Strong at databases.`

Better:

- `data / PostgreSQL / transaction isolation / predict read phenomena`
- `data / PostgreSQL / query plans / diagnose missing-index regressions`
- `data / migrations / rollout design / backward-compatible schema change`

## Levels

### Unknown

Use when there is no evidence, the user explicitly reports no familiarity, or the observed model is too incomplete to guide action.

Typical evidence:

- cannot yet identify the relevant concept;
- prediction is absent or largely guessed;
- needs a complete explanation and worked example.

Default support: Explore with a small model and concrete repository anchor.

### Conceptual

Use when the user can explain or recognize the idea but has not shown reliable application.

Typical evidence:

- predicts a standard case after explanation;
- explains the mechanism in their own words;
- recognizes where the concept applies;
- still needs substantial scaffolding to implement or debug.

Default support: Explore moving toward Apply.

### Developing

Use when the user can perform in familiar cases but remains inconsistent, scaffold-dependent, or brittle at boundaries.

Typical evidence:

- implements a normal case with limited hints;
- diagnoses a relevant failure after orientation;
- explains key tradeoffs but misses some edge conditions;
- transfers with help or succeeds only in a closely similar case.

Default support: Apply with fading hints.

### Strong

Use when the user repeatedly performs independently, diagnoses failures, explains tradeoffs, and transfers the principle.

Typical evidence:

- predicts and explains behavior accurately;
- implements and verifies without target-specific scaffolding;
- debugs a nontrivial failure using appropriate evidence;
- identifies when the approach fails or should not be used;
- succeeds in a meaningfully varied context;
- retains competence after time has passed when recency matters.

Default support: Execute, with occasional lightweight sampling.

Strong is not universal expertise. State the context in which strength was demonstrated.

## Evidence dimensions

For each entry, record evidence across applicable dimensions:

| Dimension | Evidence question | Weak evidence | Strong evidence |
|---|---|---|---|
| Explain | Can the user state the causal model? | repeats wording | explains mechanism and limits |
| Predict | Can the user anticipate behavior before running it? | guesses after prompts | correct on ordinary and edge cases |
| Implement | Can the user produce the critical logic? | copies full solution | writes/adapts with little help |
| Debug | Can the user localize and test hypotheses? | waits for diagnosis | uses evidence to isolate cause |
| Evaluate | Can the user choose among alternatives? | names preferences | ties tradeoffs to constraints |
| Transfer | Can the user adapt to changed conditions? | repeats same recipe | applies principle in a new case |
| Retain | Does performance persist? | immediate recall only | succeeds after a meaningful delay |

Record the hint level:

- `H0`: independent;
- `H1`: orienting question;
- `H2`: narrowed location or relevant principle;
- `H3`: pseudocode or ordered plan;
- `H4`: full solution supplied.

H3–H4 completion is delivery evidence but usually weak competency evidence.

## Confidence and recency

Track confidence separately:

- **Low**: self-report or one ambiguous observation.
- **Medium**: one clear work sample or several aligned indirect observations.
- **High**: repeated direct evidence across dimensions, including transfer.

Add an observation date. Lower confidence, not necessarily level, when evidence is stale or the environment changes materially. Recalibrate brittle or high-risk competencies sooner.

## Update rules

- Initialize unknown rather than guessing from seniority or job title.
- Move at most one level per ordinary session unless evidence is unusually comprehensive.
- Promote from unknown to conceptual on a correct causal explanation and prediction.
- Promote to developing on successful application with no more than limited hints.
- Promote to strong only with independent performance plus debugging/tradeoff evidence and a transfer check.
- Do not promote from agent-authored target work that the user only reviewed.
- Demote or reduce confidence after repeated unexplained errors, inability to reconstruct the model, or material context change.
- Make updates local to the exercised subcompetency.
- Record contrary evidence instead of averaging it away.

## Durable record template

Use the repository's existing convention if one exists. Otherwise produce this compact structure in chat or in a user-approved tracking file:

```yaml
competency: "runtime / async cancellation / propagation across retry boundaries"
level: "developing"
confidence: "medium"
observed: "YYYY-MM-DD"
context: "service worker; cooperative cancellation; retry loop"
evidence:
  explain: "Predicted cancellation at backoff and explained propagation. H0."
  implement: "Added cancellation-aware delay. H1."
  debug: "Localized swallowed cancellation to broad exception handler. H2."
  transfer: "Not yet observed."
contrary_evidence:
  - "Initially assumed cancellation was a normal retryable failure."
next_check: "Adapt the pattern to parallel fan-out with partial completion."
```

Do not store sensitive performance judgments or personal data. Prefer user-owned, transparent records.

## Example decomposition

For a broad target such as “learn async,” a working model might contain:

| Competency | Level | Evidence needed next |
|---|---|---|
| async / scheduling / trace suspension and resumption | conceptual | predict interleaving in repository code |
| async / structured concurrency / child lifetime ownership | developing | adapt implementation to nested task failure |
| async / cancellation / propagation | developing | independently diagnose swallowed cancellation |
| async / resource safety / cleanup on cancellation | unknown | explain and implement cleanup boundary |
| async / testing / deterministic concurrency tests | conceptual | write a stable failure-focused test |
| async / operations / diagnose stalled task | unknown | use traces or task dumps on a realistic case |

This granularity lets the agent automate already-strong scheduling syntax while protecting cognitive work around cancellation and cleanup.
