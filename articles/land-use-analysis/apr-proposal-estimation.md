---
title: Estimating Housing Proposals Without APR Data
topics:
  - apr-methodology
  - housing-proposals
  - land-use-analysis
summary: >
  Calibrate building permits and planning applications as proxy signals for
  housing proposals when HCD Annual Progress Report data is unavailable.
  Covers signal characteristics, calibration ratios, geographic segmentation,
  and confidence tiers.
aliases:
  - apr estimation
  - housing proposal estimation
  - permit-based estimation
  - proposal proxy
related:
  - fiscal-productivity
  - ca-housing-enforcement
last-updated: 2026-07-15
---

# Estimating Housing Proposals Without APR Data

## The APR Gap

HCD's Annual Progress Report (Gov. Code 65400) is the canonical source for housing proposals per jurisdiction. Cities file Table A annually, typically 6-18 months after the reporting year ends. For any analysis of the current year — or recent years before a city has filed — APR data does not exist.

This creates a gap: the most policy-relevant question ("what is happening right now?") has no ground-truth answer until the data is stale.

**Solution**: calibrate locally available data sources against APR for overlap years, then apply the calibration forward.

---

## Available Proxy Signals

Three data sources are available in most California jurisdictions before APR is filed:

| Signal | What it captures | Strengths | Weaknesses |
|--------|-----------------|-----------|------------|
| **Building permits** | Individual construction authorizations (ADUs, SFDs, duplexes, multi-family) | High volume, good coverage for small projects, machine-readable from eTRAKit/Accela | Undercounts large projects (one permit per lot in subdivisions); APR reports full subdivision |
| **Planning applications** | Development plans, density bonus, conditional use permits | Captures large projects (50+ units) that dominate unit counts | Overcounts: apps may be modified, withdrawn, or denied; not all become proposals |
| **Meeting extractions** | Council/planning commission housing discussion | Directional signal only | No reliable unit counts; repeated discussion inflates totals; keyword-dependent |

**Key insight**: permits and planning applications are complementary. Permits capture the long tail of small projects; planning captures the head of large projects. Neither alone covers the full distribution.

---

## Signal Characteristics by Project Size

The proxy signals have fundamentally different characteristics depending on project scale:

**Small projects (1-10 units)**: ADUs, SFDs, duplexes, small lot splits. These go directly to building permits without a separate planning application. Building permits are the only signal. Each permit represents one unit (ADU, SFD) or two (duplex).

**Medium projects (10-50 units)**: Townhome subdivisions, small apartment buildings. These may appear in both planning (development plan) and permits (individual lot permits). Risk of double-counting by APN. Planning descriptions usually contain unit counts; individual lot permits do not.

**Large projects (50+ units)**: Mixed-use towers, large apartment complexes, density bonus projects. These appear first in planning (sometimes years before permits), and the planning application contains the unit count. Building permits may not exist yet or may appear as a single "BLD MID RISE" permit with units in the description.

**Implication for calibration**: separate the calibration by geography or project type. Areas dominated by large projects (e.g., downtown) use planning as the signal; areas dominated by small projects use permits.

---

## Calibration Methodology

### Step 1: Identify Overlap Years

Find years where both APR data and permit/project data exist for the same jurisdiction. Minimum 2 years for meaningful calibration; 3+ preferred.

### Step 2: Compute Ratios

For each overlap year, compute:

```
DT_ratio = APR_proposed_units_downtown / planning_application_units_downtown
NDT_ratio = APR_proposed_units_non_downtown / permit_units_non_downtown
```

Where:
- `APR_proposed_units` = `tot_proposed_units` from APR Table A
- `planning_application_units` = sum of units parsed from planning project descriptions
- `permit_units` = sum of units from residential new-construction permits (ADU=1, SFD=1, duplex=2, multi-family=parsed)

### Step 3: Select Calibration Factor

Use the median ratio across overlap years. Exclude outlier years (e.g., COVID-affected 2020) or years with known data quality issues.

Typical ranges observed (Oceanside, CA):
- Downtown (planning-based): 0.6-0.8x (planning slightly overcounts vs APR)
- Non-downtown (permit-based): 2.3-3.6x (permits significantly undercount vs APR)

### Step 4: Apply Forward

For years without APR:

```
estimated_downtown = planning_units_raw × DT_calibration
estimated_non_downtown = permit_units_raw × NDT_calibration + large_planning_units
```

Where `large_planning_units` are planning projects >10 units not already counted in permits (de-duplicated by APN).

---

## Geographic Segmentation

Sub-area analysis reveals policy effects that citywide numbers obscure. A density cap, zoning change, or overlay district affects a specific geography — citywide totals wash out the signal.

**Method**: classify each record by geography using the Assessor Parcel Number (APN):

1. Obtain parcel-level zoning data (city GIS FeatureServer or assessor records)
2. Build APN → zone_code lookup table
3. Define geographic segments by zone code prefix (e.g., `D-*` = downtown in Oceanside)
4. Classify each permit/project/APR record using its APN

**Coverage**: APN-based classification requires the APN field to be populated. Coverage varies by data source and year. For Oceanside, residential permit APN coverage is >95% for 2024+. For years with lower coverage, unclassifiable records default to "non-downtown" (conservative).

---

## Unit Extraction

Permits and planning applications store unit counts in free-text description fields, not structured columns. Reliable extraction requires regex patterns tuned to local conventions:

```
(\d+)\s*(?:UNIT|MFDU|MF\s*UNIT|DU|DWELLING|APT|CONDO|TOWNHOME|HOME|SFR|LOT)
```

**Type-based defaults** when regex fails:
- `BLD ACCESSORY DWELLING` → 1 unit
- `BLD SFD OR DUPLEX` → 1 unit (2 if description contains "DUPLEX")
- `BLD MULTI FAMILY` / `BLD MID RISE` → parse description; default 4 if unparseable

**De-duplication**: when the same APN appears in both permits and planning, keep the planning unit count for large projects (planning is the application of record) and the permit count for small projects (planning may not exist).

---

## Annualization

For partial-year data (current year), scale linearly:

```
estimated_annual = raw_count × (365 / days_elapsed)
```

**Assumptions**: residential permitting is roughly uniform across the calendar year. Seasonal variation exists (fewer applications in December, more in spring) but is small relative to the calibration uncertainty.

**Confidence degrades early**: an estimate based on 2 months of data has much higher variance than one based on 10 months. Report `year_fraction` alongside the estimate so consumers can judge reliability.

---

## Confidence Tiers

| Tier | Source | When available | Reliability |
|------|--------|---------------|-------------|
| **High** | HCD APR Table A | 6-18 months after year end | Authoritative; state-audited |
| **Medium** | Calibrated estimate (permits + planning) | Real-time | Within ~30% of APR for well-calibrated jurisdictions |
| **Low** | Meeting extractions only | Real-time | Directional only; not suitable for unit counts |

Always label estimates with their confidence tier. Never present calibrated estimates as ground truth.

---

## Worked Example: Oceanside Downtown Density Cap

**Question**: What effect did the downtown density cap have on housing proposals?

**Data**: APR 2018-2025 (ground truth), building permits 2020-2026, planning projects 2023-2026, parcel zoning (61,786 APNs with zone codes).

**Calibration** (from 2023-2024 overlap):
- Downtown planning ratio: 0.7x (planning overcounts slightly)
- Non-downtown permit ratio: 2.7x (permits capture ~37% of APR)

**Result**:

| Period | Downtown share | What happened |
|--------|---------------|---------------|
| 2018-2021 | 0-7% | Pre-cap baseline |
| 2022-2023 | 35-55% | Developers use SB 330 + density bonus at unlimited density |
| 2024 | 40% | Still elevated via ministerial pathways |
| 2025 | 2% | Collapse — cap fully effective |
| 2026 (est.) | 0% | CCC reinstates 86 du/acre; zero planning apps filed |

**Key insight**: citywide proposals held at ~2,000 units/year throughout, proving the collapse was downtown-specific, not market-wide. The density cap eliminated downtown housing proposals.

---

## Limitations

- **Jurisdiction-specific ratios**: calibration factors from one city do not transfer to another. Each jurisdiction must be calibrated independently using its own overlap years.
- **Small sample sizes**: 2-3 overlap years is the minimum; ratios may be unstable. Report the range, not just the median.
- **No withdrawal tracking**: planning applications that are withdrawn or denied still count in raw planning data. The calibration ratio partially corrects for this, but jurisdiction-specific withdrawal rates may vary.
- **Seasonal and cyclical effects**: linear annualization assumes uniform distribution. Interest rate changes, policy announcements, or election cycles can cause non-uniform filing patterns.
- **APN coverage gaps**: older permits may lack APN data, making geographic classification incomplete. Report APN coverage rate per year.

---

## References

- Gov. Code 65400 — Annual Progress Report filing requirement
- HCD APR portal: https://www.hcd.ca.gov/planning-and-community-development/annual-progress-reports
- Gov. Code 65915 — Density Bonus Law
- Gov. Code 65941.1 (SB 330) — Housing Crisis Act preliminary application
