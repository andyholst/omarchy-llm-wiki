---
title: MacBook Air 5,2
created: 2026-09-10
updated: 2026-09-11
type: entity
tags: [macbook-air, hardware, intel, wifi, broadcom]
sources: [[wifi-bcm43224-test-results]]
confidence: high
---

# MacBook Air 5,2 (Mid-2012)

Intel Core i5-3427U (dual-core, 1.8GHz), Intel HD 4000, 8GB RAM. The last MacBook Air with a full SATA SSD and user-accessible internals before Apple moved to proprietary form factors.

## Hardware Specs

| Component | Details |
|-----------|---------|
| CPU | Intel i5-3427U (Ivy Bridge, dual-core, HT) |
| GPU | Intel HD 4000 |
| WiFi | Broadcom BCM43224 (14e4:4353) |
| Battery | bq20z451 (7200 mAh design, ~85% health) |
| Display | 1440x900 13.3" |
| Storage | SSD (replaceable, 2.5" SATA) |

## Software Status

- Running Omarchy Linux (Arch-based) with Hyprland
- LUKS full disk encryption + Btrfs ([[luks-btrfs-boot]])
- Custom kernel `linux-applesmc` 7.2.4 with [[applesmc-driver]] charge control patches (stock 7.2.3 preserved as fallback)
- TLP + auto-cpufreq + powertop for battery optimization
- WiFi: [[broadcom-wl-dkms]] driver (2x improvement over brcmsmac, verified by [[wifi-bcm43224-test-results]])

## Hardware Notes

- The BCM43224 WiFi requires proprietary broadcom-wl driver (no open-source replacement)
- The SMC exposes battery charge thresholds via `BCLM`/`BFCL` keys — not in upstream kernel
- Intel HD 4000 supports VA-API but not QuickSync; power management requires `i915.enable_dc=0` on this platform
- 8GB RAM is soldered — not upgradeable
- WiFi driver comparison: [[wifi-driver-comparison]] (brcmsmac vs broadcom-wl)

## Relationships

- Hosts [[bq20z451-battery]] battery gas gauge
- Managed by [[applesmc-driver]] for hardware control
- Boots via [[luks-btrfs-boot]] encrypted setup
- Uses [[kernel-module-install]] for custom module builds
- Contains [[bcm43224-wifi]] WiFi chipset
- Uses [[broadcom-wl-dkms]] proprietary WiFi driver
- Runs [[linux-applesmc-kernel]] custom kernel
- Verified by [[wifi-bcm43224-test-results]]

## See Also

- [[bq20z451-battery]] — Battery gas gauge
- [[applesmc-driver]] — System Management Control driver
- [[luks-btrfs-boot]] — Boot encryption setup
- [[kernel-module-install]] — Custom module build procedure
