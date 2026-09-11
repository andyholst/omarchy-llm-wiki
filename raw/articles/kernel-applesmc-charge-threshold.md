---
source_url: https://github.com/andyholst/linux/tree/fix/macbookair-charge-control
ingested: 2026-09-11
sha256: b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7f8a9b0c1d2e3f4a5b6c7d8e9f0a1b2c3
---

# Custom Kernel Build: linux-applesmc with Charge Threshold Patch

## Overview

Built a custom Arch Linux kernel (7.2.4) with the applesmc charge control patch from Andy Holst's `fix/macbookair-charge-control` branch. The patch exposes `charge_control_end_threshold` and `charge_control_start_threshold` sysfs entries for pre-2013 Macs.

## Why Custom Kernel

The stock Arch kernel has `CONFIG_SENSORS_APPLESMC=y`, which means the applesmc driver is built-in. This prevents loading a DKMS module with the charge threshold patch. A custom kernel build is required to either:
- Build applesmc as a module (`CONFIG_SENSORS_APPLESMC=m`)
- Or apply the patch directly to the kernel source

## Build Process

1. **Source**: `github.com/andyholst/linux` branch `fix/macbookair-charge-control`
2. **Version**: 7.2.4 (matching stock Arch kernel)
3. **Method**: Arch way — `makepkg` with custom PKGBUILD
4. **Config**: Based on stock Arch kernel config with applesmc as module

## Installation

The custom kernel was installed alongside the stock kernel:
- **`linux`** — 7.2.3-arch1-3 (stock, unchanged fallback)
- **`linux-applesmc`** — 7.2.4 (new, with charge threshold support) ← default

Both kernels use the same cmdline, same btrfs on LUKS setup. Old kernel is completely untouched.

## Verification Steps

1. Reboot → new kernel boots by default
2. Check: `ls /sys/class/power_supply/BAT0/charge_control_end_threshold`
3. Set thresholds: `echo 20 > .../charge_control_start_threshold; echo 80 > .../charge_control_end_threshold`
4. Verify charging stops at 80%

## Charge Threshold Settings

- **Start threshold**: 20% (battery begins charging when below 20%)
- **End threshold**: 80% (battery stops charging at 80%)

This preserves battery health by avoiding full charge cycles.

## Patch Status

- **Repository**: `github.com/andyholst/linux`
- **Branch**: `fix/macbookair-charge-control`
- **Upstream**: Not yet submitted to mainline kernel
- **Status**: Working on MacBook Air 5,2 hardware

## Key Insight

The stock Arch kernel's built-in applesmc driver (`CONFIG_SENSORS_APPLESMC=y`) is the blocker. A custom kernel is the cleanest solution because it allows building applesmc as a module or applying the patch directly, while preserving the stock kernel as a fallback.
