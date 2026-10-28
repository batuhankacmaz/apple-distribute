# Apple Distribute

## Overview

Portable Agent Skill for evidence-backed iOS App Store and TestFlight submission reviews. This repository contains guidance and templates, not an iOS app or an automated submission tool.

## Tech Stack

- Platform: Agent Skills-compatible coding agents.
- Language: Markdown with YAML frontmatter.
- Framework: Agent Skills format; Codex invocation uses `$apple-distribute`.
- Database: None.

## Commands

- `git diff --check` — Check changed text for whitespace errors.
- `git ls-files` — Inspect the publication file list for accidental additions.
- If the Codex Skill Creator is installed, run its `scripts/quick_validate.py` against this repository for frontmatter validation.
- There is no app build, runtime, or automated app-compliance test suite in this repository.

## Architecture

`SKILL.md` is the entrypoint. Read `references/remote-config-review.md` when remote behavior matters, and refresh the dated policy snapshot from live Apple sources. `templates/submission-report.md` defines the report structure. Keep each reference linked from the skill.

## Environment Variables

None required. Never add actual app credentials or signing material to this repository.

## Contribution Checks

- Check relative Markdown links and skill frontmatter after edits.
- Verify time-sensitive policy claims against primary Apple sources and retain dates.
- Separate confirmed issues, missing evidence, and engineering recommendations.
- Keep paths, examples, and instructions independent of the author's machine or app.
- Review changed files for secrets and private app details before publication.
- Treat new scripts as a separate capability change; do not reintroduce outdated automated readiness verdicts.
