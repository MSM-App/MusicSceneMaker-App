# Build manifest — MusicSceneMaker 0.3.0 Director Cut Beta

**Candidate build created 25 November 2026.** This manifest describes the exact Windows x64 files in the local test package. It is not a claim that live GUI/GPU acceptance has passed.

| Field | Final value |
| --- | --- |
| Product version | 0.3.0-beta |
| Release tag | pending; no public release created |
| Source repository | MSM-App/MusicSceneMaker-Source (private) |
| Source branch | release/0.3.0-beta |
| Source commit SHA | 12eda0fecc3ef2988890f08166e442218b7280fc |
| Source PR | https://github.com/MSM-App/MusicSceneMaker-Source/pull/3 |
| Build date/time | 2026-11-25 18:04:13 (UTC+03:00) |
| Windows build host | DESKTOP-DOC6977 |
| Windows version | Windows 11 Pro, build 26200, x64 |
| Architecture | x64 |
| Application EXE filename | MusicSceneMaker.exe |
| Application EXE size (bytes) | 63636992 |
| Application EXE SHA-256 | 19E1798CD3F5CA0AD84016375CCED89778C05BABE043C341287265B64DC10266 |
| NSIS installer filename | MusicSceneMaker Director Cut_0.3.0-beta_x64-setup.exe |
| NSIS installer size (bytes) | 124089618 |
| NSIS installer SHA-256 | B4F1F8409D98A305FA2069F65B2F2492133D0C1B475D98CE5261726AADDA2E51 |
| Local tester bundle ZIP | MSM_0.3.0_Director_Cut_Beta_Test.zip — 124,147,241 bytes — SHA-256 9D42ED9B31C8B6D911D2D90246ABD756613B8CB0A5D979C796C3694B2289E713 (local transfer package, not a public GitHub asset) |
| NSIS archive integrity | 7-Zip 24.09 test passed; 66 files; 188063901 uncompressed bytes |
| Code signature | NotSigned — unsigned beta installer |
| MSI | Not built. MSI bundler rejects the non-numeric prerelease identifier “beta”; NSIS x64 was built intentionally. |
| TypeScript result | PASS |
| Frontend production build | PASS |
| Rust test result | 3432 passed, 0 failed, 67 ignored |
| Previously failing Rust targets | 5/5 PASS individually |
| Related Rust regressions | 365 passed, 0 failed |
| Node / React CPU audit | 21/21 PASS (external jsdom/esbuild test tools configured) |
| GPU smoke test | NOT RUN — external beta acceptance required |
| Clean Windows install | NOT RUN — package integrity checked, installation not performed |

## Notes

- Local test package folder: `C:\Users\1\Desktop\MSM_0.3.0_Director_Cut_Beta_Test`.
- The NSIS installer is unsigned. Verify the SHA-256 before sharing; Windows may display an unknown-publisher warning.
- The executable extracted from the NSIS package has SHA-256 19E1798CD3F5CA0AD84016375CCED89778C05BABE043C341287265B64DC10266. Tauri changes the three-byte bundle-type marker when preparing NSIS; the pre-bundle target/release executable has a different hash and must not be substituted for the packaged executable.
- Full 7-Zip extraction produced all 66 files. The packaged yue-server.exe is 1,546,240 bytes and matches the source resource SHA-256.
- The release build completed with 371 non-fatal Rust warnings and no compile errors.
- The initial all-target bundle attempt failed only at the MSI metadata rule; the NSIS-only build completed successfully.
- The known SparseAttnPatch.reset()/VSA crash root cause remains open. Block Sparse Attention and VSA remain enabled.
- This manifest must be updated if the installer is rebuilt or the source commit changes.
