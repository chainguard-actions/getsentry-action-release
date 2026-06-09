# Hardening Report: getsentry--action-release/v3.6.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `ff50f15e4b79bfbf764dafdfd2579175a6ea9771`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **getsentry--action-release/v3.6.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The composite action step 'Run docker image' references a Docker image using a mutable version tag ('3.6.1') instead of an immutable SHA digest. This means the image could be silently replaced with a different (potentially malicious) version without any change to the action.yml file. The reference `uses: docker://ghcr.io/getsentry/action-release-image:3.6.1` should be replaced with a SHA-pinned form such as `uses: docker://ghcr.io/getsentry/action-release-image@sha256:<64-hex-char-digest>`. Note: the two `actions/setup-node` references are correctly pinned to SHA `53b83947a5a98c8d113130e565377fae1a50d02f`.

Locations:

- `action.yml:138`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag reference `docker://ghcr.io/getsentry/action-release-image:3.6.1` with the immutable SHA digest `docker://ghcr.io/getsentry/action-release-image@sha256:963c9e205ca7ebf35b5204a50462108ff456b8aab98d04729a15a0b668c3beb4 # 3.6.1` in action.yml at line 138. The original tag is preserved as a comment for readability.

