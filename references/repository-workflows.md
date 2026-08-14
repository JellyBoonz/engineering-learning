# Repository workflow patterns

Use these patterns as adaptations, not scripts. Classify work by the declared target before applying them.

## Contents

- Feature work
- Debugging
- Code review
- Refactoring
- Production incident
- Architecture decision
- Complete example

## Feature work

Example target: API idempotency semantics.

- Automate: repository search, endpoint inventory, fixture construction, mechanical wiring, formatting.
- Explore: ask the user to predict duplicate-request behavior and explain the consistency boundary.
- Apply: let the user select the idempotency key scope and implement the critical storage/transaction slice; provide a hint ladder.
- Execute: after transfer evidence, implement analogous endpoints directly and ask for concise review.
- Check transfer: change from synchronous response replay to asynchronous job creation and ask what must remain invariant.

## Debugging

Example target: diagnosing a distributed cache race.

- Automate: collect logs, find call sites, reproduce the failure, reduce noisy output.
- Protect: hypothesis formation and interpretation of target-related evidence.
- Explore: have the user trace one request and predict the race window.
- Apply: ask for the next discriminating experiment before running it.
- Reveal progressively: observations, narrowed component, violated invariant, then diagnosis.
- Check transfer: present a nearby race with a different interleaving.

Do not immediately fix every error. Preserve errors that provide safe, relevant evidence. Immediately handle unrelated setup failures and dangerous conditions.

## Code review

Example target: authorization-boundary reasoning.

- Automate: diff summary, call graph discovery, test lookup, style and mechanical checks.
- Explore: ask which trust boundary is crossed and what invariant should hold.
- Apply: let the user identify high-impact findings before showing the full review.
- Execute: draft all findings once the user demonstrates stable reasoning.
- Check transfer: ask whether the same flaw exists in a sibling endpoint with a different caller.

Never hide a security finding for assessment purposes. Surface it immediately, then use the explanation as the learning event.

## Refactoring

Example target: dependency direction and module boundaries.

- Automate: symbol inventory, call-site enumeration, mechanical moves, import fixes.
- Protect: boundary selection, invariant definition, and sequencing strategy.
- Explore: compare current and desired dependency direction.
- Apply: have the user choose the seam and identify a characterization test.
- Execute: perform repetitive moves and validation.
- Check transfer: ask where a new adjacent responsibility should live and why.

## Production incident

Default to the escape hatch when urgency is credible.

- Execute mitigation, evidence collection, rollback, or safe patching within authorization.
- Keep explanations terse during impact.
- Do not use a live incident as a quiz.
- Record which diagnostic or implementation operations the agent owned.
- After stabilization, reconstruct one decision point, explain the mechanism, and propose a sandboxed transfer exercise.
- Maintain honest competency levels; observing the agent is not independent performance.

## Architecture decision

Example target: consistency and failure-mode tradeoffs.

- Automate: locate constraints, summarize existing patterns, gather operational evidence, draft decision structure.
- Explore: elicit the user's model and compare two concrete failure scenarios.
- Apply: make the user own the decisive tradeoff and articulate rejected alternatives.
- Execute: draft the decision record and implementation plan after the choice.
- Check transfer: change one constraint—latency, availability, volume, or reversibility—and ask whether the decision changes.

## Complete example: cancellation-safe retries

User request:

> Add retry behavior to this worker. I know HTTP but need to learn our async runtime and cancellation semantics. Help me ship it today.

Contract:

- Delivery: bounded retries with cancellation-safe backoff and tests.
- Targets: cancellation propagation; retry boundary design.
- Incidental: locate worker, inspect conventions, build fixtures, run tests, format.
- Starting modes: Explore cancellation; Apply retry policy.

Sequence:

1. Search the repository, map the worker path, and summarize existing retry and cancellation conventions without asking the user to do tool work.
2. Ask: “If cancellation arrives during backoff, what should the caller observe, and which layer owns that outcome?”
3. Correct only the minimum conceptual gap: cancellation is a control signal, not an ordinary retryable failure.
4. Ask the user to identify the catch boundary and choose whether the delay must be cancellation-aware.
5. Generate fixtures and boilerplate. Let the user author or specify the critical exception classification branch.
6. Run tests. If a cancellation test fails, ask for one diagnosis before giving an orienting hint.
7. Complete unrelated type, formatting, and fixture fixes directly.
8. Transfer check: “If three requests run concurrently and one child is cancelled, which tasks should stop under our ownership model?”
9. Close with delivery verification and separate competency updates for propagation, exception classification, and structured child lifetime.

Urgent variant:

If the user says “just ship it,” implement and verify the entire change. Then state that no independent implementation evidence was collected, give the two-minute cancellation model, and suggest diagnosing or adapting the next retry site as the recovery exercise.
