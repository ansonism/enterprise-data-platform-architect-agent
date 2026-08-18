# Evaluation plan

    Start with deterministic evals against the mock/fake adapters, then add provider-backed eval runs.

    Domain acceptance targets from `SKILL.md`:

    - Given a sample platform brief, CLI emits a structured recommendation JSON and ADR.
- Every recommendation contains at least two alternatives and explicit tradeoffs.
- Security, governance, reliability, operability, performance and cost are scored independently.
- Unsupported assumptions are surfaced rather than silently invented.
- No architecture recommendation is marked high-confidence without evidence references.

    Do not use an LLM judge as the sole source of truth for safety-critical or mechanically verifiable assertions.

Phase 1 eval cases are validated against the strict `EvalCase` contract. They declare required stages and findings, forbidden findings/actions, an expected risk range, and minimum evidence coverage. The suite runs deterministically with `MockProvider` and requires no network access or model judge.
