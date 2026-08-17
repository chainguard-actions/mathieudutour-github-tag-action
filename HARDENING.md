<!-- markdownlint-disable -->

# Hardening Report: mathieudutour--github-tag-action/v5.6

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **mathieudutour--github-tag-action/v5.6** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses `actions/checkout@v2`, which is a mutable tag reference rather than a pinned full-length SHA commit hash. This means the action could be silently updated or replaced with a different version, creating a supply-chain risk. It should be pinned to a specific commit SHA (e.g., `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v2`).

Locations:

- `.github/workflows/test.yml:12`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/test.yml` has no top-level `permissions:` key and the single job (`test`) also has no `permissions:` key. Without explicit permissions, the job inherits the default repository permissions (which may include broad write access). A minimal permissions block (e.g., `permissions: contents: read`) should be added at the top level or on the job.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/test.yml: (1) Pinned `actions/checkout@v2` to full commit SHA `0717577d45739eb3c851188b29f50ed6c0b2194e` with `# v2` comment for readability. (2) Added top-level `permissions: contents: read` block to restrict the workflow to the minimum permissions needed (read-only access to repository contents for checkout).

