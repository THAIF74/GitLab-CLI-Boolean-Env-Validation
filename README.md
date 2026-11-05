# GitLab CLI — Boolean Environment Variable Validation

A focused record of my open-source contribution to **GitLab CLI**, addressing [issue #7969](https://gitlab.com/gitlab-org/cli/-/work_items/7969).

The contribution proposes validating boolean environment-variable values during CLI startup so invalid configuration is reported clearly instead of silently disabling the related feature.

## Contribution links

- **Upstream project:** [gitlab-org/cli](https://gitlab.com/gitlab-org/cli)
- **Issue:** [#7969 — Invalid environment variable values should return an error instead of running](https://gitlab.com/gitlab-org/cli/-/work_items/7969)
- **Merge request:** [!4334 — fix(config): reject invalid boolean environment values](https://gitlab.com/gitlab-org/cli/-/merge_requests/4334)
- **CI pipeline:** [Pipeline #3033455489](https://gitlab.com/THAIF74/cli/-/pipelines/3033455489)
- **Contribution branch:** `fix/validate-boolean-env-vars-7969`
- **Latest recorded commit:** [`9a1049ac`](https://gitlab.com/THAIF74/cli/-/commit/9a1049acf5a455c25aa0a1030ade73d63ab0332e)

## Problem

Boolean environment variables can be supplied with invalid values. Without explicit validation, a related feature may remain disabled without clearly telling the user that the configuration value was invalid.

## Proposed solution

The merge request:

1. Identifies boolean environment variables from the configuration schema and explicitly typed non-schema variables.
2. Validates values that are set and non-empty using Go's `strconv.ParseBool`.
3. Collects invalid variable names and values into a clear error message.
4. Runs validation after configuration initialization and exits with status code `2` when invalid values are found.
5. Adds tests for valid, unset, empty, invalid schema-backed, invalid non-schema, and multiple invalid values.

## Implementation files in the upstream merge request

- `internal/config/envvars.go`
- `internal/config/envvars_test.go`
- `cmd/glab/main.go`

The authoritative source code is the branch and merge request linked above. This repository is a contribution record; it is **not** a mirror of the full GitLab CLI source tree.

## Current status

**In review — not merged.**

The latest recorded pipeline is not green yet. At the last check, the integration test and several documentation/check jobs had passed, while the lint job reported two findings in `internal/config/envvars_test.go` (import grouping and an error assertion that should use `require`). Unit tests were still running and coverage had not started. Check the live [pipeline](https://gitlab.com/THAIF74/cli/-/pipelines/3033455489) for the latest result.

No approval or merge is claimed here. This status will be updated after the lint findings and remaining CI jobs are resolved and the upstream merge request receives a final outcome.

## Evidence to add after review

When the upstream merge request is accepted or otherwise reaches a final outcome, this repository can be updated with:

- The final accepted patch or relevant contribution files.
- Final commit and merge details.
- Final CI results.
- Screenshots or links showing the issue, merge request, review, and outcome.

## Scope

This repository documents one focused contribution to an existing open-source project. It does not claim ownership of GitLab CLI, reproduce the complete upstream repository, or claim that the proposed change has been merged.

---

**Author:** THAIF74  
**Upstream project:** GitLab CLI  
