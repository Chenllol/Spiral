# Spiral branch consolidation — 2026-11-05

## 1. Baseline and isolation

- Repository: local `Spiral` clone at `D:\Spiral`; remote `origin` points to the local Gitea repository.
- Source `main` / `origin/main`: `ac9eb9af47be58bb5867ecdb06814706584cd645`
- Original worktree: clean (`git status --porcelain=v1` empty); `main` was not modified.
- Integration worktree: separate local worktree, branch `integration/spiral-branch-consolidation-20261105`, based on `origin/main`.
- Integration branch started at `ac9eb9a`; this report is committed at the end of the integration branch.
- Backup: local all-refs Git bundle created before changes; no push, no remote write, no branch deletion, no history rewrite.
- Gitea: `mirror=false`, `has_pull_requests=false`, `has_actions=false`; no branch protection. Existing Issues remain open; no release action performed.

## 2. 27 branch decisions

`ahead/behind` are `main...origin/branch` counts. Classification follows the execution prompt: `CANDIDATE`, `INCLUDED_BY_OTHER_BRANCH`, `ALREADY_IN_MAIN_EQUIVALENT`, `HISTORICAL_KEEP`, `NEEDS_MANUAL_PORT`, `BLOCKED`.

| Branch | Tip (short) | Ahead/behind | Decision and evidence |
|---|---|---:|---|
| `test/issue-11-qt-playback-observability-phase11` | `a936c09` | +2/-0 | `CANDIDATE`; cherry-picked `a0c574c`, `a936c09` → `322c211`, `87cc24e`; Node diagnostics/media tests pass. |
| `fix/issue-53-command-feedback-phase1` | `6adb0d7` | +5/-0 | `CANDIDATE`; cherry-picked 5 commits → `43b2069`, `583b96b`, `bd732e3`, `1e2b90d`, `90bf567`; `Main.qml` conflict resolved by keeping both property blocks; extra log-order fix `40f275a`; Node tests pass. |
| `feat/issue-74-source-code-pro-ui` | `e43e4ca` | +2/-0 | `CANDIDATE`; includes #52 at `6fa9ac8`; cherry-picked `6fa9ac8`, `e43e4ca` → `b912a13`, `0159ae2`; Material/font Node tests pass. |
| `fix/issue-11-annotated-acoustic-transitions-phase10` | `ce50183` | +3/-0 | `CANDIDATE`; cherry-picked 3 commits → `30b1404`, `55607a9`, `1fcfa3d`; added output overwrite guard `428e7af`; 22 Python tests pass. |
| `docs/p2p-connectivity-research-20261028` | `e418b35` | +3/-0 | `CANDIDATE`; cherry-picked 3 docs commits → `9d59248`, `0a0423e`, `7423726`; docs conflict kept both #74 and P2P sections. |
| `fix/issue-52-material-dark-contrast` | `6fa9ac8` | +1/-0 | `INCLUDED_BY_OTHER_BRANCH`; exact commit is contained in #74 and was applied once in `b912a13`. |
| `test/issue-11-52-74-windows-acceptance` | `b705d47` | +3/-0 | `INCLUDED_BY_OTHER_BRANCH`; `a936c09` and `a0c574c` are in Phase11; remaining tree is #74 content (and no #53). Not re-applied separately. |
| `release/v0.1.0-preview.1-windows` | `430e517` | +8/-1 | `HISTORICAL_KEEP`; tree identical to `main`; no content merge. |
| `feat/issue-11-arming-barrier` | `68d8d7c` | +5/-10 | `ALREADY_IN_MAIN_EQUIVALENT`; `Store.AcknowledgeArming` / `arming_test.go`; no branch-only files. |
| `feat/issue-11-host-recovery-phase9` | `c994f14` | +18/-2 | `ALREADY_IN_MAIN_EQUIVALENT`; `RemoveGuest` / `host_recovery_test.go` already in main; branch is behind release files. |
| `fix/issue-11-authority-recovery-fence-phase8` | `ed64762` | +5/-3 | `ALREADY_IN_MAIN_EQUIVALENT`; `acceptWakeSnapshot` / `sleep_resync.test.cjs`; no added files. |
| `fix/issue-11-cancellation-barrier` | `e708699` | +14/-6 | `ALREADY_IN_MAIN_EQUIVALENT`; `pendingCancellationLocked` / `cancellation_barrier_test.go`. |
| `fix/issue-11-cancellation-receipts` | `ed86022` | +14/-7 | `ALREADY_IN_MAIN_EQUIVALENT`; `AcknowledgeCancellation` / `cancellation_receipt.test.cjs`. |
| `fix/issue-11-media-buffer-and-acoustic-harness` | `5b4ab23` | +20/-4 | `ALREADY_IN_MAIN_EQUIVALENT` for base behavior; `mediaLoaded` / `media_buffer_safety.test.cjs`; Phase11 adds the remaining `BufferingMedia` case. |
| `fix/issue-11-member-loss-pending-fence` | `1858a19` | +7/-8 | `ALREADY_IN_MAIN_EQUIVALENT`; `suspendPlaybackLocked` / `flow_test.go`. |
| `fix/issue-11-partition-failclosed-phase2` | `c65261c` | +3/-9 | `ALREADY_IN_MAIN_EQUIVALENT`; `safeguardAuthority` / `authority_partition.test.cjs`. |
| `fix/issue-11-suspend-clock-and-snapshot-resync` | `883b98d` | +34/-5 | `ALREADY_IN_MAIN_EQUIVALENT`; `clockcontinuity.h`, snapshot resync / `sleep_resync.test.cjs` and Go resync tests. |
| `fix/anonymous-room-admission-issue-10` | `3d0634e` | +4/-16 | `ALREADY_IN_MAIN_EQUIVALENT`; `CreateForSource` / `admission_test.go`. |
| `fix/client-transport-policy-issue-14` | `99de8a8` | +2/-17 | `ALREADY_IN_MAIN_EQUIVALENT`; `transportpolicy.h` / `transport_gate.test.cjs`. |
| `fix/clock-offset-pending-rearm-issue-3` | `5283f9f` | +2/-18 | `ALREADY_IN_MAIN_EQUIVALENT`; `receiveClock` rearm / `clock_scheduling.test.cjs`. |
| `fix/clock-offset-pending-schedule-issue-3` | `55581a5` | +1/-18 | `ALREADY_IN_MAIN_EQUIVALENT`; same QML clock path; no added files. |
| `fix/host-control-idempotency-issue-19` | `f64d3c8` | +7/-14 | `ALREADY_IN_MAIN_EQUIVALENT`; `ControlTrack`/`ControlSchedule` / `control_test.go`. |
| `fix/live-session-expiration-issue-29` | `6b263f4` | +3/-12 | `ALREADY_IN_MAIN_EQUIVALENT`; `expiryLoop` / `expiry_integration_test.go`. |
| `fix/pending-timer-recovery-issue-28` | `434765f` | +1/-13 | `ALREADY_IN_MAIN_EQUIVALENT`; `executePending` / `pending_recovery.test.cjs`. |
| `fix/reconnect-session-fencing-issue-2` | `4bf1e5c` | +3/-19 | `ALREADY_IN_MAIN_EQUIVALENT`; `Hub.isCurrent` / `fencing_test.go`. |
| `fix/websocket-control-heartbeat-issue-30` | `d16b99c` | +2/-11 | `ALREADY_IN_MAIN_EQUIVALENT`; `readTextWithControl` / `websocket_test.go`. |
| `fix/ws-required-fields-issue-6` | `723d355` | +2/-15 | `ALREADY_IN_MAIN_EQUIVALENT`; `strictEnvelope` / `envelope_test.go`. |

Equivalence method for the 19 historical branches: I compared the branch diff from its merge-base, confirmed that none has a branch-only added file, and traced the named control path to the current main implementation and its test. This is functional-equivalence evidence, not a formal line-by-line bisimulation; no branch was marked `REVIEW_REQUIRED` because each high-risk invariant has a current implementation and a passing regression. Residual line-level differences remain covered by the full Go and Node suites.

## 3. Gates and actual changes

| Gate | Source | Files / operation | Integration commit(s) |
|---|---|---|---|
| 1 | Phase11 `a0c574c`, `a936c09` | `Main.qml`, `synctools.cpp`, media/logging tests/docs; cherry-pick, no conflict | `322c211`, `87cc24e` |
| 2 | #53 `b15d63f`…`6adb0d7` | `Main.qml`, command/removal tests; cherry-pick; one property-block conflict resolved keeping both; command success logs moved to ACK; track-success log assertion added | `43b2069`, `583b96b`, `bd732e3`, `1e2b90d`, `90bf567`, `40f275a`, `c8672db` |
| 3 | #74 `6fa9ac8`, `e43e4ca` | Material dark, font assets, CMake/QML/C++ font loading, OFL; cherry-pick, auto-merged | `b912a13`, `0159ae2` |
| 4 | Phase10 `3626f8d`, `0dad14b`, `ce50183` | `tools/audio_transitions.py`, tests/docs; cherry-pick; output overwrite guard added | `30b1404`, `55607a9`, `1fcfa3d`, `428e7af`, `5c99f8f` |
| 5 | P2P `f8667f5`, `cce2e06`, `e418b35` | Research docs/roadmap/status; docs conflict resolved keeping both sections; second-round log semantics documented | `9d59248`, `0a0423e`, `7423726`, `f0728e9` |
| 6 | 20 historical branches | No branch-only added files; main functions/tests provide equivalent behavior; no merge | none |
| 7 | b705d47 QA branch | Parent is `a936c09`; `a936..b705` adds the #74 file set, while `#74..b705` contains only the Phase11 files. It has no #53 and no independent functional diff; not re-applied. | none |

## 4. Test matrix

| ID / suite | Status | Evidence |
|---|---|---|
| Go `go vet ./...` | PASS | `server`, integration HEAD |
| Go `go test ./...` | PASS | `server`, 5 packages |
| Go `go test -race ./...` | PASS | `server`, 5 packages |
| CMake `server-only` configure/build/CTest | PASS | 1/1 test |
| Node/QML source-derived tests | PASS | 16/16 files, including playback diagnostics, command feedback, material/font tests |
| Python acoustic tests | PASS | 22 tests, including transitions and output-overwrite guard |
| C++ tests (`clock_continuity`, `transport_policy`) | PASS | Qt 6.8.3 + MSVC 19.51; CTest 2/2 |
| Qt desktop build | PASS | `build/dev-msvc-4`; MSVC x64 + Qt 6.8.3 |
| Qt headless startup | PASS (startup only) | offscreen process alive for 8 s, no stderr/QML load errors |
| QML lint | PASS (warnings only) | `qmllint` exit 0; 26 warnings, mostly context-property unqualified access and QtWebSockets metadata |
| Qt interactive GUI / visual theme / DPI | UNVERIFIED | no interactive display/screenshot acceptance |
| Windows preview package | BLOCKED/NOT_RUN | no clean-machine packaged Windows validation; Gitea Actions disabled |
| Real two-device audio / P50/P95/max | UNVERIFIED | no physical devices or recording |
| P2P implementation | NOT_APPLICABLE | documentation/research only |

Qt environment used for the successful build:

- SDK: Qt 6.8.3 `win64_msvc2022_64` at a local Qt installation.
- Compiler: MSVC 19.51 (Visual Studio 18 toolchain); `cl`, `rc`, and `mt` supplied explicitly.
- Build: `build/dev-msvc-4` with `CMAKE_PREFIX_PATH` set to Qt and `SPIRAL_BUILD_SERVER=OFF`.
- The earlier MinGW attempt failed with `undefined reference` against MSVC Qt libraries; it was an ABI/toolchain mismatch, not a source-code compile failure.

## 5. Security and regression review

- Server Go code was not modified by this integration; `git diff origin/main..HEAD -- server` is empty.
- ARM/ACK/COMMIT, cancellation receipts, host removal, reconnect fencing, expiry, heartbeat and strict envelope tests remain in the Go suite and pass.
- QML changes were limited to UI feedback, playback diagnostics, Material/font styling and the existing playback/state machine. Source-derived Node tests pass; the Qt 6.8.3 client also loads and starts headlessly without QML load errors, but interactive GUI, visual contrast/font rendering and DPI behavior remain unverified.
- `Main.qml` property/function duplicate scan found no duplicate declarations; no conflict markers remain. `qmllint` exits 0 with warnings limited largely to unqualified context-property access and QtWebSockets type metadata.
- Host command success logging now occurs only after `command_ack` with `applied=true`, not at click time; `client.playback_executed` is documented as a local timer branch, not proof of audible output.
- The acoustic transition tool now refuses to use its input WAV or annotation manifest as the output path; the regression test verifies the source file remains present.
- The second-round Qt build used the MSVC ABI; the initial MinGW attempt was rejected as an ABI/toolchain mismatch, not misreported as a source failure.
- No tokens, invitation codes, local user paths or media content were added to source or report.

## 6. Rollback

- Original `main` remains at `ac9eb9af47be58bb5867ecdb06814706584cd645`.
- Integration branch is isolated; discard by deleting the worktree/branch (after review), or reset to `ac9eb9a`.
- No remote operations were performed.
- Old branches and tags were retained.
