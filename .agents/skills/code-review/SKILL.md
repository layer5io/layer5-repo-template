---
name: code-review
description: Code review and PR preparation standards for Layer5 projects. Use before creating or updating pull requests, reviewing diffs, verifying DCO sign-offs, and checking commit formatting.
---

# Code Review & PR Preparation Skill

Guidelines and checks for code review across Layer5 repositories.

## Pre-PR Checklist

1. **Developer Certificate of Origin (DCO)**:
   - Every commit must contain a valid `Signed-off-by:` line.
   - Use `git commit -s` or `--signoff`.
   - Never force-push or bypass DCO requirements.

2. **Commit Conventions**:
   - Conventional Commits: `<type>(<scope>): <short summary>` (e.g., `feat:`, `fix:`, `docs:`, `chore:`).
   - Reference open GitHub issues in PR body and commits where applicable.

3. **Clean Diffs**:
   - No untracked build artifacts, editor configurations, or test binaries.
   - No trailing whitespace or accidental indentation reformats across untouched code.
   - Keep pull requests focused on a single logical change.

4. **Security & Secrets**:
   - Never commit tokens, credentials, private keys, or internal endpoints.
