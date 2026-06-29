---
name: fetch-policy-bundle
title: Fetch Policy Bundle
type: skill
topics:
  - policy-knowledge
summary: >
  Fetch all skills matching a given topic tag from the policy knowledge base in one pass. Used at session start to bulk-load relevant policy context.
references:
  - articles/ca-housing-law/ca-housing-enforcement.md
  - articles/land-use-analysis/fiscal-productivity.md
  - articles/transportation-safety/crash-data-methodology.md
  - articles/pra-strategy/cpra-compliance.md
last-updated: 2026-06-28
---

# Fetch Policy Bundle

Bulk-fetch every skill matching a topic tag from the policy knowledge base repo.
One script, one topic, all matching skills loaded into context.

---

## Prerequisites

- `gh` CLI installed and authenticated (`gh auth status`)
- `bash` with `base64`, `grep`, `sed`, `sort` available
- Network access to GitHub API

---

## Steps

### Step 1: Set parameters

```bash
TOPIC="${1:?Usage: fetch-policy-bundle.sh <topic>}"
OWNER="lacrx"
REPO="policy-knowledge-docs"
BRANCH="main"
QUICK_REF_PATH="QUICK-REF.md"
```

### Step 2: Fetch the quick-reference index

```bash
QUICK_REF=$(gh api \
  -H "Accept: application/vnd.github.raw+json" \
  "repos/${OWNER}/${REPO}/contents/${QUICK_REF_PATH}?ref=${BRANCH}")
```

### Step 3: Filter rows matching the topic

```bash
MATCHED_ROWS=$(echo "$QUICK_REF" | grep -i "$TOPIC" || true)

if [ -z "$MATCHED_ROWS" ]; then
  echo "No skills found for topic: ${TOPIC}" >&2
  exit 0
fi
```

### Step 4: Extract and deduplicate skill paths

```bash
SKILL_PATHS=$(echo "$MATCHED_ROWS" \
  | grep -oE 'skills/[A-Za-z0-9_.+/-]+\.md' \
  | sort -u)

if [ -z "$SKILL_PATHS" ]; then
  echo "Matched rows but no skill paths for topic: ${TOPIC}" >&2
  exit 0
fi
```

### Step 5: Fetch and print each skill

```bash
SKILL_COUNT=$(echo "$SKILL_PATHS" | wc -l)
echo "Fetching ${SKILL_COUNT} skill(s) for topic: ${TOPIC}" >&2

for SKILL_PATH in $SKILL_PATHS; do
  echo "=== ${SKILL_PATH} ==="
  gh api \
    -H "Accept: application/vnd.github.raw+json" \
    "repos/${OWNER}/${REPO}/contents/${SKILL_PATH}?ref=${BRANCH}"
  echo ""
done
```

---

## Constraints

| Constraint | Rationale |
|---|---|
| No hard-coded secrets | `gh` uses existing auth token |
| Read-only | Never modify repository content |
| Output to stdout only | No disk writes |
| Empty topic match exits cleanly | Not with error |

## Outputs

- Raw markdown content of all matching skills, printed to stdout
- Each skill separated by `=== path ===` header
- Count of fetched skills on stderr
