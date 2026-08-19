<!-- markdownlint-disable -->

# Hardening Report: getsentry--action-release/v3.6.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **getsentry--action-release/v3.6.1** was hardened automatically. 1 finding(s) were identified and resolved across 2 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The composite action step 'Run docker image' references a Docker image using a mutable version tag (`docker://ghcr.io/getsentry/action-release-image:3.6.1`) instead of an immutable SHA digest. This means the image could be silently replaced with a different (potentially malicious) version without any change to the action.yml file. It should be pinned to a SHA digest, e.g. `docker://ghcr.io/getsentry/action-release-image@sha256:<64-hex-char-digest>`.

Locations:

- `action.yml:131`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image reference in action.yml line 131 from `docker://ghcr.io/getsentry/action-release-image:3.6.1` to `docker://ghcr.io/getsentry/action-release-image:3.6.1@sha256:963c9e205ca7ebf35b5204a50462108ff456b8aab98d04729a15a0b668c3beb4`. The `docker://` scheme and `:3.6.1` tag are preserved inline, with the immutable digest appended to prevent silent image replacement.

### Iteration 2

**Fixes applied:** script-injection, missing-permissions

**Notes:**

Fixed three findings: (1) create-release-tags.yml: moved `${{ github.event.release.tag_name }}` out of the run shell into an env var `TAG_NAME`, replacing single-quoted template interpolation with `"$TAG_NAME"`. (2) build.yml 'Print Node Version (After)' step: moved `${{ steps.node_before.outputs.VERSION }}` into an env var `VERSION_BEFORE` and replaced all three occurrences in the shell script. (3) build.yml lint job: added `permissions: {}` since the lint job only runs yarn commands and needs no GitHub API permissions.

