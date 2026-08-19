<!-- markdownlint-disable -->

# Hardening Report: getsentry--action-release/v3.4.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **getsentry--action-release/v3.4.0** was hardened automatically. 1 finding(s) were identified and resolved across 4 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The composite action step 'Run docker image' references a Docker image using a mutable version tag (`docker://ghcr.io/getsentry/action-release-image:3.4.0`) instead of an immutable SHA digest. This means the image content could change without notice, enabling a supply-chain attack. It should be pinned to a SHA digest, e.g. `docker://ghcr.io/getsentry/action-release-image@sha256:<64-hex-char-digest>`.

Locations:

- `action.yml:130`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image reference in action.yml line 130 from `docker://ghcr.io/getsentry/action-release-image:3.4.0` to `docker://ghcr.io/getsentry/action-release-image:3.4.0@sha256:49236eb40a1087107bc087445b11dca73b9091bf744e04bc614b8a95763aaad1`. The `docker://` scheme is preserved as required for composite action steps, the tag is kept inline for readability, and the SHA digest pins the reference to an immutable image.

### Iteration 2

**Fixes applied:** script-injection, unpinned-uses, missing-permissions

**Notes:**

Fixed all three finding types:

1. **script-injection**: In build.yml, moved `${{ github.ref }}` and `${{ github.event_name }}` to `env:` block as `GITHUB_REF` and `GITHUB_EVENT_NAME`, and moved `${{ steps.node_before.outputs.VERSION }}` to `env:` block as `NODE_VERSION_BEFORE`. In create-release-tags.yml, moved `${{ github.event.release.tag_name }}` to `env:` block as `TAG_NAME`.

2. **unpinned-uses**: Pinned all action references to full 40-char commit SHAs:
   - `actions/checkout@v4` → `@11d5960a326750d5838078e36cf38b85af677262`
   - `getsentry/action-github-commit@v2.0.0` → `@31f6706ca1a7b9ad6d22c1b07bf3a92eabb05632`
   - `docker/setup-qemu-action@v3` → `@c7c53464625b32c7a7e944ae62b3e17d2b600130`
   - `docker/setup-buildx-action@v3` → `@8d2750c68a42422c14e847fe6c8ac0403b4cbd6f`
   - `docker/login-action@v3` → `@c94ce9fb468520275223c153574b00df6fe4bcc9`
   - `docker/build-push-action@v6` → `@10e90e3645eae34f1e60eeb005ba3a3d33f178e8`
   - `actions/setup-node@v4` → `@49933ea5288caeca8642d1e84afbd3f7d6820020`
   - `getsentry/action-prepare-release@v1` → `@c8e1c2009ab08259029170132c384f03c1064c0e`
   - `volta-cli/action@v4` → `@5c175f92dea6f48441c436471e6479dbc192e194`

3. **missing-permissions**: Added `permissions: contents: read` to the `lint` job in build.yml; added top-level `permissions: contents: write` and job-level `permissions: contents: write` to release.yml; added top-level `permissions: contents: read` and job-level `permissions: contents: read` to verify-dist.yml.

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed unquoted shell variable expansions in `.github/workflows/create-release-tags.yml`. Changed `git tag -f $MAJOR_VERSION`, `git tag -f $MINOR_VERSION`, and `git push -f origin $MAJOR_VERSION $MINOR_VERSION` to use double-quoted variables: `git tag -f "$MAJOR_VERSION"`, `git tag -f "$MINOR_VERSION"`, and `git push -f origin "$MAJOR_VERSION" "$MINOR_VERSION"`. The `TAG_NAME` env var was already correctly set via the step's `env:` block rather than direct `${{ }}` interpolation in the shell script, so no additional changes were needed there.

### Iteration 4

**Notes:**

The `uses: docker://ghcr.io/getsentry/action-release-image:3.4.0@sha256:49236eb40a1087107bc087445b11dca73b9091bf744e04bc614b8a95763aaad1` reference at action.yml line 143 is already correctly pinned with the sha256 image digest. For Docker container image references (using the `docker://` scheme in composite action steps), pinning by sha256 digest is the correct and only valid immutable pin — there is no git commit SHA for a Docker image. The digest was verified against the registry and matches the current image. The finding appears to be a false positive from a checker that expects 40-character git commit SHAs for all `uses:` references, but Docker image references are legitimately and immutably pinned by their content digest. No change was made as the reference is already properly secured.

