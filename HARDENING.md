<!-- markdownlint-disable -->

# Hardening Report: mathieudutour--github-tag-action/v6.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **mathieudutour--github-tag-action/v6.2** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file uses mutable tag references instead of pinned SHA digests. `actions/checkout@v4` and `actions/setup-node@v4` both use version tags (`@v4`) which can be silently updated or hijacked. Each should be pinned to a full 40-character commit SHA (e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`).

Locations:

- `.github/workflows/test.yml:12`
- `.github/workflows/test.yml:13`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the single job (`test`) also has no `permissions:` key. Without explicit permissions, the job inherits the default repository token permissions, which may be broader than necessary. A minimal `permissions:` block (e.g. `contents: read`) should be added at the top level or on the job.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/test.yml: (1) Pinned actions/checkout@v4 to SHA 11d5960a326750d5838078e36cf38b85af677262 and actions/setup-node@v4 to SHA 49933ea5288caeca8642d1e84afbd3f7d6820020, preserving the version tags as comments. (2) Added top-level `permissions: contents: read` block to restrict the default GITHUB_TOKEN to the minimum needed for a test workflow.

