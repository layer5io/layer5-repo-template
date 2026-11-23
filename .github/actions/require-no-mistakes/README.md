# Require no-mistakes composite action

Shared composite action that enforces the `PR must be raised via no-mistakes` gate.

## What it does

Verifies that a pull request body declares a no-mistakes pipeline run:

1. The body carries the no-mistakes signature line (`Updates from [git push no-mistakes](https://github.com/kunchenguid/no-mistakes)`).
2. The body carries a parseable v1 pipeline-step attestation comment (`<!-- no-mistakes-pipeline-attestation:v1 ... -->`).
3. The attestation's `head_sha` equals the current PR head SHA, so a later push cannot pass on an older attestation.
4. `review`, `test`, and `document` each recorded status == `completed`. Skips and failures are not compliant.

This is the single shared implementation of the gate. Consumers call it instead of copying the enforcement logic, which prevents the drift that plagued inline copies.

## Usage

Caller workflow (pin to a release tag or commit SHA — never `@main`, which is editable by the very PR the gate judges):

```yaml
jobs:
  check:
    name: PR must be raised via no-mistakes
    runs-on: ubuntu-latest
    permissions:
      contents: read
      pull-requests: read
    steps:
      - name: Verify no-mistakes signature and pipeline attestation
        uses: kunchenguid/no-mistakes/.github/actions/require-no-mistakes@v1.80.1
        with:
          exempt-authors: kunchenguid
```

When called via `uses: ./.github/actions/require-no-mistakes`, the action runs from the checked-out workspace and executes the PR's own modifications. For an independent enforcement implementation that cannot be modified by the pull request under evaluation, reference the shared composite action at a fixed release or commit SHA (e.g., `uses: kunchenguid/no-mistakes/.github/actions/require-no-mistakes@v1.106.1`).

## Inputs

See `action.yml` for the full input list (`pr-body`, `pr-head-sha`, `pr-head-ref`, `pr-author`, `pr-number`, `exempt-authors`, `exempt-bot-authors`, `exempt-head-branches`, `github-token`). An ordinary `pull_request`-triggered caller passes nothing and relies on the event payload.

## Outputs

- `compliant`: `true` only when the PR body structurally satisfies the pipeline gate; `false` for exemptions.
- `exempt`: `true` when the PR bypassed the gate through a configured exemption.
- `exempt-reason`: human-readable exemption reason; empty when judged.

## Required permissions

Grant the caller workflow `pull-requests: read` so the action can read the PR's **live** body/head SHA from the GitHub API. Without it (and without explicit `pr-body`/`pr-head-sha` inputs), a live-lookup failure fails the whole gate closed rather than certifying from a possibly-stale cached event payload (see `verify.py`).

## Telemetry

This action itself performs no network telemetry. Telemetry concerns the `no-mistakes` CLI, not this gate. When a repo uses `no-mistakes`, disable telemetry by default with `NO_MISTAKES_TELEMETRY=0`; override host/website ID with `NO_MISTAKES_UMAMI_HOST` and `NO_MISTAKES_UMAMI_WEBSITE_ID` only if the repo intentionally runs its own telemetry.

## Pinning

Pin to a release tag or commit SHA. Never track `@main`: the action is judged by the PRs it enforces, and `@main` could be changed mid-review to self-certify.

---

Source: https://github.com/kunchenguid/no-mistakes (`/no-mistakes` skill)
Pinned in this template to no-mistakes `v1.106.1` (commit `5732d1e`). Regenerate on drift — do not hand-edit.