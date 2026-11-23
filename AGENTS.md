# Agent Instructions

## Repository Overview

This repository serves as a template for Layer5 projects.

These instructions provide general guidance for AI coding agents
working with repositories created from this template.

## Source of Truth

AGENTS.md is the canonical source of instructions for AI coding agents.

CLAUDE.md is a symbolic link pointing to AGENTS.md.

Contributors should only edit AGENTS.md to update agent instructions.

Do not maintain a separate copy of these instructions in CLAUDE.md.

## Project Structure

- README.md: Project overview and documentation.
- CONTRIBUTING.md: Contribution guidelines.
- Makefile: Available development and build commands.
- .github/workflows/: GitHub Actions workflows and CI configuration.
- .github/: Issue templates and repository configuration.

## Development Guidelines

1. Read README.md before making changes.
2. Follow the guidelines in CONTRIBUTING.md.
3. Inspect the Makefile to identify available build and test commands.
4. Follow the existing coding conventions.
5. Keep changes focused and well documented.
6. Run the relevant available tests before submitting a pull request.

## Agent Skills

When available, consult area-specific agent skills located at:

.agents/skills/<area>/SKILL.md

Follow the instructions applicable to the area being modified.

### no-mistakes skill (pinned)

This template ships the no-mistakes agent skill at:

skills/no-mistakes/SKILL.md

It is copied verbatim from https://github.com/kunchenguid/no-mistakes and pinned to release `v1.106.1` (commit `5732d1e`). Regenerate it from the pinned tag on drift — never hand-edit the skill body. See `skills/no-mistakes/SKILL.md` for the regeneration procedure and the pinned version note.

Agents must drive every user-facing change through the no-mistakes pipeline before a PR is raised: run `NO_MISTAKES_TELEMETRY=0 no-mistakes init` once to install the gate, then push through it with `NO_MISTAKES_TELEMETRY=0 git push no-mistakes <branch>`. The gate produces a PR whose body carries a deterministic signature and a `## Pipeline` attestation.

## Generated Files

Do not manually edit generated files.

Instead, locate the original source and use the project's documented
generation process.

Repository-specific generated files and generation commands should
be documented when this template is adapted for a project.

## PR Gate: Require no-mistakes

Every pull request in this repository must be raised through the no-mistakes pipeline.
The required GitHub Actions check `PR must be raised via no-mistakes` runs on every PR
(`opens`, `edited`, `synchronize`, `reopened`) and fails when the PR body is missing the
deterministic signature and structured pipeline-step attestation that no-mistakes writes.
PRs without them will not be reviewed or merged.

- Opt in once per repo: `NO_MISTAKES_TELEMETRY=0 no-mistakes init` (installs the gate and the `/no-mistakes` agent skill), then push through it: `NO_MISTAKES_TELEMETRY=0 git push no-mistakes <branch>`.
- The gate writes the PR body, including a `## Pipeline` section and a signature line. Preserve the whole generated body — replacing it removes the signature/attestation and makes the required check fail.
- Automation accounts (`github-actions[bot]`, `dependabot[bot]`, `release-please[bot]`) are exempt so release/dependency pipelines keep working.

## Telemetry (disabled by default)

Official no-mistakes release binaries include a default self-hosted telemetry host and website ID. This template disables telemetry by default:

- Disable: `NO_MISTAKES_TELEMETRY=0`
- Override host / website ID (only if a repo runs its own telemetry): `NO_MISTAKES_UMAMI_HOST`, `NO_MISTAKES_UMAMI_WEBSITE_ID`

Set `NO_MISTAKES_TELEMETRY=0` in setup docs, CI workflows, and install/init instructions. When disabled, telemetry uses a noop sink and performs no network lookup on each command. Verify telemetry is off by confirming no DNS/HTTP telemetry lookup occurs and the noop sink is active (see `internal/telemetry/telemetry.go` in no-mistakes).

## Repository-Specific Instructions

Repositories created from this template should document:

- Project purpose and architecture.
- Required development tools and versions.
- Setup and build commands.
- Testing and linting commands.
- Generated files that must not be edited manually.
- Additional project-specific coding conventions.

## Contributions

Follow CONTRIBUTING.md when submitting changes.

Review the relevant tests and documentation before opening a pull request.