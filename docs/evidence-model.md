# Evidence Model

## Principle

The unit of trust is not a document and not a generated paragraph. The system should preserve a chain from a material claim back to exact evidence, source identity, source family, methodology, and extraction location.

```text
Claim
  ↓ supported_by / contradicted_by
Evidence
  ↓ extracted_from
Document
  ↓ published_by
Source
  ↓ belongs_to
Source Family
```

Metrics, events, forecasts, and entity relationships may also be attached to evidence spans.

## Source

A source is a publisher, database, filing system, organization, company, authoring body, or other identifiable origin of information.

Recommended fields:

- `source_id`
- `name`
- `canonical_url`
- `authority_class`: S / A / B / C / D / E / Lead
- `source_family_id`
- `primaryness`
- `methodology_transparency`
- `jurisdiction`
- `language`
- `notes`

## Source Family

`source_family_id` represents common evidentiary origin.

Example: ten news stories that copy the same association press release are ten URLs but one source family for the copied claim.

Family relationships may include:

- direct republication
- syndicated article
- derived chart/table
- report citing same upstream dataset
- corporate group publication
- unknown relationship

Independence must be assessed at claim level when necessary. Two reports from the same publisher can still use independent datasets; two different publishers can depend on the same upstream dataset.

## Document

A document represents a retrievable publication or artifact.

Recommended fields:

- `document_id`
- title
- document type
- publisher/source ID
- publication date
- retrieval date
- canonical URL
- version/revision
- language
- geography
- raw object URI
- content hash
- parser and parser version
- access/acquisition state

## Evidence

Evidence is a bounded span inside a document or structured dataset.

Possible locations:

- HTML selector/section
- PDF page and bounding region
- spreadsheet sheet/cell range
- table ID and row/column
- API endpoint and observation keys
- figure/chart region

Recommended fields:

- `evidence_id`
- `document_id`
- extraction location
- verbatim or normalized evidence payload
- extraction method
- extraction timestamp
- parser/model version
- quality flags

## Claim

A claim should be atomic enough to verify independently.

Examples:

Good:

> Company A reported 2025 segment revenue of USD 4.2 billion.

Poor:

> Company A is the industry leader with strong growth and superior economics.

Recommended fields:

- `claim_id`
- statement
- claim type
- subject/entity IDs
- geography
- valid time / observation period
- status
- importance
- uncertainty
- supporting evidence IDs
- contradicting evidence IDs
- verification notes

Recommended statuses:

- `verified`
- `probable`
- `single_source`
- `conflicted`
- `unverified`
- `rejected`

These statuses are research-state labels, not calibrated probabilities.

## Metric

Quantitative observations require explicit scope.

Recommended fields:

- `metric_id`
- metric name
- definition
- value
- unit
- currency
- price basis: nominal / real / not_applicable / unknown
- geography
- period start/end
- observation type: historical / estimate / forecast
- base year
- forecast horizon
- segment/product scope
- value-chain level
- methodology
- evidence ID
- source family ID

## Forecast

Forecasts must retain who predicted what and when.

Recommended fields:

- forecast ID
- metric/claim target
- forecaster/source
- publication date
- base year
- target year
- point/range estimate
- assumptions
- methodology
- evidence
- later realization links

This allows forecast accuracy to be evaluated after the fact.

## Conflict

A conflict record is created only after scope normalization fails to reconcile materially different claims or metrics.

Recommended fields:

- `conflict_id`
- participating claim/metric IDs
- comparison scope
- suspected causes
- reported range
- definition-adjusted range
- best-supported estimate, if justified
- resolution status
- resolution rationale

## Research Gap

An evidence gap is a first-class object, not an absence hidden from the report.

Recommended fields:

- `gap_id`
- question
- why it matters
- affected claims/decisions
- current evidence state
- required resolving evidence
- candidate source classes
- candidate searches
- importance
- uncertainty
- contradiction
- freshness need
- acquisition cost estimate
- expected information gain
- priority
- status

## Provenance invariant

For every material claim in an executive synthesis, the system should be able to answer:

1. Which evidence supports it?
2. Where exactly is that evidence located?
3. Who originally produced the information?
4. Is corroborating evidence truly independent?
5. What methodology produced the figure or conclusion?
6. What contrary evidence exists?
7. What uncertainty remains?
