# Armbian Build for Allwinner A20 Hummingbird

This repository contains Armbian build customisations for the Allwinner A20 Hummingbird board.

The GitHub Actions workflow builds Armbian images using the upstream `armbian/build` framework with the `bananapi` board target and local `userpatches`.

## Build Targets

The workflow builds these rootfs variants:

- Ubuntu 24.04 Noble
- Ubuntu 26.04 Resolute
- Debian 13 Trixie

## Artifacts

Each workflow run uploads separate artifacts for:

- U-Boot packages and extracted U-Boot binary files
- Kernel packages and extracted `uImage` or `zImage` files
- Full compressed Armbian image and logs

Artifacts are named with the `armbian-hummingbird-*` prefix. The workflow also publishes the build artifacts to a GitHub Release after all rootfs builds finish.

Full images are compressed with `COMPRESS_OUTPUTIMAGE=xz`, so the image file is expected to use the `.img.xz` format.
