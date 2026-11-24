# World-fix format-mapping experiment

Date: 2026-11-25

## Scope

This experiment is isolated under `CLAUDE/experiments/world-fix-format-flags`. The protected Xbox input folder and the verified menu launcher/build were not modified.

## Fix applied

In `crates/victory-gpu/src/resource.rs`, the host-side format mapper now converts Xbox packed formats 86 (`B5G5R5A1_UNORM`) and 115 (`B4G4R4A4_UNORM`) to PC host format 28 (`R8G8B8A8_UNORM`) for host resources and views. Console allocation/layout accounting remains based on the original Xbox formats.

The earlier experimental flag workaround was removed after checking the Windows SDK enum definitions; formats 86 and 115 are packed color formats, not depth formats.

## Validation

- Diagnostics build completed successfully.
- Fresh WARP run: zero `no host texture` warnings; the run remained alive through the bounded test and reached 21 draws/frame at approximately 12-15 FPS, which is expected for WARP.
- Real-GPU 30-second run: zero host-texture warnings; reached the 21-draw path without a new crash.
- Real-GPU 60-second run: zero host-texture warnings; survived beyond the old immediate world-crash point, with 21 draws/frame and approximately 1.8-10 FPS while streaming.
- Real-GPU 120-second run: zero host-texture warnings; survived the full bound, reached 21 draws/frame, briefly reached 25 FPS, and did not create a new crash report.
- Intermediate target dump: target resources are successfully being captured, but the presented frame and world render-target captures remain black. A captured target shows the account-picker overlay, confirming the current cloned runtime is still at the menu/account-picker layer rather than verified playable gameplay.

## Current conclusion

The packed-format resource-creation blocker is fixed in the experiment. The remaining blocker is visible output: world render-target writes, shader output, or final plane/resource selection. Do not replace the known-good menu executable with this experiment yet.

## Key artifacts

- Experimental source: `CLAUDE/experiments/world-fix-format-flags/VIctory-main`
- Diagnostics executable: `CLAUDE/experiments/world-fix-format-flags/VIctory-main/target/diag/victory.exe`
- WARP log: `CLAUDE/logs/world-fix-format-flags-diag2-warp.err.log`
- Real-GPU 120-second log: `CLAUDE/logs/world-fix-format-flags-real3.err.log`
- Intermediate target log: `CLAUDE/logs/world-fix-targets.err.log`
- Intermediate captures: `CLAUDE/captures/world-fix-targets`
- Protected baseline/menu launcher remains under `CLAUDE/builds/Victory-pristine-target` and `CLAUDE/launchers/GTA6-Victory-Menu-Demo`.
