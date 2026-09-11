---
type: entity
title: BCM43224 WiFi Chipset
created: 2026-09-11
updated: 2026-09-11
tags: [wifi, broadcom, hardware, macbook-air]
sources: [[wifi-bcm43224-test-results]]
confidence: high
---

# BCM43224 (14e4:4353)

Broadcom WiFi chipset used in MacBook Air 5,2 (Mid-2012). 802.11n dual-band capable.

## Specifications

| Property | Value |
|----------|-------|
| PCI ID | 14e4:4353 |
| Standard | 802.11n |
| Bands | 2.4GHz + 5GHz |
| Max Link | 300 MBit/s (this hardware) |

## Driver Situation

- **brcmsmac** (open-source): 144.4 MBit/s link, 5.76 MB/s real — underperforms
- **broadcom-wl** (proprietary): 300 MBit/s link, 11.46 MB/s real — **2x improvement**

## Physical Verification

Tested on [[macbook-air-5-2]] hardware running Omarchy Linux. The proprietary broadcom-wl-dkms driver delivers significantly better performance than the open-source brcmsmac driver. This was verified by [[wifi-bcm43224-test-results]].

## Relationship to Omarchy

Andy Holst's PR #10910 adds BCM43224 detection to Omarchy's hardware setup, automatically blacklisting brcmsmac and installing broadcom-wl-dkms on MacBook Air 5,2 systems.

## Relationships

- Used in [[macbook-air-5-2]] laptop
- Managed by [[broadcom-wl-dkms]] proprietary driver
- Tested via [[wifi-bcm43224-test-results]]

## See Also

- [[macbook-air-5-2]] — Host laptop
- [[broadcom-wl-dkms]] — Proprietary driver
- [[wifi-driver-comparison]] — Driver performance comparison
