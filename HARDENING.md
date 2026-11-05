<!-- markdownlint-disable -->

# Hardening Report: getsentry--action-release/v3.7.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `374911c4be584df24e6da57af2d990570ef0f859`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **getsentry--action-release/v3.7.2** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The composite step 'Run docker image' points to a Docker image by a changeable tag instead of a sha256 digest: `uses: docker://ghcr.io/getsentry/action-release-image:3.7.2`. Whoever controls that tag can change which image runs. Pin it to a digest instead, e.g. `docker://ghcr.io/getsentry/action-release-image@sha256:<digest> # 3.7.2`.

Locations:

- `action.yml:172`

### prior-fix (severity: high)

Carried forward from this version's previous harden, which fixed it; fix it again unless the code no longer has the problem. The previous harden changed action.yml without recording a finding for it, and this analysis reported nothing there. Re-apply its security changes unless the code no longer needs them. The previous patch:
```diff
diff --git a/action.yml b/action.yml
index 4ee9836..bbdde4b 100644
--- a/action.yml
+++ b/action.yml
@@ -136,6 +136,23 @@ inputs:
 runs:
   using: 'composite'
   steps:
     # For actions running on a linux runner, we use a docker
     # approach as it's faster and encapsulates everything needed
     # to run the action.
@@ -167,7 +184,7 @@ runs:
         INPUT_WORKING_DIRECTORY: ${{ inputs.working_directory }}
         INPUT_DISABLE_TELEMETRY: ${{ inputs.disable_telemetry }}
         INPUT_DISABLE_SAFE_DIRECTORY: ${{ inputs.disable_safe_directory }}
-      uses: docker://ghcr.io/getsentry/action-release-image:3.7.2
+      uses: docker://ghcr.io/getsentry/action-release-image:3.7.2@sha256:42ecb0b701b0600bde998ba12447582a76a320525fbb66128b2eedffa7a4f9ea
 
     # For actions running on macos or windows runners, we use a composite
     # action approach which allows us to install the arch specific sentry-cli
@@ -191,7 +208,7 @@ runs:
 
     - name: Setup node
       if: runner.os == 'macOS' || runner.os == 'Windows'
       uses: actions/setup-node@53b83947a5a98c8d113130e565377fae1a50d02f # v6.3.0
       with:
         # setup-node doesn't allow absolute paths, so we can't
         # just use `github.action_path` to read this out from the `package.json`
@@ -240,7 +257,7 @@ runs:
     # Restore the original Node version
     - name: Restore original Node version
       if: (runner.os == 'macOS' || runner.os == 'Windows') && steps.node_version.outputs.NODE_VERSION != ''
       uses: actions/setup-node@53b83947a5a98c8d113130e565377fae1a50d02f # v6.3.0
       with:
         node-version: ${{ steps.node_version.outputs.NODE_VERSION }}
         package-manager-cache: false

```

Locations:

- `action.yml`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, prior-fix

**Notes:**

Pinned docker://ghcr.io/getsentry/action-release-image:3.7.2 to @sha256:42ecb0b701b0600bde998ba12447582a76a320525fbb66128b2eedffa7a4f9ea, keeping the tag in the reference. This is the same digest the previous harden used, so it reapplies that change. Both actions/setup-node uses were already pinned to a commit SHA (v6.3.0), so they needed no change.

