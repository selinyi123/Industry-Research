# Continuous Monitoring

## Goal

Continuous monitoring should update a persistent research state rather than re-run a full generic research prompt and emit a fresh summary every day.

Each run compares new evidence with the previous accepted state and focuses work on material deltas and unresolved evidence gaps.

## Monitoring inputs

Maintain at least:

- tracked industries and subindustries
- tracked entities and source families
- known authoritative datasets
- current metric observations
- open claims
- conflict records
- evidence gaps
- forecast register
- event timeline
- prior search log
- rejected-source fingerprints

## Incremental cycle

```text
Load Previous Research State
        ↓
Refresh High-value Sources
        ↓
Discover New Sources / Reports
        ↓
Acquire + Parse
        ↓
Extract New Claims / Metrics / Events
        ↓
Verify + Normalize + Resolve Conflicts
        ↓
Diff Against Previous State
        ↓
Update Evidence Gaps
        ↓
Active Follow-up Search
        ↓
Persist New State
        ↓
Materiality Gate
        ↓
Notify or Stay Silent
```

## Materiality gate

A notification should normally require one or more of:

- a newly discovered high-quality report or dataset with material information
- an official statistical revision
- a previously important evidence gap resolved
- a high-impact claim changing verification status
- a new credible contradiction
- a meaningful forecast revision
- a structural change in industry organization or value chain
- a material policy/regulatory change
- a major company action with industry implications
- a key metric moving beyond a configured materiality threshold

Routine duplicates, SEO summaries, minor article rewrites, and same-source republications should not trigger notification.

## Notification contract

A useful monitoring notification should state:

1. **What changed** — the new conclusion or material evidence.
2. **Evidence state** — verified/probable/single-source/conflicted/etc.
3. **Best sources** — preferably primary or high-authority evidence.
4. **Delta** — how this differs from the prior research state.
5. **Remaining uncertainty** — what is still unresolved.
6. **Next search target** — the highest-value follow-up gap.

## Freshness policy

Freshness need depends on the object:

- prices, outages, policy announcements, company events: high freshness
- quarterly filings and shipment data: periodic freshness
- classification definitions and standards: change-driven freshness
- historical datasets: revision-driven freshness

Do not treat publication date alone as evidence quality. A recent secondary article may be less useful than an older primary dataset that defines the metric correctly.

## Search saturation

A monitoring cycle may stop when:

- refreshed priority sources show no material delta
- high-priority gaps have no new resolvable evidence
- additional search mainly returns duplicates or dependent sources
- expected information gain falls below the run's cost threshold

The system should record why it stopped.

## State diff examples

Track transitions such as:

```text
claim: single_source → verified
claim: probable → conflicted
metric: 2025 estimate revised from 12.1 to 10.8
forecast: 2030 target revised downward 18%
source: authority class changed after methodology disclosure
conflict: unresolved → resolved
research_gap: open → resolved
entity_relationship: clue → confirmed
```

These transitions are more informative than a new prose summary with no explicit comparison.
