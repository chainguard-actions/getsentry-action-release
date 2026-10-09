<!-- markdownlint-disable -->

# Hardening Report: getsentry--action-release/v3.6.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **getsentry--action-release/v3.6.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The composite action step 'Run docker image' references a Docker image by mutable version tag rather than an immutable SHA digest: `uses: docker://ghcr.io/getsentry/action-release-image:3.6.0`. If the image at tag 3.6.0 is overwritten (e.g. by a supply-chain compromise), the action will silently execute the new, potentially malicious image. It should be pinned to a SHA256 digest, e.g. `uses: docker://ghcr.io/getsentry/action-release-image@sha256:<64-hex-char-digest> # 3.6.0`.

Locations:

- `action.yml:148`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image reference in action.yml from `docker://ghcr.io/getsentry/action-release-image:3.6.0` to `docker://ghcr.io/getsentry/action-release-image:3.6.0@sha256:452446e4f748eefec280f0c279606923a36ce9c936d427499ceeeb0930c4f0c0`. The tag is kept inline and the `docker://` scheme is preserved to ensure GitHub Actions correctly interprets it as a Docker container action.

