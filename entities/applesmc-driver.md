---
title: applesmc Driver
created: 2026-09-10
updated: 2026-09-11
type: entity
tags: [applesmc, kernel, driver, module, power]
sources: [[kernel-applesmc-charge-threshold]]
confidence: high
---

# applesmc (Apple System Management Control)

Kernel driver for Apple's SMC chip, controlling fans, LEDs, battery info, and sensors.

## Purpose

The `applesmc` kernel module provides access to Apple hardware management:

- Fan speed control (PWM)
- Temperature sensors
- Battery charge info (via [[bq20z451-battery]])
- Keyboard backlight, ambient light sensor
- Charge control thresholds (with patches)

## Patching for Charge Control

Pre-2013 Macs lack upstream `charge_control_end_threshold` support. The [[macbook-air-5-2]] uses a patched version of `applesmc` to expose:

- `charge_control_end_threshold` — limits max charge (e.g., 80%)
- `charge_control_start_threshold` — controls start threshold

**Patch status**: Committed to `github.com/andyholst/linux` branch `fix/macbookair-charge-control`. Not yet submitted upstream.

**Build method**: Custom [[linux-applesmc-kernel]] kernel (7.2.4) built via [[custom-kernel-build-arch]] — stock Arch kernel has `CONFIG_SENSORS_APPLESMC=y` which prevents DKMS module loading.

## Module Loading

```bash
sudo modprobe applesmc
ls /sys/class/power_supply/BAT0/charge_control_end_threshold
echo 80 | sudo tee /sys/class/power_supply/BAT0/charge_control_end_threshold
```

## Dependencies

- Requires `applesmc.ko` built against matching kernel version (vermagic must match)
- Modules must be in `/lib/modules/<version>/kernel/drivers/hwmon/`
- `depmod -a` must be run after module changes
- Auto-loads via `/etc/modules-load.d/applesmc.conf`

## Relationships

- Manages [[bq20z451-battery]] battery gas gauge
- Runs on [[macbook-air-5-2]] hardware
- Requires [[kernel-module-install]] for proper installation
- Part of [[luks-btrfs-boot]] boot chain when included in initramfs
- Built via [[custom-kernel-build-arch]] for charge threshold support
- Runs on [[linux-applesmc-kernel]] custom kernel
- Enables [[charge-threshold-control]] for battery preservation

## See Also

- [[macbook-air-5-2]] — Hardware using this driver
- [[bq20z451-battery]] — Battery managed via this driver
- [[kernel-module-install]] — Proper module installation procedure
- [[luks-btrfs-boot]] — Boot setup requiring correct module install
