---
type: concept
title: WiFi Driver Comparison (brcmsmac vs broadcom-wl)
created: 2026-09-11
updated: 2026-09-11
tags: [wifi, broadcom, driver, kernel, performance]
sources: [[wifi-bcm43224-test-results]]
confidence: high
---

# WiFi Driver Comparison: brcmsmac vs broadcom-wl

Performance comparison between open-source and proprietary drivers for Broadcom WiFi chipsets.

## The Two Drivers

| Driver | Type | License | Source |
|--------|------|---------|--------|
| brcmsmac | Kernel module | Open-source (GPL) | Linux kernel tree |
| broadcom-wl | DKMS module | Proprietary | Broadcom via AUR |

## Performance on BCM43224

From [[wifi-bcm43224-test-results]] (MacBook Air 5,2):

| Metric | brcmsmac | broadcom-wl | Delta |
|--------|----------|-------------|-------|
| Link speed | 144.4 MBit/s | 300 MBit/s | +2.1x |
| Real download | 5.76 MB/s | 11.46 MB/s | +2.0x |
| Signal | -35 dBm | -42 dBm | similar |
| Ping | 5.1 ms | ~5 ms | same |

## Analysis

The proprietary broadcom-wl driver delivers **2x real-world speed improvement** over brcmsmac for the BCM43224 chipset. Signal quality and latency are essentially identical — the difference is pure throughput.

This is a known limitation: Broadcom's proprietary driver better utilizes the hardware's 802.11n capabilities, likely due to firmware-level optimizations not available in the open-source implementation.

## Trade-offs

- **brcmsmac**: Free, open-source, no firmware required — but lower performance
- **broadcom-wl**: 2x faster — but proprietary, requires firmware, must be rebuilt per kernel

## When to Choose Which

- Choose broadcom-wl when performance matters and you're comfortable with proprietary firmware
- Choose brcmsmac when you require fully free software and can accept lower throughput

## Relationships

- Tested on [[bcm43224-wifi]] hardware
- Affects [[macbook-air-5-2]] WiFi performance
- [[broadcom-wl-dkms]] provides the proprietary driver
- Part of PR #10910's hardware detection logic

## See Also

- [[bcm43224-wifi]] — The WiFi chipset
- [[broadcom-wl-dkms]] — Proprietary driver entity
- [[wifi-bcm43224-test-results]] — Physical test results
