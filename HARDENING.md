<!-- markdownlint-disable -->

# Hardening Report: getsentry--action-release/v3.6.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **getsentry--action-release/v3.6.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The composite action uses a Docker image reference with a mutable tag (`3.6.1`) instead of an immutable SHA digest. If the image at that tag is replaced, the action will silently execute different code. The reference `uses: docker://ghcr.io/getsentry/action-release-image:3.6.1` should be replaced with a SHA-pinned form such as `docker://ghcr.io/getsentry/action-release-image@sha256:<64-hex-char-digest>`.

Locations:

- `action.yml:115`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag reference `docker://ghcr.io/getsentry/action-release-image:3.6.1` with the immutable SHA-pinned form `docker://ghcr.io/getsentry/action-release-image@sha256:963c9e205ca7ebf35b5204a50462108ff456b8aab98d04729a15a0b668c3beb4 # 3.6.1` in action.yml at line 115.

