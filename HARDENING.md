# Hardening Report: getsentry--action-release/v3.5.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `ff50f15e4b79bfbf764dafdfd2579175a6ea9771`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **getsentry--action-release/v3.5.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The step 'Run docker image' in action.yml references a Docker image using a mutable version tag (`docker://ghcr.io/getsentry/action-release-image:3.5.0`) instead of an immutable SHA digest. If the image at tag `3.5.0` is overwritten or the registry is compromised, a different (potentially malicious) image could be executed. It should be pinned to a SHA digest, e.g. `docker://ghcr.io/getsentry/action-release-image@sha256:<64-hex-char-digest>`.

Locations:

- `action.yml:130`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image reference in action.yml from the mutable tag `ghcr.io/getsentry/action-release-image:3.5.0` to the immutable digest `ghcr.io/getsentry/action-release-image@sha256:761c31d9ffd6aaa03cb607d295f6c18b165fb5ac2fb7b8bc537a2bb18c5a0fcd # 3.5.0`. The original tag is preserved as a comment for readability.

