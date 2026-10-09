<!-- markdownlint-disable -->

# Hardening Report: getsentry--action-release/v3.4.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **getsentry--action-release/v3.4.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The composite action step 'Run docker image' references a Docker image using a mutable tag (`docker://ghcr.io/getsentry/action-release-image:3.4.0`) instead of an immutable SHA digest. A mutable tag can be silently updated to point to a different (potentially malicious) image, enabling a supply-chain attack. It should be replaced with a reference pinned to a SHA256 digest, e.g. `docker://ghcr.io/getsentry/action-release-image@sha256:<64-hex-char-digest> # 3.4.0`.

Locations:

- `action.yml:131`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image reference in action.yml line 131 from `docker://ghcr.io/getsentry/action-release-image:3.4.0` to `docker://ghcr.io/getsentry/action-release-image:3.4.0@sha256:49236eb40a1087107bc087445b11dca73b9091bf744e04bc614b8a95763aaad1`. The `docker://` scheme and the tag are preserved inline as required.

