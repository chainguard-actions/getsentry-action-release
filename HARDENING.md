<!-- markdownlint-disable -->

# Hardening Report: getsentry--action-release/v3.7.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **getsentry--action-release/v3.7.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The composite action step 'Run docker image' references a Docker image using a mutable tag (`docker://ghcr.io/getsentry/action-release-image:3.7.0`) instead of an immutable SHA digest. This means the image could be replaced with a different (potentially malicious) version without changing the action reference. It should be pinned to a SHA digest, e.g. `docker://ghcr.io/getsentry/action-release-image@sha256:<64-hex-char-digest>`.

Locations:

- `action.yml:130`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image reference in action.yml line 130 from the mutable tag `ghcr.io/getsentry/action-release-image:3.7.0` to the immutable digest `ghcr.io/getsentry/action-release-image@sha256:3d8999c5962c55691cf509b9cc2ebd9d889a398f58a46337992aab4f1645ec7b` with a `# 3.7.0` comment for readability.

