# Contributing to AMBROSIA PROJECT

Thanks for helping with compatibility research. Contributions should improve reproducibility, correctness, documentation, testing, or platform support without adding proprietary content.

## Before opening a pull request

Run the relevant Rust formatter and tests, describe the hardware and operating system used, and identify the exact commit tested. Keep generated build output, runtime caches, saves, crash dumps, screenshots, and logs outside the repository.

## Content rules

Do not submit game executables, DLLs, assets, extracted or converted data, shader dumps, decompiled or disassembled code, screenshots, save files, telemetry, credentials, or other proprietary material. Use synthetic fixtures and small interoperability constants instead. Follow `docs/asset-policy.md`; it is the controlling repository rule.

Do not add code copied from another project unless its license is compatible and the required notices are preserved. XCL-informed research may be discussed in notes, but this repository does not claim a literal code merge with XCL.

## Pull requests

Explain the problem, the change, the test command, and any known limitations. Keep pull requests focused and do not claim gameplay or performance milestones that were not reproduced and documented.
