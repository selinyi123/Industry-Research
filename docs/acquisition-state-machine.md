# Acquisition State Machine

## Purpose

Research systems fail if every blocked page becomes either a hard failure or an instruction to bypass access controls. Acquisition should instead be modeled as an auditable state machine that attempts legitimate alternative paths and records why acquisition succeeded or failed.

## State sequence

```text
URL_DISCOVERED
      ↓
DIRECT_FETCH
      ↓
DOCUMENT_FETCH
      ↓
BROWSER_RENDER
      ↓
AUTHORIZED_SESSION
      ↓
ALTERNATE_OFFICIAL_ENDPOINT
      ↓
LEGAL_REPUBLICATION_SEARCH
      ↓
CITATION_RECOVERY
      ↓
METADATA_ONLY
      ↓
UNRESOLVED
```

A state may terminate successfully; the sequence is a fallback order, not a requirement to execute every state.

## States

### URL_DISCOVERED

Create a candidate record with discovery query, rank, title/snippet if available, referring source, and timestamp.

### DIRECT_FETCH

Attempt standard HTTP retrieval where permitted. Record status code, content type, redirects, and retrieval timestamp.

### DOCUMENT_FETCH

If the target is a downloadable document or data artifact, retrieve the native PDF, XLS/XLSX, CSV, ZIP, JSON, XML, or other supported representation rather than relying on rendered snippets.

### BROWSER_RENDER

Use normal browser rendering for JavaScript-driven pages. Ordinary Cookie/Consent interaction is allowed when it does not grant access beyond what the user is entitled to access.

### AUTHORIZED_SESSION

Use an already authorized session only when the system/user has legitimate access. Never fabricate, steal, or circumvent credentials or account restrictions.

### ALTERNATE_OFFICIAL_ENDPOINT

Search for official APIs, print views, export endpoints, press-release mirrors, filing databases, data portals, or alternative official publications carrying the same evidence.

### LEGAL_REPUBLICATION_SEARCH

Look for lawful public versions such as author manuscripts, institutional repositories, government mirrors, conference versions, or explicitly republished copies.

### CITATION_RECOVERY

If the desired document cannot be acquired, follow its visible citations or secondary references to recover the original data or claim from another legitimate source.

### METADATA_ONLY

Retain title, publisher, date, DOI/report identifier, abstract/snippet, and acquisition-failure reason. Metadata-only material is a lead, not full-text evidence unless the claim is directly supported by the available metadata.

### UNRESOLVED

Stop. Record the reason and optionally create an evidence gap or manual-review target.

## Failure classification

Normalize failures so policy can distinguish remediation paths:

- `javascript_required`
- `cookie_consent`
- `rate_limited`
- `temporary_server_error`
- `not_found`
- `moved_or_renamed`
- `authentication_required`
- `subscription_required`
- `captcha_required`
- `robots_disallowed`
- `explicit_access_denial`
- `geo_restriction`
- `unsupported_format`
- `parse_failure`
- `unknown`

## Retry policy

Retries should be deterministic and bounded.

- rate limits: exponential backoff with jitter
- temporary 5xx failures: bounded retry
- parse failures: alternate parser before re-downloading when possible
- permanent 4xx access denial: do not brute-force retry
- CAPTCHA: stop automated access path and pursue alternative public evidence

## Prohibited behavior

The acquisition layer must not:

- bypass CAPTCHA challenges
- defeat paywall authorization
- evade account permissions
- defeat explicit robots restrictions
- rotate identities/proxies for the purpose of circumventing access denial
- exploit vulnerabilities to retrieve protected material

The desired capability is **information-path recovery**, not access-control circumvention.

## Provenance requirements

Each acquisition attempt records:

- candidate/source ID
- state
- start/end timestamps
- request target
- result status
- response metadata
- content hash when acquired
- failure classification
- parent attempt
- authorization context category, without storing secrets

This history makes later evidence auditing and reproducibility possible.
