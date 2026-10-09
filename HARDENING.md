<!-- markdownlint-disable -->

# Hardening Report: getsentry--action-release/v3.5.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **getsentry--action-release/v3.5.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The composite action step 'Run docker image' references a Docker image using a mutable version tag (`3.5.0`) instead of an immutable SHA digest. This means the image could be replaced with a different (potentially malicious) version without changing the action reference. The failing reference is: `uses: docker://ghcr.io/getsentry/action-release-image:3.5.0`. It should be pinned to a SHA digest, e.g. `uses: docker://ghcr.io/getsentry/action-release-image@sha256:<64-hex-char-digest>`. The two `actions/setup-node@49933ea5288caeca8642d1e84afbd3f7d6820020` references are correctly pinned.

Locations:

- `action.yml:143`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image reference `ghcr.io/getsentry/action-release-image:3.5.0` to its immutable SHA digest in action.yml line 143. The updated reference is `docker://ghcr.io/getsentry/action-release-image:3.5.0@sha256:761c31d9ffd6aaa03cb607d295f6c18b165fb5ac2fb7b8bc537a2bb18c5a0fcd`, preserving both the `docker://` scheme and the version tag inline.

