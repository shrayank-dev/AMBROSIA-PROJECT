# AMBROSIA PROJECT — Current Progress

**Date:** 2026-11-26

## Pre-flight

The restored menu launcher and stable Victory executable were verified against the protected pre-world-fix savepoint. The launcher SHA-256 is `3C89FDD07A94D49B347FD5ED7DA9654765A6434E06627F4707E05C47F581448B`; the stable Victory executable SHA-256 is `8F9D616648020E0FF68E520EF09B421100FB65B2A4EDFADA6D9CE1671D77DEB0`. The Xbox source folder was not modified.

## Launcher check

The launcher was started on 2026-11-26 and produced a real `Americas | VIctory` window. Its title reported approximately 30 FPS and 33.3 ms/frame during the check. A 20-second H.264 capture was technically encoded at 30 FPS, but visual inspection found that the captured pixels were a white/black rendering artifact rather than a readable menu. It is therefore rejected as public proof and must not be uploaded or described as a valid menu capture.

Rejected artifacts:

- `captures/proof/ambrosia-launcher-proof-20261126.mp4`
- `captures/proof/ambrosia-launcher-proof-20261126.jpg`

The rejected MP4 is retained locally for debugging only.

## PortWatch check

The accessible PortWatch VI page currently reports an XCL update claiming 30 FPS and tester reports of world loading, but it does not expose a clear public submission form or verified upload endpoint. An independent PC Games Hardware report dated 2026-11-24 describes PortWatch's standings as VIctory 67% and XCL 62.5%, while emphasizing that neither is a finished playable PC port. The same report describes VIctory's menu boot and early world/title-card milestone, but notes that world frames remain very slow and dark.

Ambrosia should be described conservatively as a user-owned compatibility-layer research effort with a reproducible menu-window launch under Victory, not as a playable PC port. No public update should claim that today's recording proves a stable rendered menu because it does not.

## Next evidence gate

Before any GitHub, Discord, or PortWatch upload, capture must show readable Victory content in the actual game window. Desktop screenshots, white/black capture artifacts, and stale earlier captures are not acceptable substitutes.

## References

- PortWatch VI: https://portwatch-vi.xyz/
- PC Games Hardware report: https://www.pcgameshardware.de/GTA-6-Spiel-55239/News/GTA-6-PC-ports-Leonida-offline-VIctory-leads-XCL-1560947/
