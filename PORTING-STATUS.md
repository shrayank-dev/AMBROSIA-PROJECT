# GTA VI Victory Porting Research

This repository records compatibility research and source changes for running the user-owned Xbox Series build through Victory on Windows. It is a research snapshot, not a redistribution of the game.

## Current milestone

Victory reliably reaches the calibration/menu path at approximately 30 FPS on the real GPU. The isolated packed-format experiment maps Xbox formats 86 and 115 to host format 28 for PC resources/views while preserving Xbox layout accounting. This removes the observed host-texture creation failures and lets the world path survive substantially longer, but visible playable world rendering is not yet confirmed.

The latest stable-menu run also reached repeated Jason/Lucia loading screens without missing imports. The next controlled milestone is input, settings, profile, and save persistence testing against cloned runtime data, followed by a reproducible world-entry sequence.

## Repository safety

This repository intentionally excludes the Xbox game directory, game executable and DLLs, runtime cache/data, saves, profiles, crash dumps, generated binaries, captures, and local logs. Those remain on the user's computer and are never part of this repository.

## Licensing

Victory source retains its upstream GPL-3.0-or-later license. See `LICENSE` and the upstream project documentation before redistributing or combining code with other projects.
