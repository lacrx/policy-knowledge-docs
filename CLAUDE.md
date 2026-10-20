# Policy Knowledge Base Agent Instructions

## When to Fetch (Continuous)
Fetch whenever the task touches: ca-housing-law, land-use-analysis, transportation-safety, municipal-fiscal, pra-strategy, political-landscape, housing-advocacy, rhna-compliance, obstruction-patterns, sb-79, density-bonus, adu-law, housing-element, vision-zero, complete-streets, crash-data, dsa, left-yimby, social-democracy, democratic-socialism.

Unlike engineering knowledge bases (fetched once during planning), this KB is a **runtime reference** — fetch articles and skills during extractions, analysis, drafting, evaluation, or any policy-adjacent work. Not just at session start.

If the task does not involve these topics, skip KB lookup entirely.

## How to Fetch
Fetch files with: `gh api repos/lacrx/policy-knowledge-docs/contents/{path}?ref=main -H "Accept: application/vnd.github.raw+json"`
Never clone the repo. One command per file.

## Discovery Flow
1. Fetch `QUICK-REF.md` first. Find the row matching the task's topic.
2. Extract the article or skill path from the matched row and fetch it.
3. If no match, fetch `TOPIC-INDEX.md` and retry.
4. If still no match, note "not covered in KB" and continue.

## Contribution
When adding or modifying files in `articles/` or `skills/`, read `AGENTS.md` first and follow its contribution workflow exactly.

## Guardrails
Never edit `QUICK-REF.md` or `TOPIC-INDEX.md` manually — they are auto-generated.
Run `python scripts/validate_articles.py` before committing article changes.
Run `python scripts/validate_skills.py` before committing skill changes.
Run `python scripts/generate_topic_index.py` after adding or changing articles or skills.
Run `python -m pytest tests/` before committing changes to scripts.

## Repo Structure
- `articles/` — reference docs organized by category subdirectory
- `skills/` — step-by-step executable instructions (flat directory)
- `scripts/` — generators and validators (stdlib-only Python)
- `tests/` — pytest suite for all scripts
