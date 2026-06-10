<!-- markdownlint-disable -->

# Hardening Report: getsentry--action-release/v3.5.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **getsentry--action-release/v3.5.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yml references a Docker image using a mutable version tag (`3.5.0`) instead of an immutable SHA digest. This means the image pulled at runtime could change without notice, enabling a supply-chain attack. The reference `docker://ghcr.io/getsentry/action-release-image:3.5.0` should be replaced with a SHA-pinned form such as `docker://ghcr.io/getsentry/action-release-image@sha256:<64-hex-char-digest>`.

The two `uses: actions/setup-node@49933ea5288caeca8642d1e84afbd3f7d6820020` references are correctly SHA-pinned and are not findings.

Locations:

- `action.yml:131`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag `ghcr.io/getsentry/action-release-image:3.5.0` with the immutable SHA-pinned reference `ghcr.io/getsentry/action-release-image@sha256:761c31d9ffd6aaa03cb607d295f6c18b165fb5ac2fb7b8bc537a2bb18c5a0fcd # 3.5.0` in action.yml line 131. The two `actions/setup-node@49933ea5288caeca8642d1e84afbd3f7d6820020` references were already correctly pinned and required no changes.

