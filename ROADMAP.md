# Roadmap

The repository begins protocol-first. Implementation should preserve the evidence and provenance contracts before optimizing search volume or agent sophistication.

## Phase 0 — Protocol and contracts

Status: **initial specification committed**

- [x] Define end-to-end research pipeline
- [x] Define acquisition fallback state machine
- [x] Define source-family independence concept
- [x] Define claim-level verification states
- [x] Define metric scope requirements
- [x] Define continuous monitoring and materiality gate
- [x] Add initial Source, Claim, Metric, and ResearchRun schemas
- [ ] Add Document, Evidence, Conflict, ResearchGap, Entity, Relationship, Event, and Forecast schemas
- [ ] Add schema fixtures and validation tests

## Phase 1 — Minimal auditable research engine

Goal: one industry target can run end to end while preserving full provenance.

- [ ] Research target input contract
- [ ] Research Matrix builder
- [ ] Industry Graph seed builder
- [ ] Source Registry persistence
- [ ] Search-provider adapter interface
- [ ] Query-mode planner
- [ ] Acquisition router
- [ ] HTML/PDF/spreadsheet parser interface
- [ ] raw artifact hashing and object storage
- [ ] claim/metric/evidence extraction
- [ ] claim-to-evidence resolver
- [ ] Search Log and Rejected Sources ledger
- [ ] deterministic run checkpoints

Exit criterion: a material claim in the final synthesis can be traced to an exact evidence location and source family.

## Phase 2 — Verification and contradiction engine

- [ ] source-family/entity resolution
- [ ] independent corroboration detection
- [ ] scope-compatibility checks
- [ ] metric normalization rules
- [ ] CAGR recomputation
- [ ] contradiction-search planner
- [ ] Conflict Register
- [ ] claim status transition engine
- [ ] evidence-quality scoring policy with explicit non-probabilistic semantics

Exit criterion: incompatible market estimates are diagnosed and preserved instead of silently averaged.

## Phase 3 — Active search and gap-driven research

- [ ] Evidence Gap object and persistence
- [ ] expected-information-gain heuristic
- [ ] adaptive query selection
- [ ] regional/local-language expansion
- [ ] citation chasing and upstream-source recovery
- [ ] saturation test
- [ ] search budget/cost policy

Exit criterion: the engine can explain why the next query is worth running and why a research cycle stopped.

## Phase 4 — Continuous monitoring

- [ ] persistent prior-state loading
- [ ] high-value source refresh scheduler
- [ ] state diff engine
- [ ] forecast revision tracking
- [ ] official-data revision detection
- [ ] materiality gate
- [ ] notification formatter
- [ ] silent-run behavior when no material delta exists

Exit criterion: repeated runs report meaningful changes rather than regenerate near-duplicate summaries.

## Phase 5 — Document intelligence

- [ ] native PDF structure extraction
- [ ] table extraction with coordinates
- [ ] spreadsheet cell-level provenance
- [ ] chart/figure extraction
- [ ] parser fallback routing
- [ ] document-version comparison

Candidate technologies to evaluate rather than assume: Docling and equivalent structured-document parsers.

## Phase 6 — Acquisition adapters

Implement provider adapters behind stable internal contracts. Candidate technologies may include browser automation and research-focused crawlers, but provider choice must remain replaceable.

Candidates to evaluate:

- Firecrawl
- Crawl4AI
- browser/Playwright-based rendering
- official API/data portal adapters

Do not let crawler-specific response shapes leak into the evidence domain model.

## Phase 7 — Research orchestration

- [ ] durable execution and retries
- [ ] idempotent tasks
- [ ] checkpoint/resume
- [ ] per-run budgets
- [ ] concurrency policy
- [ ] model/provider abstraction
- [ ] deterministic schema validation at agent boundaries

Candidate reasoning/workflow components may include LangGraph-style stateful agent graphs, but job durability, retries, permissions, and persistence should remain explicit system responsibilities.

## Phase 8 — Evaluation

Build a benchmark set of industry-research questions containing:

- known primary sources
- deliberate syndicated-source traps
- incompatible market-size definitions
- revised official statistics
- misleading CAGR claims
- stale forecasts
- entity aliases
- contradictory credible reports
- inaccessible source with recoverable upstream citation

Evaluate:

- primary-source recall
- source-family independence precision
- claim-evidence grounding
- metric scope accuracy
- contradiction detection
- false consensus rate
- citation/provenance completeness
- gap prioritization quality
- monitoring signal-to-noise ratio
- cost and latency

## Phase 9 — Production hardening

- [ ] observability
- [ ] audit logs
- [ ] secrets isolation
- [ ] access-control policy
- [ ] retention policy
- [ ] artifact integrity checks
- [ ] migrations/versioned schemas
- [ ] backfill strategy
- [ ] failure recovery drills
- [ ] reproducible research-run export

## Non-goals

The project should not optimize for:

- producing the longest possible report
- maximizing number of URLs
- treating all search results as equivalent sources
- bypassing access controls
- hiding conflicts for narrative simplicity
- using LLM confidence as evidence confidence

## Near-term implementation order

1. Complete core schemas and fixtures.
2. Implement persistence and provenance first.
3. Add one search provider and one direct-fetch acquisition path.
4. Add HTML + PDF extraction.
5. Implement claim/metric extraction and exact evidence linking.
6. Add verification and source-family deduplication.
7. Add gap-driven follow-up search.
8. Only then expand crawler/provider breadth and agent autonomy.
