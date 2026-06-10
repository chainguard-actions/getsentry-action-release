<!-- markdownlint-disable -->

# Hardening Report: getsentry--action-release/v3.6.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **getsentry--action-release/v3.6.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The composite action step 'Run docker image' references a Docker image using a mutable tag instead of an immutable SHA digest: `uses: docker://ghcr.io/getsentry/action-release-image:3.6.0`. A tag like `3.6.0` can be overwritten at any time, enabling a supply-chain attack. It should be replaced with a reference pinned to a full SHA256 digest, e.g. `docker://ghcr.io/getsentry/action-release-image@sha256:<64-hex-char-digest>`.

Locations:

- `action.yml:130`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag reference `docker://ghcr.io/getsentry/action-release-image:3.6.0` with the immutable SHA256 digest `docker://ghcr.io/getsentry/action-release-image@sha256:452446e4f748eefec280f0c279606923a36ce9c936d427499ceeeb0930c4f0c0 # 3.6.0` in action.yml at line 130. The digest was resolved via the Docker Registry HTTP API v2.

