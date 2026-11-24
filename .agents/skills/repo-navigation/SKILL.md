---
name: repo-navigation
description: Orientation and repository navigation guide for Layer5 projects. Use when starting a new task, exploring the repository layout, identifying entry points, locating build targets, or looking up config ownership.
---

# Repository Navigation Skill

Guide for agents exploring and navigating Layer5 repositories derived from `layer5-repo-template`.

## Core Layout

- `Makefile`: Entry point for all development, build, test, and lint tasks. Never invent ad-hoc build commands if a Makefile target exists.
- `.github/workflows/`: Authoritative CI/CD pipeline definitions and automated checks.
- `.github/`: Issue templates, PR templates, labeler configuration, release-drafter, and community automation.
- `AGENTS.md` (and `CLAUDE.md` symlink): Single source of truth for agent instructions.
- `.agents/skills/`: Area-specific and workflow skills.

## Navigation Protocol

1. **Locate Build Commands**:
   - Inspect `Makefile` first. Check for `build`, `test`, `lint`, `setup`, and `docker` targets.
   - For modular Makefiles, review `.github/build/*.mk`.

2. **Locate Configuration & Docs**:
   - Check `CONTRIBUTING.md` and `CONTRIBUTING-gitflow.md` for contribution workflows.
   - Check `.github/release-drafter.yml` for release categorization.
   - Check `.github/labeler.yml` for PR/issue categorization tags.

3. **Check Generated Files**:
   - Look for generation scripts or Makefile targets (`gen-*`, `generate-*`) before modifying any file marked generated.
