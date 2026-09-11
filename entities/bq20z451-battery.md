---
title: bq20z451 Battery Gas Gauge
created: 2026-09-10
updated: 2026-09-11
type: entity
tags: [battery, hardware, applesmc, power]
sources: [[kernel-applesmc-charge-threshold]]
confidence: high
---

# bq20z451

Texas Instruments battery gas gauge, used in MacBook Air 5,2 (mid-2012).

## Specifications

| Property | Value |
|----------|-------|
| Manufacturer | Texas Instruments |
| Chemistry | Li-Polymer |
| Design Capacity | 7200 mAh |
| Current Health | ~85% (6086/7200 mAh) |
| Cycle Count | ~399 cycles |
| Voltage | 7.6V nominal |

## Status

- Monitored via [[applesmc-driver]] in kernel
- Charge control patches allow setting `charge_control_end_threshold` to limit charging at 80-85%
- Health declining slowly — typical for 12+ year old battery
- Charge thresholds set via [[charge-threshold-control]]: start at 20%, stop at 80%

## Relationships

- Installed in [[macbook-air-5-2]] laptop
- Managed by [[applesmc-driver]] kernel module
- Requires [[kernel-module-install]] for patched driver builds
- Controlled via [[charge-threshold-control]] for battery preservation
- Powered by [[linux-applesmc-kernel]] custom kernel

## See Also

- [[macbook-air-5-2]] — Host laptop
- [[applesmc-driver]] — Driver that exposes battery info
- [[kernel-module-install]] — Custom module build procedure
