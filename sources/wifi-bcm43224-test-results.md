---
type: source
title: "WiFi Test Results: MacBook Air 5,2 with BCM43224"
authors: ["Physical hardware test"]
url: "https://github.com/andyholst/omarchy/pull/10910"
raw: "raw/articles/wifi-bcm43224-test-results.md"
ingested: 2026-09-11
tags: [wifi, broadcom, hardware, testing, macbook-air]
entities: [macbook-air-5-2, bcm43224-wifi, broadcom-wl-dkms]
concepts: [wifi-driver-comparison]
---

# WiFi Test Results: MacBook Air 5,2 with BCM43224

Physical verification of WiFi performance on MacBook Air 5,2 hardware after applying Andy Holst's PR #10910 patch that switches from open-source brcmsmac to proprietary broadcom-wl-dkms driver.

## Key Results

| Metric | BEFORE (brcmsmac) | AFTER (broadcom-wl/dkms) | Delta |
|--------|-------------------|-------------------------|-------|
| Link speed | 144.4 MBit/s | 300 MBit/s | **+2.1x** |
| Real download | 5.76 MB/s | 11.46 MB/s | **+2.0x** |
| Signal | -35 dBm | -42 dBm | similar |
| Ping avg | 5.1 ms | ~5 ms | same |

## Analysis

The patch delivers **2x real-world speed improvement** on this hardware. The PR's claim of 1170 MBit/s link was tested on a different network; this machine caps at 300 MBit/s due to router/AP limitations.

The broadcom-wl-dkms driver provides significantly better performance than brcmsmac for BCM43224 hardware. Trade-off: proprietary firmware required.

## PR #10910 Details

Andy Holst's PR adds BCM43224 detection to Omarchy's hardware detection and blacklists brcmsmac in favor of broadcom-wl-dkms. Specific to MacBook Air 5,2 hardware.

## Where this fits

- [[macbook-air-5-2]] — Hardware tested
- [[bcm43224-wifi]] — WiFi chip entity
- [[broadcom-wl-dkms]] — Proprietary driver entity
- [[wifi-driver-comparison]] — brcmsmac vs broadcom-wl analysis
