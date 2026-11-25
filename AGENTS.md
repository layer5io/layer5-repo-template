# AGENTS.md

This file is for agentic coding tools working in this repo.

This repository is created from the `layer5io/layer5-repo-template`
boilerplate. It provides a consistent foundation for all Layer5 projects.
This AGENTS.md is the single source of truth for AI coding agent instructions
in this repository. CLAUDE.md is a symbolic link to AGENTS.md.

---

## Repository Overview

> **REPO-SPECIFIC — fill in for your project**

- **Purpose:** `<one-line description of what this repo does>`
- **Primary language:** `<e.g. Go, JavaScript, Python, Docker>`
- **Entry point:** `<e.g. cmd/<app>, main.go, index.js, Dockerfile>`
- **Implementation layout:** `<brief description of key directories>`
- **License:** Apache 2.0 (see LICENSE)

This repo follows Layer5 project conventions. Read README.md before making changes.
See README.md and CONTRIBUTING.md for project- and community-level details.

---

## Source of Truth

- `AGENTS.md` is the canonical source of instructions for AI coding agents.
- `CLAUDE.md` is a symbolic link pointing to `AGENTS.md`.
- Edit only `AGENTS.md` to update agent instructions.
- Do not maintain a separate copy in `CLAUDE.md`.

---

## Build, Test, and Lint

Build, test, and release commands are owned by the `Makefile`; read it
for the full target list instead of relying on a copy here.

### Common targets (verify in the repo's Makefile)

| Target | Purpose |
|--------|---------|
| `make setup` | Install dependencies |
| `make build` | Build the project |
| `make test` | Run unit tests |
| `make lint` | Run linters |
| `make docker` | Build Docker image |

### Suggested local verification sequence after non-trivial changes

1. Run any language-specific formatter (e.g. `gofmt -w .` for Go, `prettier --write` for JS/TS).
2. `make lint`, if the Makefile defines it, to run all configured linters.
3. `make test`, if the Makefile defines it, to run the test suite.
4. `make build` — confirm a clean build.
5. `make docker` (if applicable) — build or run the Docker environment.

> **REPO-SPECIFIC — replace with the actual commands and tags for this repo**

---

## Where Detail Lives

### Per-area implementation maps

Area-specific agent skills live at:

```
.agents/skills/<area>/SKILL.md
```

`.claude/skills` is a symbolic link to `.agents/skills` where supported by the agent
toolchain. Read the matching skill before changing that area:

- `.agents/skills/repo-navigation/SKILL.md` — Repository navigation, layout orientation, and build targets
- `.agents/skills/code-review/SKILL.md` — Code review, DCO sign-off, commit standards, and PR hygiene
- `.agents/skills/test-guidance/SKILL.md` — Testing procedures, test execution, and verification evidence
- `.agents/skills/docs-guidance/SKILL.md` — Documentation standards, markdown formatting, and link integrity

Example areas to add when adapting this template (customize per repo):

- `.agents/skills/cli/SKILL.md` — CLI command structure, flag parsing, command registration
- `.agents/skills/api/SKILL.md` — API routes, handlers, request/response shapes
- `.agents/skills/ui/SKILL.md` — frontend components, styling, state management
- `.agents/skills/infra/SKILL.md` — infrastructure, Docker, Kubernetes, deployment

### no-mistakes skill (pinned)

This template ships the no-mistakes agent skill at:

```
skills/no-mistakes/SKILL.md
```

It is copied verbatim from https://github.com/kunchenguid/no-mistakes and pinned to release `v1.106.1` (commit `5732d1e`). Regenerate it from the pinned tag on drift — never hand-edit the skill body. See `skills/no-mistakes/SKILL.md` for the regeneration procedure and the pinned version note.

Agents must drive every user-facing change through the no-mistakes pipeline before a PR is raised: run `NO_MISTAKES_TELEMETRY=0 no-mistakes init` once to install the gate, then push through it with `NO_MISTAKES_TELEMETRY=0 git push no-mistakes <branch>`. The gate produces a PR whose body carries a deterministic signature and a `## Pipeline` attestation.

### Docs and config that own behavior

Do not guess where user-facing semantics live — these files are authoritative:

| What | Where |
|------|-------|
| CI / GitHub Actions workflows | `.github/workflows/*.yml` |
| Release notes configuration | `.github/release-drafter.yml` |
| PR/issue labeling rules | `.github/labeler.yml`, `.github/workflows/labeler.yml` |
| Label commenter responses | `.github/label-commenter-config.yml` |
| Stale issue handling | `.github/stale.yml` |
| Behaviorbot welcome messages | `.github/config.yml` |
| Contribution guidelines | `CONTRIBUTING.md`, `CONTRIBUTING-gitflow.md` |
| Code of conduct | `CODE_OF_CONDUCT.md` |
| Docker build args / release channel | `.github/build/latest_release.sh`, `.github/build/Makefile.core.mk` |
| Makefile targets | `Makefile`, `.github/build/Makefile.core.mk`, `.github/build/Makefile.show-help.mk` |

> **REPO-SPECIFIC — adjust paths as needed for your project layout**

### Generated files — do not hand-edit

The following are generated from source. Never edit them directly;
modify the source and run the documented generation process instead.

> **REPO-SPECIFIC — list generated files and their generation commands**

Examples (adopt or remove as applicable):

| Generated file | Source | Generation command |
|----------------|--------|-------------------|
| `skills/<name>/SKILL.md` | `internal/skill/skill.go` (or equivalent) | `make generate-skills` |
| `CHANGELOG.md` | Release drafter / git history | `make changelog` or GitHub release |
| `docs/api/*` | Source code annotations | `make gen-docs` |

If a file is not listed above and appears generated, check for a header comment
or generation script before editing.

---

## Invariants Every Change Must Keep

> **REPO-SPECIFIC — add project-specific invariants, security boundaries, or rules**

Layer5-wide conventions:

- All commits must be signed off (`Signed-off-by:` line) per the DCO.
- Use `git commit -s` or `--signoff` to sign off automatically.
- Follow the fork-and-PR workflow described in `CONTRIBUTING-gitflow.md`.
- Reference an open issue in every pull request.
- Keep changes focused and well documented.

### PR Gate: Require no-mistakes

Every pull request in this repository must be raised through the no-mistakes pipeline.
The required GitHub Actions check `PR must be raised via no-mistakes` runs on every PR
(`opens`, `edited`, `synchronize`, `reopened`) and fails when the PR body is missing the
deterministic signature and structured pipeline-step attestation that no-mistakes writes.
PRs without them will not be reviewed or merged.

- Opt in once per repo: `NO_MISTAKES_TELEMETRY=0 no-mistakes init` (installs the gate and the `/no-mistakes` agent skill), then push through it: `NO_MISTAKES_TELEMETRY=0 git push no-mistakes <branch>`.
- The gate writes the PR body, including a `## Pipeline` section and a signature line. Preserve the whole generated body — replacing it removes the signature/attestation and makes the required check fail.
- Automation accounts (`github-actions[bot]`, `dependabot[bot]`, `release-please[bot]`) are exempt so release/dependency pipelines keep working.

### Telemetry (disabled by default)

Official no-mistakes release binaries include a default self-hosted telemetry host and website ID. This template disables telemetry by default:

- Disable: `NO_MISTAKES_TELEMETRY=0`
- Override host / website ID (only if a repo runs its own telemetry): `NO_MISTAKES_UMAMI_HOST`, `NO_MISTAKES_UMAMI_WEBSITE_ID`

Set `NO_MISTAKES_TELEMETRY=0` in setup docs, CI workflows, and install/init instructions. When disabled, telemetry uses a noop sink and performs no network lookup on each command. Verify telemetry is off by confirming no DNS/HTTP telemetry lookup occurs and the noop sink is active (see `internal/telemetry/telemetry.go` in no-mistakes).

---

## Maintaining This File

Keep this file for knowledge useful to almost every future agent session in
this project. Do not repeat what the codebase already shows; point to the
authoritative file or command instead. Prefer rewriting or pruning existing
entries over appending new ones. When updating this file, preserve this bar
for all agents and keep entries concise.

---

## Repository-Specific Sections to Complete

When adapting this template for a specific Layer5 repo, replace every
`> **REPO-SPECIFIC — ...**` placeholder with concrete values:

- [ ] Repository Overview — purpose, language, entry point, layout
- [ ] Build, Test, and Lint — actual Makefile targets and commands
- [ ] Where Detail Lives — actual skill areas, doc paths, generated files
- [ ] Invariants — project-specific rules and security boundaries
- [ ] Any additional area-specific skill files under `.agents/skills/`

---

## Contributions

Follow `CONTRIBUTING.md` when submitting changes.

Review the relevant tests and documentation before opening a pull request.

All Layer5 projects are community-built and welcome collaboration. Join the
[Layer5 Community](https://layer5.io/community) and our
[Slack](http://slack.layer5.io).
