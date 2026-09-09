<!-- markdownlint-disable -->

# Hardening Report: cloudposse--github-action-yaml-config-query/v1.0.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **cloudposse--github-action-yaml-config-query/v1.0.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference external actions using mutable tags (@main, @v2, @v3, @v4) instead of pinned 40-character commit SHAs. This exposes the workflow to supply-chain attacks if the referenced tag is moved to a malicious commit. Affected references include: cloudposse/.github/.github/workflows/shared-github-action.yml@main, cloudposse/github-actions-workflows/.github/workflows/ci-typescript-app-check-dist.yml@main, actions/checkout@v4, actions/setup-node@v4, cloudposse/.github/.github/workflows/shared-release-branches.yml@main, actions/checkout@v3, github/codeql-action/init@v2, github/codeql-action/autobuild@v2, github/codeql-action/analyze@v2, nick-fields/assert-action@v2.

Locations:

- `.github/workflows/branch.yml:24`
- `.github/workflows/build-and-test.yml:13`
- `.github/workflows/build-and-test.yml:23`
- `.github/workflows/build-and-test.yml:27`
- `.github/workflows/codeql.yml:35`
- `.github/workflows/codeql.yml:40`
- `.github/workflows/codeql.yml:57`
- `.github/workflows/codeql.yml:67`
- `.github/workflows/release.yml:9`
- `.github/workflows/test-multiline.yml:31`
- `.github/workflows/test-multiline.yml:33`
- `.github/workflows/test-multiline.yml:62`
- `.github/workflows/test-multiline.yml:68`
- `.github/workflows/test-negative.yml:31`
- `.github/workflows/test-negative.yml:33`
- `.github/workflows/test-negative.yml:55`
- `.github/workflows/test-negative.yml:60`
- `.github/workflows/test-negative.yml:65`
- `.github/workflows/test-positive.yml:31`
- `.github/workflows/test-positive.yml:33`
- `.github/workflows/test-positive.yml:54`
- `.github/workflows/test-positive.yml:59`
- `.github/workflows/test-query-1.yml:31`
- `.github/workflows/test-query-1.yml:33`
- `.github/workflows/test-query-1.yml:57`
- `.github/workflows/test-query-1.yml:62`
- `.github/workflows/test-query-2.yml:31`
- `.github/workflows/test-query-2.yml:33`
- `.github/workflows/test-query-2.yml:57`
- `.github/workflows/test-query-2.yml:62`
- `.github/workflows/test-query-3.yml:31`
- `.github/workflows/test-query-3.yml:33`
- `.github/workflows/test-query-3.yml:55`
- `.github/workflows/test-structure.yml:31`
- `.github/workflows/test-structure.yml:33`
- `.github/workflows/test-structure.yml:57`
- `.github/workflows/test-structure.yml:62`
- `.github/workflows/test-structure.yml:67`
- `.github/workflows/test-wrong-yaml-config.yml:31`
- `.github/workflows/test-wrong-yaml-config.yml:33`
- `.github/workflows/test-wrong-yaml-config.yml:57`
- `.github/workflows/test-wrong-yaml-config.yml:62`
- `.github/workflows/test-wrong-yaml-config.yml:67`

### missing-permissions (severity: medium)

These workflow files have no top-level `permissions:` block and no job-level `permissions:` block on any job. Without explicit permissions, GitHub Actions defaults to the repository's default token permissions (which may be broad), violating the principle of least privilege.

Locations:

- `.github/workflows/build-and-test.yml:1`
- `.github/workflows/test-multiline.yml:1`
- `.github/workflows/test-negative.yml:1`
- `.github/workflows/test-positive.yml:1`
- `.github/workflows/test-query-1.yml:1`
- `.github/workflows/test-query-2.yml:1`
- `.github/workflows/test-query-3.yml:1`
- `.github/workflows/test-structure.yml:1`
- `.github/workflows/test-wrong-yaml-config.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all unpinned action references across 10 workflow files by replacing mutable tags (@v2, @v3, @v4, @main) with pinned 40-character commit SHAs (verified via lookup_action_sha). Added top-level `permissions: {}` blocks to 9 workflow files that were missing them (build-and-test.yml, test-multiline.yml, test-negative.yml, test-positive.yml, test-query-1.yml, test-query-2.yml, test-query-3.yml, test-structure.yml, test-wrong-yaml-config.yml). The branch.yml, codeql.yml, and release.yml files already had permissions blocks and only needed their action references pinned.

