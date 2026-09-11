---
type: entity
title: broadcom-wl-dkms (Proprietary Driver)
created: 2026-09-11
updated: 2026-09-11
tags: [wifi, broadcom, driver, dkms, kernel]
sources: [[wifi-bcm43224-test-results]]
confidence: high
---

# broadcom-wl-dkms

Proprietary Broadcom WiFi driver packaged for Arch Linux with DKMS for automatic rebuilds on kernel updates.

## Purpose

Provides better performance than the open-source brcmsmac driver for Broadcom WiFi chipsets like the [[bcm43224-wifi]] in [[macbook-air-5-2]].

## Performance

Per [[wifi-bcm43224-test-results]] on MacBook Air 5,2:

| Metric | brcmsmac | broadcom-wl |
|--------|----------|-------------|
| Link speed | 144.4 MBit/s | 300 MBit/s |
| Real download | 5.76 MB/s | 11.46 MB/s |
| Improvement | — | **2.0x** |

## Installation

Available in AUR as `broadcom-wl-dkms`. DKMS ensures the module is rebuilt when the kernel updates.

Requires blacklisting the open-source `brcmsmac` driver:

```
blacklist brcmsmac
blacklist bcma
```

## Caveats

- Proprietary — source code not available
- Requires firmware
- Must be rebuilt for each kernel version (DKMS handles this)
- May conflict with brcmsmac if both are loaded

## Relationships

- Replaces [[bcm43224-wifi]]'s default driver
- Installed on [[macbook-air-5-2]] per PR #10910
- Performance verified by [[wifi-bcm43224-test-results]]

## See Also

- [[bcm43224-wifi]] — The WiFi chipset
- [[macbook-air-5-2]] — Hardware using this driver
- [[wifi-driver-comparison]] — Performance comparison analysis
