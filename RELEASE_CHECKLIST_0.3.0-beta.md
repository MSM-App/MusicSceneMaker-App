# MusicSceneMaker 0.3.0 Director Cut Beta — release checklist

> Internal checklist. The NSIS candidate is built, but do not publish a public download until installation and live smoke tests are completed.

## A. Source of truth

- [x] Connect to the development workstation.
- [x] Verify the working directory: MusicSceneMaker_Dev_0.3_Director_Cut_Beta.
- [x] Verify current branch and HEAD commit.
- [x] Inspect git status, staged changes and untracked files.
- [x] Compare current working tree with the latest pushed private Source branch.
- [x] Preserve all valid 0.3 changes; no reset, clean or mass restore was used.
- [x] Review the 0.3 source diff after the 0.2.4 / 0.2.5 baseline.
- [x] Exclude local user projects, generated videos, model weights, tokens, credentials, machine-specific paths and temporary test data.
- [x] Review/update THIRD_PARTY_NOTICES.
- [x] Push the complete source to private branch release/0.3.0-beta; draft source PR #3 is open.

## B. Documentation

- [x] Review CHANGELOG_0.3.0-beta.md against the source worktree and development journal.
- [x] Review TESTING_GUIDE_0.3.0-beta.md against the current UI.
- [x] Review KNOWN_ISSUES_0.3.0-beta.md against the candidate build and remaining acceptance work.
- [x] Record exact test commands and results.
- [x] Record previous Rust failures separately from the final passing run.
- [ ] Update the public README after the candidate is approved for publication.

## C. Build

- [x] Confirm package version 0.3.0-beta and product name MusicSceneMaker Director Cut.
- [x] Confirm separate application identifier app.musicscenemaker.beta030.
- [x] Confirm app icon and Windows x64 target.
- [x] Run TypeScript checks.
- [x] Run frontend production build.
- [x] Run Rust unit tests: 3,432 passed, 0 failed, 67 ignored.
- [x] Run Node / React audit: 21/21 passed.
- [x] Build Tauri release executable from source commit 12eda0fecc3ef2988890f08166e442218b7280fc.
- [x] Build NSIS x64 installer.
- [x] Record skipped MSI target and reason: prerelease identifier “beta” is not numeric-only; NSIS succeeded.
- [x] Verify NSIS archive integrity with 7-Zip (66 files).
- [x] Confirm build artifacts were produced from the final source commit; worktree remained clean.

## D. Smoke test — NOT YET PERFORMED

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

- [ ] Choose final tag (for example, v0.3.0-beta.1) only after smoke-test review.
- [x] Record source commit SHA: 12eda0fecc3ef2988890f08166e442218b7280fc.
- [x] Record installer filename, exact byte size and SHA-256 in BUILD_MANIFEST_0.3.0-beta.md.
- [x] Record Windows version and build environment.
- [ ] Upload installer to a GitHub pre-release.
- [ ] Verify download URL and checksum after upload.
- [ ] Merge/publish tester guide and known-issues page after review.
- [ ] Announce the beta and collect structured reports.

## F. Public release must not claim

- [x] Do not claim the VSA root cause is fixed; it remains open.
- [x] Do not claim 8 GB / 24 GB physical GPUs passed; those paths were simulated.
- [x] Do not claim every model/engine is fully accepted.
- [x] Do not claim StudioPolish real-time A/B playback is complete.
- [x] Do not claim partial export has passed full FFmpeg acceptance.
- [x] Do not claim the image queue passed real-engine testing.
- [x] Clearly state that the NSIS installer is unsigned and that MSI was not produced.
