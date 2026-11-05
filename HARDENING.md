<!-- markdownlint-disable -->

# Hardening Report: getsentry--action-release/v3.7.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `374911c4be584df24e6da57af2d990570ef0f859`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **getsentry--action-release/v3.7.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

A composite step in action.yml uses a Docker image by a mutable tag instead of a sha256 digest: `uses: docker://ghcr.io/getsentry/action-release-image:3.7.1`. Pin it to an @sha256:<digest> reference. The actions/setup-node references are already pinned to full commit SHAs.

Locations:

- `action.yml:184`

### prior-fix (severity: high)

Carried forward from this version's previous harden, which fixed it; fix it again unless the code no longer has the problem. The previous harden changed action.yml without recording a finding for it, and this analysis reported nothing there. Re-apply its security changes unless the code no longer needs them. The previous patch:
```diff
diff --git a/action.yml b/action.yml
index 82b76cc..0ee75b6 100644
--- a/action.yml
+++ b/action.yml
@@ -1,7 +1,6 @@
 name: 'Sentry Release'
 description: 'GitHub Action for creating a release on Sentry'
 author: 'Sentry'
-
 inputs:
   environment:
     description: |-
@@ -132,10 +131,26 @@ inputs:
       You can turn this off by setting this flag.
     default: false
     required: false
-
 runs:
   using: 'composite'
   steps:
     # For actions running on a linux runner, we use a docker
     # approach as it's faster and encapsulates everything needed
     # to run the action.
@@ -167,8 +182,7 @@ runs:
         INPUT_WORKING_DIRECTORY: ${{ inputs.working_directory }}
         INPUT_DISABLE_TELEMETRY: ${{ inputs.disable_telemetry }}
         INPUT_DISABLE_SAFE_DIRECTORY: ${{ inputs.disable_safe_directory }}
-      uses: docker://ghcr.io/getsentry/action-release-image:3.7.1
-
+      uses: docker://ghcr.io/getsentry/action-release-image:3.7.1@sha256:13ae40e0b5abf0cde0b316819c6ed9d256c1d86378eeb1e0f5e86774fc83627a
     # For actions running on macos or windows runners, we use a composite
     # action approach which allows us to install the arch specific sentry-cli
     # binary that's needed for the runner.
@@ -178,7 +192,6 @@ runs:
       shell: bash
       run: |
         git config --global --add safe.directory "$GITHUB_WORKSPACE"
-
     # Save the current Node version before changing it
     - name: Save current Node version
       if: runner.os == 'macOS' || runner.os == 'Windows'
@@ -188,23 +201,20 @@ runs:
         if command -v node &> /dev/null; then
           echo "NODE_VERSION=$(node --version | sed 's/v//')" >> $GITHUB_OUTPUT
         fi
-
     - name: Setup node
       if: runner.os == 'macOS' || runner.os == 'Windows'
       uses: actions/setup-node@53b83947a5a98c8d113130e565377fae1a50d02f # v6.3.0
       with:
         # setup-node doesn't allow absolute paths, so we can't
         # just use `github.action_path` to read this out from the `package.json`
         # any changes to the runtime need to be reflected here
         node-version: 24.14.1
         package-manager-cache: false
-
     - name: Install Sentry CLI v2
       if: runner.os == 'macOS' || runner.os == 'Windows'
       shell: bash
       run: npm install --no-package-lock @sentry/cli@^2.58.6
       working-directory: ${{ github.action_path }}
-
     - name: Run Release Action
       if: runner.os == 'macOS' || runner.os == 'Windows'
       env:
@@ -236,15 +246,13 @@ runs:
       shell: bash
       run: npm run start
       working-directory: ${{ github.action_path }}
-
     # Restore the original Node version
     - name: Restore original Node version
       if: (runner.os == 'macOS' || runner.os == 'Windows') && steps.node_version.outputs.NODE_VERSION != ''
       uses: actions/setup-node@53b83947a5a98c8d113130e565377fae1a50d02f # v6.3.0
       with:
         node-version: ${{ steps.node_version.outputs.NODE_VERSION }}
         package-manager-cache: false
-
 branding:
   icon: 'triangle'
   color: 'purple'

```

Locations:

- `action.yml`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, prior-fix

**Notes:**

Pinned docker://ghcr.io/getsentry/action-release-image:3.7.1 in action.yml to @sha256:13ae40e0b5abf0cde0b316819c6ed9d256c1d86378eeb1e0f5e86774fc83627a. The tag stays inline and the docker:// scheme is kept. The digest came from a registry lookup and is the same one the previous harden used. Pinning the image was the previous patch's only security change, so this one edit also re-applies the prior fix. The actions/setup-node references were already pinned to commit SHAs.

