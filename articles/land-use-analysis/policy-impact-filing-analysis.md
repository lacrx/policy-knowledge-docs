---
title: Proving Policy Impact via Filing Analysis
topics:
  - land-use-analysis
  - density-caps
  - permit-analysis
  - obstruction-patterns
  - policy-impact
summary: >
  Three-check methodology for proving a land use policy killed development
  activity, using permit filing data with geographic and temporal controls.
aliases:
  - filing freeze analysis
  - density cap impact
  - development application analysis
  - permit filing methodology
related:
  - apr-proposal-estimation
  - ca-housing-enforcement
last-updated: 2026-07-18
---

# Proving Policy Impact via Filing Analysis

## The Question

When a jurisdiction adopts a restrictive land use policy (density cap, moratorium, downzoning), advocates need to prove it chilled development. Correlation alone is insufficient — you need to rule out alternative explanations (market downturn, regional trend, data gap). This methodology uses permit filing data with geographic and temporal controls to build an airtight case.

## Three-Check Validation

The core technique isolates the policy's effect by testing three conditions. All three must hold for the finding to be credible.

### Check 1: Prior Years, Same Geography

Establish that development applications were being filed in the affected area before the policy took effect. This rules out "nobody was filing there anyway."

- Pull filing data for the affected geography for 3-5 years before the policy.
- Show a baseline of activity — ideally with an upward trend if the policy was adopted in response to increased development.
- Note the volume: if the area had 20+ filings/year before and zero after, the signal is strong.

### Check 2: Same Year, Different Geography

Establish that development applications are still being filed in the same jurisdiction, outside the affected area. This rules out citywide market downturn, regional economic conditions, or a data pipeline failure.

- Pull filing data for the same time period, same jurisdiction, excluding the affected geography.
- Show that filings continue at normal or elevated rates elsewhere.
- If filings dropped everywhere, the policy may not be the cause — investigate further.

### Check 3: Same Year, Same Geography

Confirm zero (or near-zero) filings in the affected area after the policy took effect. This is the finding itself, but it only has meaning after Checks 1 and 2 establish the counterfactual.

- Pull filing data for the affected geography for the period after the policy.
- Distinguish between genuinely new applications and extensions/modifications of pre-existing entitlements — time extensions (EXT) and site plan compliance (SC) on old projects are not new filings.
- Note any applications that used SB 330 vesting to lock in pre-policy standards — these confirm developers knew the policy would make projects infeasible.

## Data Sources

### Etrakit / Permit Tracking Systems

Municipal permit tracking systems (eTrakit, Accela, OpenGov) are the authoritative source for when an application was filed. Each record typically includes:
- **Application number** with year prefix (e.g., RD24-00007 = Development Plan filed 2024)
- **Applied date** — the actual filing date
- **Address and APN** — for geographic filtering
- **Description** — project type and unit count
- **Status** — pending, approved, denied, withdrawn

These systems capture ministerial and discretionary applications at time of submission, before they reach any hearing body.

### HCD Annual Progress Report (Table A)

Gov. Code § 65400 requires cities to report annually on housing applications. Table A includes `APP_SUBMIT_DT`, unit counts by income category, and `UNIT_CAT` (ADU/SFD/2-4/5+). Covers the prior calendar year; typically filed by April 1. Use for cross-referencing etrakit data and for income-level breakdowns not available in etrakit.

**Limitation**: APR data is 6-18 months stale. For current-year analysis, rely on etrakit.

### Meeting Records

Council and commission agendas/minutes capture projects after they reach a hearing. These are NOT filing records — a project filed in 2023 may not appear in meeting records until 2025. Never use meeting records alone to determine when an application was filed. Use application number year prefixes or etrakit data instead.

## Geographic Filtering

Downtown districts, specific plan areas, and overlay zones require careful geographic definition. Methods:

- **Street-based**: Define downtown by its boundary streets. Requires local knowledge.
- **APN-based**: Use assessor parcel numbers if available in filing data. Most precise.
- **Zoning-based**: Filter by zoning designation (e.g., D-1 through D-5 for downtown subdistricts).
- **Application number context**: Some jurisdictions use application types that imply location (e.g., Regular Coastal Permit = coastal zone).

Cross-reference multiple methods when possible. A project at "Mission Avenue" could be downtown or on the Mission Avenue corridor miles inland.

## Interpreting the Zero

A zero-filing finding after a policy change is strong evidence, but consider:

- **SB 330 vesting**: Projects filed before the policy with SB 330 preliminary applications (Gov. Code § 65589.5) locked in pre-policy standards. A wave of SB 330 filings immediately before the policy confirms developers anticipated the freeze.
- **Time extensions**: Extensions on pre-policy entitlements show developers protecting existing approvals — they can't file new ones.
- **Affordable-only filings**: If the only new filings are 100% affordable projects (which may be exempt from density caps via state density bonus law), this confirms the cap is the binding constraint on market-rate development.
- **Small-project-only filings**: If only projects small enough to fit under the cap are filing, the cap is the binding constraint on larger projects.

## Presenting the Finding

Structure the analysis as:

1. **Timeline**: When the policy was proposed, adopted, and certified (if coastal zone / LCP amendment required).
2. **Before**: Filing volume by year in the affected area, showing baseline.
3. **Control**: Filing volume in the same period outside the affected area, showing the pipeline works.
4. **After**: Zero or near-zero filings in the affected area, with breakdown of what the remaining activity actually is (extensions, modifications, small projects).
5. **Duration**: Months since last genuine filing — the longer the freeze, the stronger the evidence.

## Limitations

- Filing data measures applications, not housing built. A jurisdiction could have a healthy filing pipeline but deny everything — that requires a different analysis.
- Some policies have delayed effects. A downzoning may not freeze filings immediately if developers take time to reassess feasibility.
- Ministerial approvals (ADUs, SB 9 lot splits) may not appear in discretionary project tracking systems. Use building permit data or ADU-specific tracking for those.
- This methodology proves correlation with strong controls but cannot establish causation with certainty. Developer interviews, feasibility analyses, and economic modeling strengthen the causal argument.
