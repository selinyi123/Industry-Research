# Verification and Conflict Resolution

## Verification is claim-level

A document may contain both reliable and weak assertions. Verification therefore operates on atomic claims and metrics rather than assigning a single truth score to an entire report.

## Evidence quality dimensions

A practical evidence-quality model may consider:

- source authority
- methodology transparency
- primaryness
- independent corroboration
- scope consistency
- freshness
- reproducibility

A numeric score may be useful for ranking, but it must not be presented as a probability that the claim is true unless the score has actually been calibrated as such.

## Suggested internal weighting

One initial policy can be:

| Dimension | Weight |
|---|---:|
| Source authority | 25 |
| Methodology transparency | 20 |
| Primaryness | 15 |
| Independent corroboration | 15 |
| Scope consistency | 10 |
| Freshness | 10 |
| Reproducibility | 5 |

These weights are defaults to be tested, not universal truth.

## Verification statuses

### `verified`

Material claim is supported by sufficiently strong evidence and, where appropriate, independent corroboration with compatible scope.

### `probable`

Evidence is strong but incomplete, partially dependent, or missing one important validation dimension.

### `single_source`

Claim is directly supported, but only one source family is available.

### `conflicted`

Credible evidence sources materially disagree after reasonable normalization.

### `unverified`

Claim has insufficient evidence or is only present in weak/indirect material.

### `rejected`

Claim is contradicted by stronger evidence, based on invalid methodology, unsupported by the cited source, or outside the defined research scope.

## Independence check

Before counting two pieces of support as corroboration, inspect whether they share:

- the same original dataset
- the same press release
- the same analyst estimate
- the same association table
- the same syndicated article
- a direct citation relationship

Multiple URLs do not imply multiple independent observations.

## Quantitative conflict workflow

Given several estimates for the same apparent metric:

1. Normalize time period.
2. Normalize geography.
3. Normalize product/segment definition.
4. Normalize value-chain level.
5. Distinguish revenue, GMV, shipments, installed base, capacity, production, etc.
6. Normalize currency and exchange-rate basis.
7. Distinguish nominal and real prices.
8. Distinguish historical, estimated, and forecast values.
9. Normalize fiscal/calendar year conventions.
10. Inspect methodology and upstream data dependence.

Only after these checks should values be considered genuinely conflicting.

## Conflict Register output

For unresolved conflicts, store:

- all reported values
- exact definitions
- source families
- methodology differences
- reported range
- definition-adjusted range
- best-supported estimate, if one is defensible
- reason for preferring or not preferring an estimate
- remaining evidence needed

Never manufacture a consensus by averaging incompatible figures.

## CAGR validation

When a report states start value, end value, number of periods, and CAGR, recompute CAGR independently.

If the reported CAGR differs, determine whether the discrepancy arises from:

- inclusive/exclusive period counting
- rounded endpoint values
- hidden intermediate assumptions
- currency conversion
- data revision
- report error

Preserve both the reported and recomputed values when materially different.

## Contradiction search

A verification pass should intentionally search for evidence that could falsify or weaken an important claim.

Common query patterns include combinations of the target with:

- revised
- cancelled
- delayed
- decline
- methodology
- correction
- restatement
- investigation
- alternative estimate
- criticism

The purpose is to reduce confirmation bias, not to force a negative conclusion.

## Causal claims

Treat causal language separately from descriptive facts.

A claim such as “policy X caused demand to rise” should preserve:

- observed timing
- mechanism
- competing explanations
- confounders
- supporting studies or natural experiments if available
- confidence/verification status

Correlation alone must not be rewritten as causation.
