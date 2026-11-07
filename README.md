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

**Open for review — not approved or merged.**

The latest recorded pipeline (#3033455489) finished with a failed status because the lint job found two issues in `internal/config/envvars_test.go`:

- Import grouping / formatting must satisfy `gci`.
- The error assertion should use `require`, as requested by `testifylint`.

The following jobs passed: unit tests, integration tests, coverage, comment lint, documentation build and checks, argument checks, embedded-file checks, commit lint, and generated-code checks. The coverage job reported **73.80%**. The optional `govulncheck` job was manual and allowed to fail; it was not run.

The two lint findings still need to be fixed and CI rerun. No approval or merge is claimed.

## Archived implementation patch\n\nThe exact unified diff from the current upstream merge request is stored at [`patches/mr-4334-boolean-env-validation.patch`](patches/mr-4334-boolean-env-validation.patch). Pipeline findings are recorded in [`reports/ci-pipeline-3033455489.md`](reports/ci-pipeline-3033455489.md). The patch reflects the submitted MR head; it is not yet the lint-corrected final version.\n\n## Evidence to add after review

After the lint findings are resolved and the upstream merge request reaches a final outcome, this repository can be updated with:

- The final accepted patch or relevant contribution files.
- Final commit and merge details.
- Final CI results.
- Screenshots or links showing the issue, merge request, review, and outcome.

## Scope

This repository documents one focused contribution to an existing open-source project. It does not claim ownership of GitLab CLI, reproduce the complete upstream repository, or claim that the proposed change has been merged.

---

**Author:** THAIF74  
**Upstream project:** GitLab CLI  
