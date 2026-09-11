---
type: entity
title: linux-applesmc (Custom Kernel)
created: 2026-09-11
updated: 2026-09-11
tags: [kernel, applesmc, charge-control, build, arch-linux, power]
sources: [[kernel-applesmc-charge-threshold]]
confidence: high
---

# linux-applesmc

Custom Arch Linux kernel with the applesmc charge threshold patch from Andy Holst's `fix/macbookair-charge-control` branch.

## Specifications

| Property | Value |
|----------|-------|
| Version | 7.2.4 |
| Source | `github.com/andyholst/linux` |
| Branch | `fix/macbookair-charge-control` |
| Base | Stock Arch kernel config |
| Key change | applesmc as module + charge threshold support |

## Why Custom

Stock Arch kernel has `CONFIG_SENSORS_APPLESMC=y` (built-in), which prevents loading a DKMS module with the charge threshold patch. Custom kernel solves this cleanly.

## Installation

Installed alongside stock kernel in [[luks-btrfs-boot]] setup:

- `linux` — 7.2.3-arch1-3 (stock, unchanged fallback)
- `linux-applesmc` — 7.2.4 (new, default boot)

## Charge Thresholds

Per [[kernel-applesmc-charge-threshold]]:

- **Start**: 20% (charge begins below this)
- **End**: 80% (charge stops at this)

## Relationships

- Runs on [[macbook-air-5-2]] hardware
- Uses [[applesmc-driver]] patched module
- Requires [[custom-kernel-build-arch]] build process
- Part of [[luks-btrfs-boot]] multi-kernel boot setup

## See Also

- [[applesmc-driver]] — The patched driver
- [[macbook-air-5-2]] — Host hardware
- [[custom-kernel-build-arch]] — Build process
- [[charge-threshold-control]] — Threshold concept
