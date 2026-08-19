<!-- markdownlint-disable -->

# Hardening Report: mathieudutour--github-tag-action/v6.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **mathieudutour--github-tag-action/v6.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses actions/checkout@v2, which is a mutable tag reference rather than a pinned 40-character commit SHA. This means the action could be silently updated to a different (potentially malicious) version without any change to the workflow file, creating a supply-chain risk.

Locations:

- `.github/workflows/test.yml:12`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key, and the only job (`test`) also has no job-level `permissions:` key. Without explicit permissions, the GITHUB_TOKEN is granted its default (broad) permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/test.yml: (1) Pinned actions/checkout@v2 to full SHA 0717577d45739eb3c851188b29f50ed6c0b2194e with '# v2' comment for readability. (2) Added top-level 'permissions: {}' block to enforce least-privilege — the workflow only runs npm CI/test/build commands and requires no GITHUB_TOKEN permissions.

