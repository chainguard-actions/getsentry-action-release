# Hardening Report: getsentry--action-release/v3.5.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `ff50f15e4b79bfbf764dafdfd2579175a6ea9771`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **getsentry--action-release/v3.5.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yml references a Docker image using a mutable tag instead of a SHA digest: `uses: docker://ghcr.io/getsentry/action-release-image:3.5.0`. A tag like `3.5.0` can be overwritten to point to a different image, enabling supply-chain attacks. It should be replaced with a reference pinned to a full SHA256 digest, e.g. `docker://ghcr.io/getsentry/action-release-image@sha256:<64-hex-char-digest>`.

Locations:

- `action.yml:116`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Fixed the unpinned Docker image reference in action.yml line 116. Replaced `docker://ghcr.io/getsentry/action-release-image:3.5.0` with `docker://ghcr.io/getsentry/action-release-image@sha256:761c31d9ffd6aaa03cb607d295f6c18b165fb5ac2fb7b8bc537a2bb18c5a0fcd # 3.5.0`. The SHA256 digest was resolved via the Docker Registry HTTP API v2 and is immutable, preventing supply-chain attacks via tag mutation.

