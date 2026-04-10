---
name: git-codebase-health-report
description: Analyze one or more git repositories using their commit history to assess codebase health, risk, and team dynamics — before reading any source code.
---

# Git Codebase Health Report

## Purpose

Analyze one or more git repositories using their commit history to assess codebase health, risk, and team dynamics — before reading any source code. Based on the methodology from [Piechowski's "5 Git Commands Before Reading Code"](https://piechowski.io/post/git-commands-before-reading-code).

## Instructions

For each repository provided, run these 5 git analyses using bash commands, then synthesize into a structured report.

### Analysis 1: High-Churn Files

```bash
git log --format=format: --name-only --since="1 year ago" | sort | uniq -c | sort -nr | head -20
```
Identifies the 20 most-changed files in the past year. High churn signals code that is unstable, under active development, or poorly factored (constantly needing patches).

### Analysis 2: Bus Factor & Contributors

```bash
git log --format='%aN' | sort | uniq -c | sort -rn
```

Also gather:
```bash
git rev-list --count HEAD
git log --reverse --format='%ad' --date=short | head -1
git log -1 --format='%ad' --date=short
```

Ranks contributors by commit count. Watch for: alias fragmentation (same person, different git configs), single-contributor dominance (>60% = critical bus factor risk), and how many people actually carry the project.

### Analysis 3: Bug Hotspots

```bash
git log -i -E --grep="fix|bug|broken" --name-only --format='' | sort | uniq -c | sort -nr | head -20
```

Identifies files most frequently touched in bug-fix commits. Files that appear on both the churn list AND the bug list are the highest-risk code — they break repeatedly and get patched rather than properly fixed.

### Analysis 4: Development Momentum

```bash
git log --format='%ad' --date=format:'%Y-%m' | sort | uniq -c
```

Shows commit frequency by month across the full history. Look for: sustained velocity, declining trends, spikes (release deadlines), and periods of inactivity.

### Analysis 5: Firefighting Patterns

```bash
git log --oneline --since="1 year ago" | grep -iE 'revert|hotfix|emergency|rollback'
```

Counts reverts and emergency fixes. A handful per year is normal. Reverts every couple of weeks means the team doesn't trust its deploy/test process.

## Report Format

For each repository, produce:

### Per-Repository Section

* **Overview table** — total commits, active period, contributor count
* **Bus Factor** — rated 🔴 (1 person >60%), 🟡 (2-3 person core >90%), 🟢 (distributed) — with de-duped contributor table showing commit counts and percentages. Note any alias fragmentation.
* **High-Churn Files** — table of top files with churn count and a brief signal note (e.g., "version bumps — noise", "core logic — real churn")
* **Bug Hotspots** — table of top files. Explicitly call out any files that appear on both the churn and bug lists as highest-risk.
* **Development Momentum** — narrative summary of the commit-over-time trend, noting peaks, declines, spikes, and dormancy.
* **Firefighting** — list the reverts/hotfixes with brief descriptions. Rate as 🟢 (0-3/year), 🟡 (4-10/year), 🔴 (>10/year).

### Cross-Repository Summary

After all individual sections, produce:

* **Summary Risk Matrix** — table with repos as rows and dimensions (Bus Factor, Churn+Bug Overlap, Momentum, Firefighting, Overall Risk) as columns, using 🔴🟡🟢⚪ ratings.
* **Key Takeaways** — 3-5 bullet points identifying the most actionable risks and patterns across the repositories.

## Additional Context

If the repositories have dependency relationships (submodules, shared libraries), check for `.gitmodules` and note how changes in one repo may ripple to others.

When de-duplicating contributor aliases, look for:
* Same first/last name with different casing or formatting
* Username-style entries that match a full-name entry
* Domain-prefixed names (e.g., COMPANY\user)

## Usage

When requested to run a codebase health report on certain directories or repositories, apply this skill systematically to all requested paths.
