# Hardening Report: getsentry--action-release/v3.6.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `ff50f15e4b79bfbf764dafdfd2579175a6ea9771`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **getsentry--action-release/v3.6.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yml references a Docker image using a mutable version tag (`3.6.0`) instead of an immutable SHA digest. This means the image could be replaced with a different (potentially malicious) version without changing the workflow. The reference `uses: docker://ghcr.io/getsentry/action-release-image:3.6.0` should be replaced with a SHA-pinned form such as `uses: docker://ghcr.io/getsentry/action-release-image@sha256:<64-hex-char-digest>`. The two `actions/setup-node` references are correctly pinned to a full commit SHA and pass.

Locations:

- `action.yml:130`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag reference `docker://ghcr.io/getsentry/action-release-image:3.6.0` with the immutable SHA-pinned form `docker://ghcr.io/getsentry/action-release-image@sha256:452446e4f748eefec280f0c279606923a36ce9c936d427499ceeeb0930c4f0c0 # 3.6.0` in action.yml at line 130. The digest was resolved via the Docker Registry HTTP API v2.

