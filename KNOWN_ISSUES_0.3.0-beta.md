# MusicSceneMaker 0.3.0 Director Cut Beta — known issues and validation status

> This is a pre-release register assembled from development reports through 24 November 2026. Re-check every item against the final candidate build before publication.

## Critical / release-blocking validation

### ComfyUI Python crash in SparseAttnPatch.reset()

- **Observed:** Python process aborts in `SparseAttnPatch.reset()` during cleanup after sampler, before the first denoising step completes.
- **VSA observation:** adaptive grouping reduced the head group from 56 to 2.
- **Root cause:** not established.
- **Mitigation/diagnostics:** adaptive VSA head grouping is implemented; emergency diagnostics record process exit code, last node, available graph, RAM/VRAM measurements and Python log tail. UI action: «Открыть диагностику».
- **Constraint:** Block Sparse Attention and VSA must remain enabled. Disabling either is not an accepted fix.
- **Validation:** RTX 5080 16 GB comparison showed 1,710 → 115 MiB coarse-group peak, 222.04 / 222.48 seconds, identical latents and MP4 SHA-256. 8 GB and 24 GB paths were simulated, not physically validated.
- **Status:** OPEN — root cause and multi-GPU validation required.

### Final installer after 22–24 November changes

- The 0.3.0-beta NSIS package built on 16 November predates several later fixes.
- The later emergency diagnostics and image queue work were not included in that installer.
- A subsequent Tauri release build was blocked by Windows access denial.
- **Status:** OPEN — build a fresh candidate from the reconciled working tree and smoke-test it.

## Feature-specific validation still open

### Writer / Director and scene assembly

- CPU tests cover multiple director and scene-assembly rules.
- A ten-scene test exposed location, prop, action and clothing-state inconsistencies; targeted fixes were applied and 101 CPU tests passed.
- GPU-rendered acceptance of the corrected scenes has not been completed.
- A transition to a café was present in the source screenplay and must not automatically be classified as an assembler defect.
- **Status:** PARTIALLY VALIDATED — real generated scene review required.

### Wardrobe and identity continuity

- The scene-020 wardrobe issue was traced to a short `outfit` field in `looks.json` replacing the full approved outfit description.
- ID-bound outfit propagation was fixed for the tested project copy and both Continuity Chain chunks.
- 500 T2V tests and 5 character-card tests passed; scene-020 prompt acceptance passed.
- GPU visual acceptance remains open.
- **Status:** PARTIALLY VALIDATED.

### Screen singing / vocal continuity

- Six regressions for scenes 007–009 passed.
- 499 T2V H3 tests and 59 director-module tests passed.
- CPU / FFmpeg checks only; no GPU render acceptance was performed.
- One broader Director Cut command test was blocked by `PROJECT_PATH_UNSAFE`.
- **Status:** CPU-VALIDATED — GPU acceptance and broader project-path test remain open.

### Selected image generation queue

- «Нарисовать выбранное» creates a sequential queue for selected characters, props and locations.
- Navigation and stop-after-current behavior are implemented in the UI.
- Earlier verification used a mocked engine, not real image generation.
- **Status:** UI-VALIDATED ONLY — real engine lifecycle required.

### YuE2 / StudioPolish

- Voice Map handling and quick vocal markup were improved.
- StudioPolish has analysis and EQ / Dynamics / Mastering UI work.
- Full per-tab playback, loop, A/B and real-time processing are not confirmed complete.
- Accentuation remains experimental.
- **Status:** PARTIALLY IMPLEMENTED — do not advertise unfinished controls as ready.

### Export

- Partial export of ready scenes was implemented.
- Full FFmpeg acceptance of the new path was not confirmed.
- **Status:** OPEN.

## Model and hardware limitations

### Pika H3 Flex

- Native local generation maximum: **1344 × 768 (768p, 16:9)**.
- Higher output dimensions require a separate upscale stage.
- GPU generation, lip-sync and Continuity acceptance across hardware configurations is not confirmed.
- **Status:** EXPERIMENTAL.

### Qwen Image 2.1 frame size

- HD and QHD passed the recorded resolution checks.
- In Full HD, the model returned 1920 × 1088 and the app cropped to 1920 × 1080.
- Validate saved image dimensions and visual crop in the final build.
- **Status:** KNOWN OUTPUT ADJUSTMENT — recheck final UI.

### Fast H3 Omni

- Reference-oriented route; no-reference behavior uses the H3 fallback.
- Validate routing, missing-reference warnings and the actual generation graph.
- **Status:** ROUTING IMPLEMENTED — acceptance by hardware/model combination required.

### LTX 2.5

- The recent MiniMax H3 wardrobe, screen-singing and scene-assembly fixes do not imply changes to LTX 2.5.
- Treat LTX as a separate route and test it independently.
- **Status:** NOT RE-ACCEPTED BY THE RECENT H3 FIXES.

### Dedicated P6 I2V Director Cut — acceptance still required

- P6 now has its own Screenwriter / Director Cut route and its own motion-adaptation stage. The motion stage observes the saved start frame with Vision, generates a motion description, then commits only if the source frame and accepted context have not changed.
- P6 motion is an active feature in 0.3; it must not be described as a retired command.
- A few Rust source-contract tests still contain old expectations that P6 motion is retired or unavailable. Those tests need to be aligned with the current profile-owned I2V route and rerun.
- Real GPU acceptance of the full P6 writer → frame → observed-frame motion → H3 generation chain remains open.

## Current automated validation snapshot (25 November 2026)

- Frontend production build: **passed**.
- Rust library suite: **3,426 passed, 5 failed, 67 ignored** (3,498 tests total).
- The five failures currently cover:
  1. An audio-semantics writer test still expecting the former P6 generic writer path.
  2. An I2V async-ownership test still expecting P6 motion to be retired.
  3. A profile-boundary test still expecting the old P6 motion boundary.
  4. A cleanup test using a temporary directory outside the configured project roots; it is rejected by the current project-path safety guard before reaching the legacy-command assertion.
  5. A Windows runtime test that expects the pure `managed_pid` probe to reap an exited child, while actual reaping and exit logging are performed by `reap_exited_child`.
- These appear to be stale test contracts / fixture assumptions rather than five confirmed user-facing defects, but that classification is **not final until the tests are corrected and rerun**.
- The Node audit was previously run with two UI suites blocked because the external `MSM_TEST_TOOLS` path (jsdom / esbuild) was not configured. Re-run after restoring that test harness.
- No post-24-Nov NSIS installer has yet been verified.

## Test interpretation

- Test counts from different dates, branches and suites must not be summed into a single success percentage.
- A CPU test does not prove GPU generation works.
- A mocked engine test does not prove the real ComfyUI workflow works.
- A successful build does not prove clean Windows installation.
- A passing prompt/graph assertion does not prove visual continuity in the generated video.

## Release gate

Do not mark 0.3.0 Director Cut Beta as ready for public download until:

1. The exact source tree is synchronized and reviewed.
2. The post-24-Nov installer is built.
3. Fresh install and upgrade paths are smoke-tested.
4. A small real GPU generation is completed for each engine advertised as available.
5. The SparseAttnPatch/VSA crash is either resolved or clearly disclosed with diagnostics and a safe test protocol.
6. The final SHA-256, file size, build date and commit SHA are recorded.
