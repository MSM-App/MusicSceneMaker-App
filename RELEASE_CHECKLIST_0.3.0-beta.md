# MusicSceneMaker 0.3.0 Director Cut Beta — release checklist

> Internal checklist. Do not publish the candidate installer until all required gates are checked.

## A. Source of truth

- [ ] Connect to the development workstation.
- [ ] Verify the working directory: `MusicSceneMaker_Dev_0.3_Director_Cut_Beta`.
- [ ] Verify current branch and HEAD commit.
- [ ] Inspect `git status`, staged changes and untracked files.
- [ ] Compare current working tree with the latest pushed private Source branch.
- [ ] Preserve all valid 0.3 changes; do not reset or overwrite the worktree.
- [ ] Review all diffs after 0.2.4 Beta 2, including changes made 15–24 November.
- [ ] Exclude local user projects, generated videos, model weights, tokens, credentials, machine-specific paths and temporary test data.
- [ ] Confirm required licenses and THIRD_PARTY_NOTICES are current.

## B. Documentation

- [ ] Review CHANGELOG_0.3.0-beta.md against the actual diff.
- [ ] Review TESTING_GUIDE_0.3.0-beta.md against the actual UI.
- [ ] Review KNOWN_ISSUES_0.3.0-beta.md against the candidate build.
- [ ] Record exact test commands and results.
- [ ] Record all baseline failures separately from new regressions.
- [ ] Update README only after the release candidate is verified.

## C. Build

- [ ] Confirm package version and product name.
- [ ] Confirm app icon, installer metadata and Windows x64 target.
- [ ] Run TypeScript checks.
- [ ] Run frontend production build.
- [ ] Run the appropriate Rust test suite.
- [ ] Run the relevant Node / React regression suites.
- [ ] Build the Tauri release executable.
- [ ] Build NSIS x64 installer.
- [ ] Record skipped targets and reasons; do not report MSI as built if it was skipped.
- [ ] Ensure build artifacts are from the final commit.

## D. Smoke test

- [ ] Install on the development workstation.
- [ ] Launch and close the app cleanly.
- [ ] Verify first-run component status and paths.
- [ ] Open an existing test project copy.
- [ ] Create and save a new project.
- [ ] Verify Writer / Director basic flow.
- [ ] Verify character cards and scene image selection.
- [ ] Verify MiniMax H3 T2V.
- [ ] Verify MiniMax H3 I2V.
- [ ] Verify Fast H3 Omni routing with references.
- [ ] Verify Pika H3 Flex resolution warning and actual native output.
- [ ] Verify a short Continuity Chain.
- [ ] Verify queue of selected images with the real engine.
- [ ] Verify YuE2 quick markup and Voice Map.
- [ ] Verify export of one ready scene.
- [ ] Capture diagnostics if ComfyUI crashes.
- [ ] Do not disable Block Sparse Attention or VSA to make the test pass.

## E. Release metadata

- [ ] Choose final tag (for example, `v0.3.0-beta.1`) only after build verification.
- [ ] Record source commit SHA.
- [ ] Record installer filename and exact byte size.
- [ ] Calculate SHA-256.
- [ ] Record Windows version and build environment.
- [ ] Upload the installer to a GitHub pre-release.
- [ ] Verify download URL and checksum after upload.
- [ ] Publish tester guide and known-issues page.
- [ ] Announce that this is a beta and collect structured reports.

## F. Public release must not claim

- [ ] No claim that VSA root cause is fixed unless proven.
- [ ] No claim that 8 GB / 24 GB physical GPUs passed unless tested on hardware.
- [ ] No claim that every model/engine is fully accepted.
- [ ] No claim that StudioPolish real-time A/B playback is complete unless verified.
- [ ] No claim that partial export has passed full FFmpeg acceptance unless verified.
- [ ] No claim that the image queue passed real-engine testing unless verified.
