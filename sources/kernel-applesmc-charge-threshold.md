---
type: source
title: "Custom Kernel Build: linux-applesmc with Charge Threshold Patch"
authors: ["Physical hardware test"]
url: "https://github.com/andyholst/linux/tree/fix/macbookair-charge-control"
raw: "raw/articles/kernel-applesmc-charge-threshold.md"
ingested: 2026-09-11
tags: [kernel, applesmc, charge-control, build, arch-linux, power]
entities: [applesmc-driver, macbook-air-5-2, linux-applesmc-kernel]
concepts: [custom-kernel-build-arch, charge-threshold-control]
---

# Custom Kernel Build: linux-applesmc with Charge Threshold Patch

Built a custom Arch Linux kernel (7.2.4) with the applesmc charge control patch from Andy Holst's `fix/macbookair-charge-control` branch. The patch exposes `charge_control_end_threshold` and `charge_control_start_threshold` sysfs entries for pre-2013 Macs.

## Why Custom Kernel

Stock Arch kernel has `CONFIG_SENSORS_APPLESMC=y` (applesmc built-in), preventing DKMS module loading. Custom kernel required to build applesmc as module or apply patch directly.

## Build & Installation

- **Source**: `github.com/andyholst/linux` branch `fix/macbookair-charge-control`
- **Version**: 7.2.4 (matching stock Arch kernel)
- **Method**: Arch way — `makepkg` with custom PKGBUILD
- **Result**: Two kernels in Limine boot menu:
  - `linux` — 7.2.3-arch1-3 (stock, unchanged fallback)
  - `linux-applesmc` — 7.2.4 (new, with charge threshold support) ← default

## Charge Threshold Settings

- **Start threshold**: 20% (battery begins charging when below 20%)
- **End threshold**: 80% (battery stops charging at 80%)

## Verification Steps

1. Reboot → new kernel boots by default
2. Check: `ls /sys/class/power_supply/BAT0/charge_control_end_threshold`
3. Set thresholds: `echo 20 > .../charge_control_start_threshold; echo 80 > .../charge_control_end_threshold`
4. Verify charging stops at 80%

## Where this fits

- [[applesmc-driver]] — Driver being patched
- [[macbook-air-5-2]] — Hardware using this kernel
- [[linux-applesmc-kernel]] — Custom kernel entity
- [[custom-kernel-build-arch]] — Build process concept
- [[charge-threshold-control]] — Battery charge control concept
- [[kernel-module-install]] — Module installation procedure
- [[luks-btrfs-boot]] — Boot setup with multiple kernels
