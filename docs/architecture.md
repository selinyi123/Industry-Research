# Architecture

## Objective

Build a durable research system that can discover, acquire, verify, normalize, compare, and continuously refresh global industry intelligence while preserving provenance and unresolved uncertainty.

The architecture deliberately separates deterministic workflow control from probabilistic research reasoning.

## Logical components

```text
Scheduler / Trigger
      ↓
Research Orchestrator
      ↓
┌───────────────────────────────────────────────┐
│ Research Planner                              │
│ Query Generator                              │
│ Search Provider Adapters                     │
│ Acquisition Router                           │
│ Document Processor                           │
│ Entity / Metric / Claim Extractors           │
│ Evidence Resolver                            │
│ Skeptic / Verifier                           │
│ Conflict Resolver                            │
│ Gap Analyzer                                 │
│ Synthesizer                                  │
└───────────────────────────────────────────────┘
      ↓
Research State Store + Artifact Store
      ↓
Monitoring / Notifications
```

## Component boundaries

### 1. Research Orchestrator

Owns durable execution, retries, checkpoints, job identity, budgets, cancellation, and state transitions. These responsibilities should not be delegated to an LLM.

### 2. Research Planner

Expands a research target into a Research Matrix and Industry Graph. It identifies high-value unknowns, translates them into evidence requirements, and prioritizes follow-up work.

### 3. Query Generator

Produces queries by search mode: discovery, authority, report, data, regional/local-language, company/value-chain, contradiction, citation chasing, and gap search.

### 4. Search Provider Adapters

Normalize search results from multiple providers into a common candidate format. Provider-specific ranking is treated as a retrieval signal, not truth.

### 5. Acquisition Router

Attempts legal acquisition through the state machine defined in `acquisition-state-machine.md`. It records every attempt and failure reason.

### 6. Document Processor

Parses HTML, PDF, spreadsheet, table, and chart content while retaining original artifacts, hashes, page/section coordinates, and extraction metadata.

### 7. Extractors

Produce structured entities, relationships, metrics, events, forecasts, and atomic claims. Extraction is not equivalent to verification.

### 8. Evidence Resolver

Links claims and metrics to their exact evidence spans, source documents, source families, and methodologies.

### 9. Skeptic / Verifier

Actively searches for independent corroboration, contrary evidence, scope mismatch, stale data, methodological weakness, and hidden source dependence.

### 10. Conflict Resolver

Normalizes scope before comparing estimates and registers unresolved conflicts without forcing false consensus.

### 11. Gap Analyzer

Maintains the open-question set and prioritizes the next search using expected information gain rather than a fixed research depth.

### 12. Synthesizer

Produces human-facing research outputs from verified structured state. It may summarize evidence, but it must not mutate evidence provenance.

## Storage model

Recommended separation:

- **PostgreSQL**: research runs, sources, documents, claims, entities, relationships, conflicts, events, forecasts, search logs.
- **pgvector or equivalent**: semantic retrieval only; vector similarity must never be treated as evidence truth.
- **S3/MinIO-compatible object storage**: original PDFs, spreadsheets, snapshots, screenshots, normalized documents.
- **Parquet + DuckDB**: analytical processing of large metric tables and time series.

## Durable workflow vs agent reasoning

Use deterministic workflow logic for:

- retries and exponential backoff
- idempotency
- budget limits
- timeout handling
- checkpointing
- schema validation
- notification policy
- access-control decisions

Use model reasoning for:

- query expansion
- ontology refinement
- entity resolution hypotheses
- evidence interpretation
- contradiction diagnosis
- gap prioritization
- synthesis

## Core invariant

No final conclusion should exist only inside generated prose. Material conclusions must be reconstructable from structured claims and evidence records.
