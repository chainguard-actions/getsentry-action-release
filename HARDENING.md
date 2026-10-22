<!-- markdownlint-disable -->

# Hardening Report: getsentry--action-release/v3.7.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **getsentry--action-release/v3.7.2** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

action.yml has a step that runs a container image by mutable tag instead of an immutable sha256 digest: `uses: docker://ghcr.io/getsentry/action-release-image:3.7.2`. Whoever controls that tag can change the image, which makes this a supply-chain risk. Pin it as `docker://ghcr.io/getsentry/action-release-image@sha256:<digest> # 3.7.2`. Both actions/setup-node references are already pinned to a full commit SHA.

Locations:

- `action.yml:182`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned docker://ghcr.io/getsentry/action-release-image:3.7.2 to its digest. The reference is now docker://ghcr.io/getsentry/action-release-image:3.7.2@sha256:42ecb0b701b0600bde998ba12447582a76a320525fbb66128b2eedffa7a4f9ea. The docker:// scheme and the tag stay inline, as the hardening rules require. The actions/setup-node references were already pinned to a commit SHA.

