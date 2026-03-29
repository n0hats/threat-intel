# Threat Intel — Agent Instructions

## Project Overview
This is a GitHub Pages site that tracks active cybersecurity threats — 0-days, CVEs, exploits, and advisories. The agent team researches threats from public sources and publishes structured posts to the site.

## GitHub
- Repo owner: n0hats
- Repo name: threat-intel
- GitHub Pages branch: `gh-pages` (or `main` with `/docs` folder)
- Create repo if it doesn't exist: `gh repo create n0hats/threat-intel --public --source=. --push`
- Enable GitHub Pages: `gh api repos/n0hats/threat-intel/pages --method POST -f source[branch]=main -f source[path]=/docs`

## Team Structure
- **Lead agent**: Coordinates research tasks, prioritizes threats by severity
- **Research agent**: Monitors public threat feeds, writes threat summaries
- **Publisher agent**: Formats posts as markdown, commits and opens PRs
- **Review agent**: Fact-checks posts before approving PRs

## Tech Stack
- Jekyll static site (GitHub Pages native)
- Markdown posts in `docs/_posts/`
- Minimal theme (Minima or custom)
- No build step needed — GitHub Pages handles Jekyll automatically

## Threat Sources to Monitor
- NVD (National Vulnerability Database): https://nvd.nist.gov/feeds/json/cve/1.1/
- CISA Known Exploited Vulnerabilities: https://www.cisa.gov/known-exploited-vulnerabilities-catalog
- GitHub Security Advisories
- Exploit-DB
- Packet Storm Security

## Post Format
Each threat post should follow this structure:
```markdown
---
layout: post
title: "CVE-YYYY-XXXXX: <Short Title>"
date: YYYY-MM-DD
severity: critical|high|medium|low
tags: [cve, 0-day, ransomware, etc]
---

## Summary
One paragraph overview of the threat.

## Affected Systems
- List of affected software/versions

## Impact
What an attacker can do if exploited.

## Mitigation
- Patch version / workaround steps
- CVSS score: X.X

## References
- Link to NVD
- Link to vendor advisory
```

## Git Workflow
- Branch per post: `git checkout -b post/<cve-id-or-slug>`
- One PR per post or batch of related posts
- Open PR: `gh pr create --title "Add: CVE-YYYY-XXXXX" --body "..."`
- Auto-approve and merge when fact-check passes:
  `gh pr review --approve && gh pr merge --squash`

## PR Approval
- Use `gh pr review --approve` to approve PRs
- Enable self-approval: `gh api repos/n0hats/threat-intel --method PATCH -f allow_self_approval=true`

## Publishing Standards
- Only publish CVEs with CVSS score >= 7.0 unless it's a widely exploited 0-day
- Always include mitigation steps — never publish without them
- Use factual, neutral language
- Tag posts accurately for filtering

## Environment
- Enable agent teams: `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`
- This is set automatically via `.claude/settings.json`
