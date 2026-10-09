<!-- markdownlint-disable -->

# Hardening Report: getsentry--action-release/v3.7.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **getsentry--action-release/v3.7.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The composite action step 'Run docker image' references a Docker image using a mutable version tag (`docker://ghcr.io/getsentry/action-release-image:3.7.1`) instead of an immutable SHA digest. This means the image content could change without notice, enabling a supply-chain attack. It should be pinned to a SHA digest, e.g. `docker://ghcr.io/getsentry/action-release-image@sha256:<64-hex-char-digest>`. The two `uses: actions/setup-node` references are correctly pinned to a full 40-character commit SHA.

Locations:

- `action.yml:148`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image reference in action.yml line 148 from `docker://ghcr.io/getsentry/action-release-image:3.7.1` to `docker://ghcr.io/getsentry/action-release-image:3.7.1@sha256:13ae40e0b5abf0cde0b316819c6ed9d256c1d86378eeb1e0f5e86774fc83627a`. The `docker://` scheme and `:3.7.1` tag are preserved inline. The two `actions/setup-node` references were already pinned to full commit SHAs and required no changes.

