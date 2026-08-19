<!-- markdownlint-disable -->

# Hardening Report: getsentry--action-release/v3.6.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **getsentry--action-release/v3.6.0** was hardened automatically. 1 finding(s) were identified and resolved across 2 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yml references a Docker image using a mutable version tag (`3.6.0`) instead of an immutable SHA digest. This means the image could be silently replaced with a different (potentially malicious) version. The reference `docker://ghcr.io/getsentry/action-release-image:3.6.0` should be replaced with a SHA-pinned form such as `docker://ghcr.io/getsentry/action-release-image@sha256:<64-hex-char-digest>`.

Locations:

- `action.yml:118`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image reference in action.yml from the mutable tag `ghcr.io/getsentry/action-release-image:3.6.0` to the immutable digest form `ghcr.io/getsentry/action-release-image:3.6.0@sha256:452446e4f748eefec280f0c279606923a36ce9c936d427499ceeeb0930c4f0c0`. The `docker://` scheme and the version tag are both preserved inline for readability and correctness.

### Iteration 1

**Fixes applied:** script-injection, missing-permissions

**Notes:**

Fixed all four findings:
1. build.yml 'Get docker tag' step: moved ${{ github.ref }} and ${{ github.event_name }} into env block as GITHUB_REF and GITHUB_EVENT_NAME.
2. build.yml 'Print Node Version (After)' step: moved ${{ steps.node_before.outputs.VERSION }} into env block as NODE_VERSION_BEFORE.
3. build.yml lint job: added `permissions: contents: read` job-level block.
4. create-release-tags.yml 'Create and push major and minor version tags' step: moved ${{ github.event.release.tag_name }} into env block as TAG_NAME.
5. verify-dist.yml: added top-level `permissions: contents: read` block.

