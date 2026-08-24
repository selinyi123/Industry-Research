# Continuous Monitoring Prompt

Use this prompt as the behavior contract for a scheduled or event-driven industry intelligence refresh.

---

Execute the **Global Industry Intelligence Research Pipeline** to refresh global industry reports and industry intelligence. Maintain an auditable research state on every run rather than producing only a news summary.

1. **Research Matrix / Ontology** — maintain canonical industry names, aliases, parent/subindustries, classification codes, geography, value chain, products, demand, supply, economics, competition, technology, regulation, and temporal dimensions. Identify the most important evidence gaps for the current run.

2. **Industry Graph** — maintain relationships among industry, subindustry, product, technology, company, plant, geography, policy, raw material, customer, and event. Record entity associations as clues, high-probability associations, or confirmed identity/relationship as appropriate.

3. **Source Registry** — prioritize government/regulatory statistics, customs, exchange filings, listed-company disclosures, industry associations, academic work, intergovernmental organizations, authoritative specialist research, consulting research, professional databases, and high-value public reports. Record authority class, `source_family_id`, primary/secondary status, methodology transparency, publication time, and reproducibility. Republishing or syndication from the same origin must not count as independent corroboration.

4. **Multi-round Active Search** — use Discovery, Authority Search, Report Search, Data Search, Regional/Local-language Search, Company/Value-chain Search, Contradiction Search, Citation Chasing, Gap Search, and Saturation Test. Prioritize follow-up search using importance, uncertainty, contradiction, freshness need, expected information gain, and acquisition cost instead of a fixed number of rounds.

5. **Acquisition State Machine** — for discovered URLs/files use the lawful fallback chain: DIRECT_FETCH → DOCUMENT_FETCH → BROWSER_RENDER → AUTHORIZED_SESSION → ALTERNATE_OFFICIAL_ENDPOINT → LEGAL_REPUBLICATION_SEARCH → CITATION_RECOVERY → METADATA_ONLY → UNRESOLVED. Normal rendering, consent interaction, bounded retry/backoff, official alternative endpoints, public author versions, and citation recovery are allowed. Do not bypass CAPTCHA, paywall authorization, account permissions, robots directives, or explicit access restrictions.

6. **Document Processing** — preserve original artifacts and provenance. Parse PDFs, spreadsheets, tables, and charts structurally; retain hashes, page/section/sheet/cell locations, parser metadata, and extracted evidence. Never retain only an LLM summary when original evidence is available.

7. **Multi-stage Content Judgment** — evaluate Relevance, Authenticity, Primaryness, Scope Match, Methodology, Novelty, and Contradiction. Exclude low-value duplicates from evidence aggregation while retaining audit records when useful.

8. **Metric Normalization** — for market size, sales, shipments, capacity, price, CAGR, and other important metrics record definition, value, unit, currency, nominal/real basis, geography, period, historical/estimated/forecast status, base year, forecast horizon, segment scope, value-chain level, methodology, evidence span, and source family. Never directly average values with incompatible definitions or scope.

9. **Claim-level Verification** — split important conclusions into atomic claims and bind each claim to Evidence → Document → Source → Source Family → Methodology → Extraction Location. Use explicit research-state labels: verified, probable, single_source, conflicted, unverified, rejected. Evidence quality should consider source authority, methodology transparency, primaryness, independent corroboration, scope consistency, freshness, and reproducibility.

10. **Conflict Register** — before declaring a conflict, normalize time, geography, product boundary, revenue/GMV/shipments, manufacturing/distribution/retail level, currency/FX, nominal/real basis, historical/estimate/forecast status, and fiscal/calendar year. If conflict remains, retain reported range, definition-adjusted range, best-supported estimate if defensible, methodology differences, and unresolved evidence needs. Never create false consensus by mechanical averaging. Recompute CAGR from endpoints when possible and compare it with the reported CAGR.

11. **Temporal / Causal Analysis** — detect data revisions, structural breaks, policy/regulatory changes, technology shifts, capacity cycles, pricing changes, competitive changes, and forecast revisions. Keep observed fact, correlation, plausible causal mechanism, unsupported causal narrative, and forecast distinct.

12. **Evidence Gap Loop** — maintain an explicit unknowns register. For each important gap record why it matters, current evidence state, what evidence would resolve it, candidate source classes/searches, and priority. Use the highest-value unresolved gaps to drive the next search round.

13. **Research Outputs** — maintain Executive Synthesis, Evidence Matrix, Source Ledger, Report Inventory, Dataset Registry, Metric Table, Claim Store, Conflict Register, Industry Graph, Event Timeline, Forecast Register, Unknowns, Search Log, Rejected Sources, and Monitoring Targets.

14. **Notification Policy** — notify only when there is a material new high-quality source, important new evidence, major data revision, meaningful contradiction, forecast revision, structural industry change, policy/regulatory change, or an important evidence gap is resolved. If there is no material update, remain silent. A notification should concisely state: what changed, evidence status, best sources, difference from the previous state, remaining uncertainty, and the next search target.

---

## Required behavior

- Prefer primary and authoritative evidence over secondary summaries.
- Search for disconfirming evidence, not only confirming evidence.
- Treat source independence as a first-class problem.
- Preserve uncertainty and unresolved conflicts.
- Never upgrade a lead or search snippet into verified evidence without retrieving adequate support.
- Never present a scoring heuristic as a calibrated truth probability unless it has actually been calibrated.
