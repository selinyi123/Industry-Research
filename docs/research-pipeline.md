# Research Pipeline

## 0. Research target

Each run starts from a research target containing at least an industry/topic, geographic scope, time horizon, and intended decision context when known.

## 1. Research Matrix / Ontology

Before broad search, expand the target into a structured research space.

Required dimensions:

- industry identity: canonical name, aliases, historical names, adjacent and confusable categories
- classifications: ISIC, NAICS, NACE, CPC, HS or other applicable codes
- geography: global, region, country, subnational where material
- value chain: inputs, components, manufacturing, distribution, customers, after-sales
- product and technology segments
- demand: customers, penetration, installed base, sales/shipments
- supply: production, capacity, utilization, supplier structure, import dependence
- economics: revenue, ASP, margin, CAPEX/OPEX, unit economics
- competition: participants, share, concentration, entry/exit
- regulation: standards, incentives, licensing, trade restrictions
- time: history, current state, forecast horizon, structural breaks
- evidence requirements: what would be sufficient to support each important conclusion

## 2. Industry Graph

Maintain explicit relationships among:

```text
Industry ↔ Subindustry ↔ Product ↔ Technology
        ↕                 ↕
Company ↔ Plant ↔ Country/Region ↔ Policy
        ↕
Supplier ↔ Raw Material ↔ Customer ↔ Event
```

Entity resolution must distinguish:

- clue
- high-probability association
- confirmed same entity

Do not collapse aliases or organizations without sufficient evidence.

## 3. Source Registry

Every source receives structured metadata before it is treated as evidence.

Suggested authority classes:

- **S** — government statistics, regulators, customs, exchange filings, formal standards, courts/legislation
- **A** — company filings and investor materials, industry associations, academic research, official databases, intergovernmental organizations
- **B** — established specialist research/database providers with identifiable methodology
- **C** — major consulting research and professional trade publications
- **D** — mainstream financial/news media and expert commentary
- **E** — report aggregators, generic market-size pages, opaque SEO research sites
- **Lead** — social media, forums, snippets, secondary mentions used only for discovery

Record `source_family_id` so syndicated or copied material is not miscounted as independent corroboration.

## 4. Multi-round Active Search

Search is adaptive rather than a fixed prompt chain.

Recommended modes:

1. **Discovery** — learn terminology, entities, datasets, and likely sources.
2. **Authority Search** — target primary and official sources.
3. **Report Search** — identify major reports, studies, and market analyses.
4. **Data Search** — retrieve tables, series, spreadsheets, APIs, and numerical evidence.
5. **Regional / Local-language Search** — search in local terminology and local engines/sources where relevant.
6. **Company / Value-chain Search** — work upstream and downstream through companies, suppliers, customers, and filings.
7. **Contradiction Search** — intentionally seek counterevidence, revisions, cancellations, declines, methodology criticism, and alternative estimates.
8. **Citation Chasing** — follow references back to original evidence; also search exact metrics/phrases to identify the earliest source.
9. **Gap Search** — search specifically for unresolved high-value evidence gaps.
10. **Saturation Test** — determine whether further search is producing meaningful independent evidence.

## 5. Search prioritization

Use a priority concept such as:

```text
Priority =
  Importance
  × Uncertainty
  × Contradiction
  × FreshnessNeed
  × ExpectedInformationGain
  ÷ AcquisitionCost
```

The formula is a policy heuristic, not a calibrated probability model. Individual factors should be normalized and documented if implemented numerically.

## 6. Acquisition

Each result enters the acquisition state machine. All attempts and terminal states are logged. See `acquisition-state-machine.md`.

## 7. Document processing

Persist:

- raw artifact
- cryptographic hash
- normalized text/structure
- source URL and retrieval time
- page, section, table, sheet, cell, or chart location
- parser/version metadata
- extraction records

Do not replace source artifacts with summaries.

## 8. Content judgment

Evaluate each candidate in sequence:

1. Relevance
2. Authenticity
3. Primaryness
4. Scope Match
5. Methodology
6. Novelty
7. Contradiction

Low-value duplicates may be retained in the ledger but excluded from evidence aggregation.

## 9. Metric normalization

Every important quantitative observation should preserve:

- metric name and definition
- value
- unit
- currency
- nominal vs real
- geography
- period
- historical / estimated / forecast status
- base year
- forecast horizon
- methodology
- evidence span
- source and source family

Never average values that have not been scope-normalized.

## 10. Claim-level verification

Split conclusions into atomic claims and link each claim to evidence. Verification status is explicit and may change as the research state evolves.

## 11. Conflict handling

Before treating values as conflicting, test differences in:

- time period
- geographic boundary
- product/segment boundary
- revenue vs GMV
- manufacturer vs distributor vs retail value
- currency and FX conversion
- nominal vs real prices
- historical vs estimate vs forecast
- fiscal vs calendar year

If conflict remains, preserve it. Do not manufacture consensus.

## 12. Temporal and causal analysis

Track revisions and events over time. Separate:

- observed fact
- correlation
- plausible causal mechanism
- unsupported causal narrative
- forecast

## 13. Evidence Gap Analysis

Maintain an explicit unknowns register. Each high-value unknown should contain:

- why it matters
- current evidence state
- what evidence would resolve it
- candidate sources/search strategies
- priority

These gaps drive the next active-search cycle.

## 14. Stopping rule

A research cycle can stop when high-priority gaps are resolved or when additional searching produces low expected information gain relative to cost. Stopping does not imply certainty; unresolved questions remain visible.

## 15. Continuous monitoring

Future runs compare the new state with the previous state and notify only when the delta is material. See `continuous-monitoring.md`.
