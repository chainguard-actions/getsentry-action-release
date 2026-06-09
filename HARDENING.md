# Hardening Report: getsentry--action-release/v3.7.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `ff50f15e4b79bfbf764dafdfd2579175a6ea9771`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **getsentry--action-release/v3.7.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The composite action step 'Run docker image' references a Docker image using a mutable version tag (`3.7.0`) instead of an immutable SHA digest. This means the image could be replaced with a different (potentially malicious) version without changing the action reference. It should be pinned to a SHA digest, e.g. `docker://ghcr.io/getsentry/action-release-image@sha256:<64-hex-char-digest>`.

Locations:

- `action.yml:131`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image reference at action.yml line 131 from `docker://ghcr.io/getsentry/action-release-image:3.7.0` to `docker://ghcr.io/getsentry/action-release-image@sha256:3d8999c5962c55691cf509b9cc2ebd9d889a398f58a46337992aab4f1645ec7b # 3.7.0` using the immutable SHA digest resolved via the Docker Registry API.

