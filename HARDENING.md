<!-- markdownlint-disable -->

# Hardening Report: getsentry--action-release/v3.5.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **getsentry--action-release/v3.5.0** was hardened automatically. 1 finding(s) were identified and resolved across 3 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yml references a Docker image using a mutable version tag instead of an immutable SHA digest. `uses: docker://ghcr.io/getsentry/action-release-image:3.5.0` uses the tag `3.5.0`, which can be silently overwritten by the registry, enabling supply-chain attacks. It should be replaced with a reference pinned to a SHA digest, e.g. `docker://ghcr.io/getsentry/action-release-image@sha256:<64-hex-char-digest>`.

Locations:

- `action.yml:138`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image reference in action.yml line 138 from the mutable tag `ghcr.io/getsentry/action-release-image:3.5.0` to the immutable digest `ghcr.io/getsentry/action-release-image:3.5.0@sha256:761c31d9ffd6aaa03cb607d295f6c18b165fb5ac2fb7b8bc537a2bb18c5a0fcd`. The `docker://` scheme and the `:3.5.0` tag were preserved inline as required.

### Iteration 2

**Fixes applied:** script-injection, unpinned-uses, missing-permissions

**Notes:**

Fixed all findings across 4 workflow files:

**script-injection** (4 locations):
- build.yml 'Get docker tag': moved `${{ github.ref }}` and `${{ github.event_name }}` to env vars `GH_REF` and `GH_EVENT_NAME`
- build.yml 'Print Node Version (After)': moved `${{ steps.node_before.outputs.VERSION }}` to env var `NODE_VERSION_BEFORE`
- create-release-tags.yml 'Create and push major and minor version tags': moved `${{ github.event.release.tag_name }}` to env var `TAG_NAME`

**unpinned-uses** (14 locations): Pinned all action references to full 40-char SHAs:
- actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262
- getsentry/action-github-commit@v2.0.0 → @31f6706ca1a7b9ad6d22c1b07bf3a92eabb05632
- docker/setup-qemu-action@v3 → @c7c53464625b32c7a7e944ae62b3e17d2b600130
- docker/setup-buildx-action@v3 → @8d2750c68a42422c14e847fe6c8ac0403b4cbd6f
- docker/login-action@v3 → @c94ce9fb468520275223c153574b00df6fe4bcc9
- docker/build-push-action@v6 → @10e90e3645eae34f1e60eeb005ba3a3d33f178e8
- actions/setup-node@v4 → @49933ea5288caeca8642d1e84afbd3f7d6820020
- getsentry/action-prepare-release@v1 → @c8e1c2009ab08259029170132c384f03c1064c0e
- volta-cli/action@v4 → @5c175f92dea6f48441c436471e6479dbc192e194

**missing-permissions** (3 jobs):
- build.yml lint job: added `permissions: contents: read`
- release.yml release job: added `permissions: contents: write`
- verify-dist.yml check-dist job: added `permissions: contents: read`

### Iteration 1

**Fixes applied:** script-injection

**Notes:**

Fixed script injection in `.github/workflows/create-release-tags.yml` by double-quoting `$MAJOR_VERSION` and `$MINOR_VERSION` in the three shell commands (`git tag -f`, `git tag -f`, and `git push -f origin`). These variables are derived from `TAG_NAME` which is set from `${{ github.event.release.tag_name }}` — an attacker-controllable value. Without quotes, a crafted tag name containing shell metacharacters could cause arbitrary command execution. The `TAG_NAME` was already correctly isolated in the step's `env:` block; only the quoting of the derived variables was missing.

