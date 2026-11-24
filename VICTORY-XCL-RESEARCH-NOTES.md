# XCL / Victory investigation notes

## External XCL evidence
- Upstream issue: https://github.com/xcl-dev/xcl/issues/232
- Upstream issue API: https://api.github.com/repos/xcl-dev/xcl/issues/232
- Upstream comments API: https://api.github.com/repos/xcl-dev/xcl/issues/232/comments

The issue documents the same retail title and the same null write at `game_scarlett_master.exe+0x2215c35`. A reported run on plain upstream main reached 3,599 presents and 3,599 frame boundaries without the null write. The issue comments say list slots #131/#132 were present in the same runs and that making them named no-ops changed logging, not behavior. The comments identify frame stalls / presentation timing and forced eager PSO compilation as more plausible causes than #131/#132.

The local A/B run with XCL_CONSOLE_LISTS=1, XCL_UMA_MB=2048, XCL_NETWORK=0, XCL_ACTIVITY=1 and default async/lazy behavior exited code 0. Activity telemetry showed presents and frame-event waits with zero timeouts, but also zero draws/dispatches. The compute-only console recorder logged unsupported root record `0xc000b600` (decoded parameter index 45, offset 128, one value) and repeated PC command-list Close failures `0x80004005`; this indicates the recorder is being used for graphics lists and is not a complete graphics implementation.

## Victory project
- Local path: `D:\GTA VI\CLAUDE\VIctory-main`
- README: `D:\GTA VI\CLAUDE\VIctory-main\README.md`
- Local source is a Rust workspace with crates for loader, HLE, GPU, shader translation, pipeline, and game runtime.
- README status (dated 2026-11-23): menus and intro video reportedly work at 30 fps on an AMD RX 6700 XT; world loading works; world rendering reaches indirect draws but remains dark and takes 0.5–1.8 s/frame. It explicitly says it is not playable and warns real-GPU world rendering can hang the driver; WARP diagnostics are recommended.
- Victory README says it supports Xbox native shader recompilation, tiled textures, descriptor lifetimes, indirect execution, and mesh pipelines, but many world shaders/features remain incomplete.
- Victory `Cargo.toml` declares GPL-3.0-or-later. XCL's project notes say XCL was relicensed GPL-2.0-only to incorporate AnyPS5. Therefore code cannot be blindly merged from Victory into XCL without resolving the license incompatibility; use as an architectural/reference source unless permission/relicensing is established.

## Patched XCL experiment (2026-11-25)

The XCL console-list parser was changed so a bounded root-parameter record whose index is absent from the remembered compute layout is skipped instead of aborting the rest of the list. The release build succeeded. The full library/graphics test suites passed; two fixture-dependent XCL end-to-end tests failed only because `xcl_testtitle.exe` and `testgame_mw.dll` were not built.

A bounded diagnostic using console lists, async/lazy PSO behavior, network disabled, and activity logging reached three presents/frame boundaries and three actual draws before reproducing the existing null write at `game_scarlett_master.exe+0x2215c35`. The report recorded 3,573 unique shaders, 204,723 shader submissions, 17 translated pipelines, and no translation errors. This is the first run where the decoder change coincided with nonzero draw activity; it confirms that stopping at the unsupported root record was blocking later graphics work. The run is still unstable and black, and the null-write/presentation stall remains the next blocker.

Victory then compiled successfully as `D:\GTA VI\CLAUDE\VIctory-target\release\victory.exe`, with its Cargo target kept outside the source tree. Its read-only census of the Xbox executable found 587 imported functions: 88 HLE-covered, 427 host-covered, and 72 currently missing. The missing set is concentrated in shipped game DLLs such as Bink, HTTP client, FidelityFX, and Xbox BVH builder, so a direct Victory run would need its configured game-directory/DLL policy and is not yet a safer baseline than XCL. No game launch was attempted because Victory warns that its current real-GPU world path can hang/reset the display driver.
