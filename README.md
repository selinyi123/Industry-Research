# Industry Research

A provenance-first, evidence-driven workflow for global industry intelligence research.

This repository formalizes the **Global Industry Intelligence Research Pipeline** developed for long-running industry report discovery, verification, normalization, contradiction handling, and continuous monitoring.

The system is designed around one principle:

> Do not optimize for “searching longer”. Maintain an auditable research state that knows what is verified, what conflicts, what remains unknown, and what should be searched next.

## Core pipeline

```text
Research Matrix / Ontology
        ↓
Industry Graph
        ↓
Source Registry
        ↓
Multi-round Active Search
        ↓
Acquisition State Machine
        ↓
Document Processing + Provenance
        ↓
Multi-stage Content Judgment
        ↓
Metric Normalization
        ↓
Claim-level Verification
        ↓
Conflict Register
        ↓
Temporal / Causal Analysis
        ↓
Evidence Gap Analysis
        ↺
Continuous Monitoring
```

## Repository structure

- `docs/architecture.md` — system architecture and component boundaries
- `docs/research-pipeline.md` — end-to-end research workflow
- `docs/acquisition-state-machine.md` — resilient and lawful acquisition fallback chain
- `docs/evidence-model.md` — source, evidence, claim, metric, and provenance model
- `docs/verification-and-conflict.md` — claim verification and conflict resolution rules
- `docs/continuous-monitoring.md` — incremental monitoring behavior and notification policy
- `spec/` — machine-readable JSON Schemas for core research entities
- `prompts/continuous-monitoring.md` — reusable monitoring task prompt
- `ROADMAP.md` — implementation roadmap

## Research outputs

A mature research run should maintain at least:

- Executive Synthesis
- Evidence Matrix
- Source Ledger
- Report Inventory
- Dataset Registry
- Metric Table
- Claim Store
- Conflict Register
- Industry Graph
- Event Timeline
- Forecast Register
- Unknowns / Evidence Gaps
- Search Log
- Rejected Sources
- Monitoring Targets

## Design constraints

1. Independent corroboration is counted by **source family**, not by number of URLs.
2. Conflicting market numbers are never mechanically averaged before scope normalization.
3. Every material conclusion should be reducible to atomic claims with evidence and extraction locations.
4. Original documents and provenance are retained; LLM summaries are not treated as source evidence.
5. Search depth is adaptive and driven by information gaps rather than a fixed number of rounds.
6. Access recovery must remain lawful: no bypassing CAPTCHA, paywall authorization, account permissions, robots directives, or explicit access controls.
7. Facts, correlations, causal hypotheses, and forecasts must remain distinguishable.

## Status

This repository currently defines the research protocol and data contracts. The next phase is to implement the orchestration, acquisition adapters, parsers, evidence store, verification engine, and monitoring runtime described in `ROADMAP.md`.
