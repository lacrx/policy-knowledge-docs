---
name: evaluate-crash-study
title: Evaluate a Transportation Safety Study
type: skill
topics:
  - transportation-safety
  - crash-data
summary: >
  Step-by-step checklist to evaluate a crash study or safety claim against proper epidemiological and engineering standards. Pass/fail per item with overall verdict.
references:
  - articles/transportation-safety/crash-data-methodology.md
last-updated: 2026-06-28
---

# Evaluate a Transportation Safety Study

Run a structured evaluation of a crash study, safety claim, or council presentation
against the methodology checklist. Produces a pass/fail scorecard.

---

## Prerequisites

- The study, report, presentation, or claim to evaluate
- Author name(s) and affiliations
- The specific conclusion being drawn (e.g., "bike lanes increased crashes by X%")

---

## Steps

### Step 1: Identify the claim

State the specific safety claim in one sentence:
- What infrastructure or intervention?
- What outcome is claimed? (increase/decrease in crashes, injuries, fatalities)
- What magnitude? (percentage, count, rate)
- What action is recommended? (build, remove, modify, delay)

### Step 2: Check author credentials

Search for the author(s) in:
- Google Scholar — look for publications in transportation safety journals
- University faculty directories — appointment in transportation, public health, or planning
- Professional licenses — PE in transportation/traffic engineering

**Score:**
- [ ] **PASS**: Published in peer-reviewed transportation safety journals
- [ ] **FAIL**: No transportation safety publications; credentials in unrelated field
- [ ] **FLAG**: Affiliated with vehicular cycling organizations (CyclingSavvy, LAB instructor certification without research record)

### Step 3: Check denominator / exposure

Does the study report crash **rates** or raw **counts**?

- [ ] **PASS**: Reports per-trip, per-mile, or per-rider crash rates with ridership data
- [ ] **FAIL**: Reports only raw crash counts with no ridership denominator
- [ ] **FAIL**: Claims "X% increase in crashes" without controlling for ridership changes

If FAIL: the study cannot make safety conclusions. Note this and continue evaluation.

### Step 4: Check statistical testing

- [ ] **PASS**: Reports significance test (chi-square, Poisson, etc.) with p-values or confidence intervals
- [ ] **FAIL**: No statistical test applied — percentage changes are anecdotal
- [ ] **FLAG**: Sample size < 50 crashes (underpowered for most designs)

### Step 5: Check study design

- [ ] **PASS**: Before-after longitudinal design on the same corridor
- [ ] **PARTIAL**: Cross-sectional comparison (different corridors) — weaker, note confounders
- [ ] **FAIL**: N=1 case report generalized to the category
- [ ] **FAIL**: Ecological study (city-level) used to draw corridor-level conclusions

### Step 6: Check data source integrity

- [ ] **PASS**: Uses SWITRS/TIMS/CCRS, EMS dispatch, or hospital records consistently across periods
- [ ] **FAIL**: Mixes crowdsourced data (Facebook, self-reports) with official data
- [ ] **FAIL**: Different data sources used for before vs. after periods
- [ ] **FLAG**: Does not acknowledge police report under-capture (40-92% of bicycle crashes missing)

### Step 7: Check confounder controls

Does the study account for:
- [ ] Ridership/exposure changes (e-bike adoption, COVID, seasonal)
- [ ] Vehicle speed and volume changes
- [ ] Road geometry changes
- [ ] Demographic shifts in road users

**Score:**
- [ ] **PASS**: Controls for ≥3 major confounders
- [ ] **PARTIAL**: Acknowledges confounders but doesn't control
- [ ] **FAIL**: No confounder discussion

### Step 8: Check crash type accounting

- [ ] **PASS**: Reports ALL crash types (vehicle-bicycle, solo, ped, intersection, mid-block)
- [ ] **FAIL**: Reports only infrastructure-caused crashes (bollard hits) without comparing to prevented crashes
- [ ] **FAIL**: Excludes intersection crashes (where most fatalities occur)

### Step 9: Check control comparison

- [ ] **PASS**: Uses a comparable control corridor or time period
- [ ] **PARTIAL**: Control exists but differs significantly from treatment
- [ ] **FAIL**: No control — treatment corridor compared only to itself with no baseline

### Step 10: Render verdict

Count PASS, PARTIAL, FAIL, FLAG across steps 2-9.

| Result | Criteria |
|--------|----------|
| **Credible** | 6+ PASS, 0 FAIL on steps 3 or 6 (denominator and data integrity are non-negotiable) |
| **Weak but directional** | 4+ PASS, no FAIL on denominator, design limitations acknowledged |
| **Not credible** | Any FAIL on denominator (step 3) or data integrity (step 6), OR 3+ FAIL total |
| **Suspect** | Any FLAG on credentials (step 2) combined with FAIL on methodology |

### Step 11: Check against the evidence base

Does the claim's direction match the global evidence base?

- If the study claims protected infrastructure **increases** safety: consistent with literature. Design-specific findings still need methodological rigor.
- If the study claims protected infrastructure **decreases** safety: contradicts the entire meta-analytic evidence base. Requires extraordinary methodological rigor to be taken seriously. Check for vehicular cycling ideology.

---

## Constraints

| Constraint | Rationale |
|---|---|
| Never accept counts without rates as safety evidence | A corridor that increased ridership 4x and crashes 1.5x got safer, not more dangerous |
| Never accept N=1 as generalizable | One corridor's experience cannot overturn meta-analyses across hundreds of corridors |
| Always check for undisclosed ideological commitments | Vehicular cycling ideology produces predictable conclusions regardless of data |
| Distinguish design critique from category critique | "This intersection treatment is dangerous" ≠ "protected bike lanes are dangerous" |

## Outputs

- Pass/fail scorecard for the evaluated study
- Overall credibility verdict with justification
- Specific methodological failures identified
- Comparison to global evidence base direction
