---
name: evaluate-enforcement-claim
title: Evaluate an Automated Enforcement Claim
type: skill
topics:
  - transportation-safety
  - automated-enforcement
  - red-light-cameras
  - speed-cameras
summary: >
  Evaluate a claim for or against automated traffic enforcement (red light cameras, speed cameras) against the peer-reviewed evidence base. Produces a structured verdict with specific rebuttals.
references:
  - articles/transportation-safety/automated-enforcement-evidence.md
  - articles/transportation-safety/crash-data-methodology.md
last-updated: 2026-09-17
---

# Evaluate an Automated Enforcement Claim

Structured evaluation of a claim about automated traffic enforcement effectiveness.
Identifies which argument pattern is being used and provides evidence-based rebuttal.

---

## Prerequisites

- The specific claim to evaluate
- Source of the claim (council presentation, Reddit comment, news article, study)
- The jurisdiction or context

---

## Steps

### Step 1: Classify the claim

Which argument pattern does this match?

- [ ] **"Cameras increase crashes"** — usually citing rear-end increase without severity weighting
- [ ] **"Cameras are revenue generators"** — motive attribution without addressing safety data
- [ ] **"Our city is different"** — exceptionalism without evidence
- [ ] **"Just fix signal timing"** — false dichotomy (they're complementary)
- [ ] **"The research is mixed"** — citing Erke 2009 or cherry-picked studies
- [ ] **"Site selection matters"** — true but used to oppose the study that would produce good site selection
- [ ] **"Privacy concerns"** — legitimate concern, but SB 720 addresses with data protections
- [ ] **Other** — describe the specific argument

### Step 2: Check the evidence cited

If the claim cites a study:

- [ ] Is it peer-reviewed? (conference papers and advocacy reports are not peer review)
- [ ] Does it measure crash severity or just counts? (counts without severity weighting are misleading)
- [ ] Does it use Empirical Bayes or comparison groups? (simple before-after without controls fails)
- [ ] Does it control for regression to the mean? (high-crash sites regress naturally)
- [ ] Does it account for traffic volume changes? (COVID, construction, development)
- [ ] Is it Erke 2009? If yes: directly rebutted by Burkey & Obeng 2009, superseded by Hoye 2013

Apply the full crash-data-methodology.md checklist if the claim rests on a specific study.

### Step 3: Check against the evidence base

Compare the claim to the automated-enforcement-evidence.md article:

- Does the claim contradict the meta-analyses? (Hoye 2013, Cohn 2020, Wilson 2010)
- Does the claim contradict the IIHS fatal crash studies? (Hu & Cicchino 2017)
- Does the claim ignore camera removal evidence? (crashes increase every time)
- Does the claim ignore the AEB finding? (rear-end tradeoff is disappearing)

### Step 4: Identify rhetorical patterns

Common bad-faith patterns:

- **Motte-and-bailey:** "cameras don't work" (bailey) retreats to "site selection matters" (motte) when challenged with evidence
- **Moving goalposts:** demands increasingly specific evidence while never stating what would change their mind
- **Cherry-picking:** citing rear-end increase from FHWA-HRT-05-048 while ignoring the study's own conclusion that net benefit is positive
- **False equivalence:** treating one methodologically flawed study as equal to 8 meta-analyses
- **Concern trolling:** "I support studying cameras" while opposing the vote to study cameras

### Step 5: Produce verdict

**Format:**

```
CLAIM: [one sentence]
PATTERN: [from Step 1]
EVIDENCE CITED: [what they cited, if anything]
EVIDENCE QUALITY: [PASS/FAIL per Step 2]
CONTRADICTS: [which meta-analyses/studies from Step 3]
RHETORICAL PATTERN: [from Step 4, if applicable]
VERDICT: [SUPPORTED / UNSUPPORTED / MISLEADING]
REBUTTAL: [2-3 sentences with specific citations]
```
