---
type: concept
title: Battery Charge Threshold Control
created: 2026-09-11
updated: 2026-09-11
tags: [battery, power, charge-control, applesmc, kernel]
sources: [[kernel-applesmc-charge-threshold]]
confidence: high
---

# Battery Charge Threshold Control

Limiting battery charge to preserve long-term battery health, especially important for older batteries like the [[bq20z451-battery]].

## Why Limit Charging

Lithium-polymer batteries degrade faster when kept at 100% charge. For a 12+ year old battery (~85% health, ~400 cycles), reducing the maximum charge extends usable life.

## Typical Thresholds

- **Start threshold**: 20% — battery begins charging when below this level
- **End threshold**: 80% — battery stops charging at this level

This avoids both deep discharge and full charge, keeping the battery in the 20-80% sweet spot.

## Hardware Support

Pre-2013 Macs lack upstream `charge_control_end_threshold` support. The [[applesmc-driver]] exposes this via sysfs when patched:

```bash
echo 20 | sudo tee /sys/class/power_supply/BAT0/charge_control_start_threshold
echo 80 | sudo tee /sys/class/power_supply/BAT0/charge_control_end_threshold
```

## Patch Implementation

The charge threshold patch from Andy Holst adds sysfs entries to the applesmc driver:

- `charge_control_start_threshold` — percentage to start charging
- `charge_control_end_threshold` — percentage to stop charging

These are exposed through the standard Linux power supply subsystem.

## Verification

After booting the patched [[linux-applesmc-kernel]]:

1. Check sysfs entries exist: `ls /sys/class/power_supply/BAT0/charge_control_*`
2. Set thresholds as above
3. Monitor battery: `cat /sys/class/power_supply/BAT0/capacity`
4. Verify charging stops at 80%

## Relationships

- Applies to [[bq20z451-battery]] battery
- Requires [[applesmc-driver]] patched kernel module
- Runs on [[linux-applesmc-kernel]] custom kernel
- Built via [[custom-kernel-build-arch]] process

## See Also

- [[bq20z451-battery]] — The battery entity
- [[applesmc-driver]] — Driver exposing thresholds
- [[linux-applesmc-kernel]] — Custom kernel with patch
- [[kernel-applesmc-charge-threshold]] — Build documentation
