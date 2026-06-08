# Hardening Report: getsentry--action-release/v3.4.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `ff50f15e4b79bfbf764dafdfd2579175a6ea9771`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **getsentry--action-release/v3.4.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yml references a Docker image using a mutable tag (`3.4.0`) instead of an immutable SHA digest. This means the image could be changed without notice, enabling a supply-chain attack. The failing reference is: `uses: docker://ghcr.io/getsentry/action-release-image:3.4.0`. It should be replaced with a SHA-pinned reference such as `docker://ghcr.io/getsentry/action-release-image@sha256:<64-hex-char-digest>`.

Locations:

- `action.yml:119`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag reference `docker://ghcr.io/getsentry/action-release-image:3.4.0` with the immutable SHA-pinned reference `docker://ghcr.io/getsentry/action-release-image@sha256:49236eb40a1087107bc087445b11dca73b9091bf744e04bc614b8a95763aaad1 # 3.4.0` in action.yml at line 119. The digest was resolved using the Docker Registry HTTP API v2.

