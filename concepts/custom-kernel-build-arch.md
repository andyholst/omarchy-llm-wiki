---
type: concept
title: Custom Kernel Build (Arch Linux)
created: 2026-09-11
updated: 2026-09-11
tags: [kernel, build, arch-linux, makepkg, power]
sources: [[kernel-applesmc-charge-threshold]]
confidence: high
---

# Custom Kernel Build (Arch Linux)

How to build a custom Arch Linux kernel the "Arch way" using `makepkg` and a custom PKGBUILD, while preserving the stock kernel as a fallback.

## When Needed

- Patching drivers that are built into the stock kernel (`=y` instead of `=m`)
- Adding custom kernel features not in the stock config
- Testing kernel changes without destroying the working system

## The Arch Way

1. **Get kernel source**: `asp export linux` or clone from GitHub
2. **Modify the PKGBUILD**: Change version, add patches, modify config
3. **Build**: `makepkg -s` in the kernel directory
4. **Install**: `sudo pacman -U linux-custom-x.x.x-x-x86_64.pkg.tar.zst`

## Key Principle: Preserve the Stock Kernel

Always install the custom kernel **alongside** the stock kernel, not as a replacement:

```
linux          — stock kernel (untouched fallback)
linux-custom   — your patched kernel (default boot)
```

This ensures you can always boot into a working system if the custom kernel fails.

## With Charge Threshold Patch

For the [[applesmc-driver]] charge control patch:

- Stock Arch has `CONFIG_SENSORS_APPLESMC=y` (built-in, can't load DKMS)
- Custom kernel sets `CONFIG_SENSORS_APPLESMC=m` (as module) or applies the patch directly
- Build from Andy Holst's `fix/macbookair-charge-control` branch

## Boot Loader Setup

With [[luks-btrfs-boot]], both kernels appear in Limine:

```
/+Omarchy
  //linux            7.2.3-arch1-3    (stock, fallback)
  //linux-applesmc   7.2.4            (new, default)
```

Each kernel has its own initramfs. Both use the same LUKS-encrypted Btrfs root.

## Relationships

- Used by [[linux-applesmc-kernel]] for build process
- Required for [[macbook-air-5-2]] custom kernel support
- Part of [[luks-btrfs-boot]] multi-kernel boot setup
- Integrates [[applesmc-driver]] patched module

## See Also

- [[linux-applesmc-kernel]] — Custom kernel entity
- [[applesmc-driver]] — Driver being patched
- [[luks-btrfs-boot]] — Boot setup with multiple kernels
- [[kernel-module-install]] — Module installation procedure
