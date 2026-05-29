# Armbian Build for Allwinner A20 Hummingbird

This repository contains Armbian build customisations for the Allwinner A20 Hummingbird board.

The GitHub Actions workflow builds Armbian images using the upstream `armbian/build` framework with the `bananapi` board target and local `userpatches`.

## GMAC / Gigabit Ethernet Issue

If wired Ethernet does not come up after boot, bounce the interface once.
Some images may name the interface `eth0`; others may name it `end0`.

```bash
iface=eth0
ip link show "$iface" >/dev/null 2>&1 || iface=end0

ip link set "$iface" down
sleep 5
ip link set "$iface" up
```

To use the legacy `eth0` name instead of predictable names such as `end0`, edit `/boot/armbianEnv.txt` and add:

```text
extraargs=net.ifnames=0
```

Do not quote the value.

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
