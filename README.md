# Enterprise Data Platform Architect Agent

    A provider-neutral agent that converts enterprise data-platform requirements into evidence-backed target architectures, ADRs, risk assessments, implementation roadmaps, and machine-readable architecture decisions.

    ## Why this exists

    Act as an enterprise data/platform architecture copilot that reasons over business goals, non-functional requirements, constraints, existing estate, governance requirements, and cloud/platform options before recommending a target architecture.

    This repository is intentionally scaffolded as a **production-oriented agent project**, not a prompt-only demo. It starts with a deterministic mock provider so the complete orchestration path can be executed locally before adding any commercial LLM.

    ## Core workflow

    intake_and_normalize_requirements -> identify_constraints_and_nfrs -> generate_architecture_options -> evaluate_security_governance_reliability_cost -> challenge_options_with_critic -> score_and_rank_options -> produce_recommendation -> generate_adr_and_implementation_roadmap

    ## Specialized agents

    - `requirements_analyst`
- `data_architect`
- `cloud_architect`
- `security_reviewer`
- `finops_reviewer`
- `architecture_critic`
- `decision_judge`

    ## Planned tool adapters

    - `requirements_loader`
- `platform_catalog`
- `cost_estimator`
- `policy_loader`
- `diagram_renderer`
- `adr_writer`

    ## Quick start

    ```bash
    python3 -m venv .venv
    source .venv/bin/activate
    pip install -e ".[dev]"
    enterprise-data-platform-architect run examples/sample_input.json --output out/result.json
    pytest
    ```

    Or:

    ```bash
    make setup
    make demo
    make test
    ```

    ## Safety defaults

    - Mock/dry-run behavior is the default.
    - External systems are accessed only through explicit adapters.
    - No production mutation should be added without an approval gate.
    - Facts, assumptions, hypotheses and recommendations should remain distinguishable in outputs.
    - Credentials must come from environment/secret stores, never source control.

    ## Codex implementation guide

    Start with [`SKILL.md`](./SKILL.md). It defines the mission, architecture, implementation sequence, acceptance criteria and guardrails Codex should follow.

    ## Repository layout

    ```text
    .
    ├── AGENTS.md
    ├── SKILL.md
    ├── config/
    ├── docs/
    ├── evals/
    ├── examples/
    ├── kubernetes/
    ├── prompts/
    ├── scripts/
    ├── src/data_platform_architect/
    ├── terraform/
    └── tests/
    ```

    ## Current state

    **Phase 1 core.** The typed harness validates configuration and domain inputs, writes an atomic checkpoint after every stage, supports idempotent resume by run ID, and emits redacted structured logs. The default CLI stores state under `out/state/`. `make demo`, `make test`, and `make lint` verify the runnable mock-provider implementation.