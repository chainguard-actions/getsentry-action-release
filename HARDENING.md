# Hardening Report: getsentry--action-release/v3.6.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `ff50f15e4b79bfbf764dafdfd2579175a6ea9771`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **getsentry--action-release/v3.6.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yml references a Docker image using a mutable version tag instead of an immutable SHA digest. `uses: docker://ghcr.io/getsentry/action-release-image:3.6.1` can be silently replaced by a different image if the tag is overwritten in the registry, enabling a supply-chain attack. It should be pinned to a SHA digest, e.g. `docker://ghcr.io/getsentry/action-release-image@sha256:<64-hex-char-digest>`.

Note: The two `actions/setup-node` references are correctly pinned to SHA `53b83947a5a98c8d113130e565377fae1a50d02f` and are not a concern.

Locations:

- `action.yml:148`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag `ghcr.io/getsentry/action-release-image:3.6.1` with the immutable SHA digest `ghcr.io/getsentry/action-release-image@sha256:963c9e205ca7ebf35b5204a50462108ff456b8aab98d04729a15a0b668c3beb4 # 3.6.1` in action.yml at line 148. The two `actions/setup-node` references were already correctly pinned and required no changes.

