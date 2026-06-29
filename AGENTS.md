---
description: Onboarding guide for AI agents and human contributors to the policy knowledge base.
alwaysApply: false
---
# Policy Knowledge Base — Onboarding

## Purpose
- **AI agents**: Retrieve articles and skills at runtime to inform policy analysis, legal evaluation, and advocacy work.
- **Advocates**: Look up statute references, enforcement pipelines, analytical frameworks, and rebuttal patterns.
- **Contributors**: Add or update articles and skills following the formats and validation rules below.

---
## Repository Structure
```
├── articles/                  # Advisory reference docs (rationale, evidence, law)
│   ├── ca-housing-law/        #   California housing statutes, enforcement, case law
│   ├── land-use-analysis/     #   Fiscal analysis, density evidence, policy evaluation
│   ├── transportation-safety/ #   Crash data methodology, infrastructure evidence
│   ├── municipal-fiscal/      #   Revenue-per-acre, infrastructure lifecycle, subsidy analysis
│   └── pra-strategy/          #   Public records requests, CPRA compliance, document analysis
├── skills/                    # Executable step-by-step procedures (flat)
├── scripts/                   # Generators and validators (stdlib-only Python)
├── tests/                     # Pytest suite for all scripts
├── QUICK-REF.md               # Auto-generated lookup table (do not edit)
├── TOPIC-INDEX.md             # Auto-generated topic index (do not edit)
├── CLAUDE.md                  # Claude Code agent instructions
└── AGENTS.md                  # This file
```

---
## How Agents Retrieve Content
Fetch files directly via the GitHub API. Never clone the repo.
```bash
# Quick-reference index
gh api repos/lacrx/policy-knowledge-docs/contents/QUICK-REF.md?ref=main -H "Accept: application/vnd.github.raw+json"
# An article
gh api repos/lacrx/policy-knowledge-docs/contents/articles/ca-housing-law/enforcement-pipeline.md?ref=main -H "Accept: application/vnd.github.raw+json"
# A skill
gh api repos/lacrx/policy-knowledge-docs/contents/skills/evaluate-sb79-compliance.md?ref=main -H "Accept: application/vnd.github.raw+json"
```
**Discovery flow**: Fetch `QUICK-REF.md` → find matching row → fetch linked article or skill. If no match, try `TOPIC-INDEX.md`. If still no match, note "not covered" and continue.

---
## Article Format
```yaml
---
title: Human-Readable Title
topics:
  - lowercase-hyphen-tag
summary: >
  One-line summary.
skills:
  - companion-skill-slug
aliases:
  - alternate-name
last-updated: YYYY-MM-DD
---
```
- Maximum 500 lines. Topic tags: `^[a-z0-9]+(-[a-z0-9]+)*$`.
- Focus on evidence, statutes, and analytical frameworks — not step-by-step instructions.
- Reference companion skills for executable procedures.
- Cite peer-reviewed sources where applicable. Include statute code sections.

---
## Skill Format
```yaml
---
name: skill-slug-matching-filename
topics:
  - lowercase-hyphen-tag
summary: >
  One-line summary.
references:
  - articles/category/related-article.md
last-updated: YYYY-MM-DD
---
```
- Must contain `## Prerequisites`, `## Steps`, `## Constraints`, `## Outputs` sections.
- Steps: numbered, with concrete examples. No hard-coded secrets.
- One task per skill. `name` must match filename stem.

---
## How to Contribute
### Adding an Article
1. Pick or create a category under `articles/` (lowercase-hyphen name).
2. Run `python scripts/new_article.py <slug> --category <category>`.
3. Fill in body sections and frontmatter.
4. Run validation and regenerate indexes, then commit together.

### Adding a Skill
1. Run `python scripts/new_skill.py <slug>`.
2. Fill in Steps with numbered, executable instructions.
3. Run validation and regenerate indexes, then commit together.

---
## Validation
Run before every commit:
```bash
python scripts/validate_articles.py
python scripts/validate_skills.py
python scripts/generate_topic_index.py
python -m pytest tests/
```

---
## Guardrails
- Never hard-code secrets — use env vars or secret managers.
- Never edit `TOPIC-INDEX.md` or `QUICK-REF.md` manually — auto-generated.
- All content must pass validation before merging.
- Update `last-updated` in frontmatter on every change.
- Articles = advisory (evidence, law, frameworks). Skills = executable (steps).
- Regenerate indexes whenever articles or skills change.
- Cite statute code sections precisely (e.g., Gov. Code § 65589.5, not "the HAA").
- Cite peer-reviewed studies by author, year, and journal.

---
Last updated: 2026-06-28
