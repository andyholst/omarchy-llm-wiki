---
source_url: https://github.com/andyholst/omarchy/pull/10910
ingested: 2026-09-11
sha256: a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7f8a9b0c1d2e3f4a5b6c7d8e9f0a1b2
---

# WiFi Test Results: MacBook Air 5,2 with BCM43224

## Test Setup

- **Hardware**: MacBook Air 5,2 (Mid-2012), Broadcom BCM43224 WiFi (14e4:4353)
- **OS**: Omarchy Linux (Arch-based), kernel 7.2.3-arch1-3
- **Router**: 802.11n/ac dual-band
- **Test date**: 2026-09-10

## Results

| Metric | BEFORE (brcmsmac) | AFTER (broadcom-wl/dkms) | Delta |
|--------|-------------------|-------------------------|-------|
| Driver | brcmsmac (open) | wl (proprietary) | — |
| Link speed | 144.4 MBit/s | 300 MBit/s | **+2.1x** |
| Signal | -35 dBm | -42 dBm | similar |
| Real download | 5.76 MB/s | 11.46 MB/s | **+2.0x** |
| Ping avg | 5.1 ms | ~5 ms | same |

## Analysis

The patch **works** — 2x real-world speed improvement. The PR's claim of 1170 MBit/s link was tested on a different network; this machine caps at 300 MBit/s (likely router/AP limitations).

The broadcom-wl-dkms driver provides significantly better performance than the open-source brcmsmac driver for BCM43224 hardware. The trade-off is using proprietary firmware.

## PR #10910 Details

Andy Holst's PR adds BCM43224 detection to Omarchy's hardware detection and blacklists the open-source brcmsmac driver in favor of broadcom-wl-dkms. This is specific to MacBook Air 5,2 hardware.

## Conclusion

Physical verification confirms the PR's claims of improved WiFi performance. The 2x speed improvement is real and measurable on this hardware.
