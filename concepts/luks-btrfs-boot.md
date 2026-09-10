---
title: LUKS + Btrfs Boot Setup
created: 2026-09-10
updated: 2026-09-10
type: concept
tags: [luks, btrfs, systemd, mkinitcpio, limine]
sources: []
confidence: high
---

# LUKS + Btrfs Boot Setup

Full disk encryption with LUKS on a Btrfs filesystem, using systemd-based initramfs.

## Architecture

```
UEFI Firmware
  → Limine Bootloader (EFI stub)
    → vmlinuz + initramfs (separate files)
      → initramfs: sd-encrypt hook unlocks LUKS
        → Btrfs mounted from /dev/mapper/root
          → systemd boots from @
```

## Partition Layout

| Partition | Type | Purpose |
|-----------|------|---------|
| /dev/sda1 | FAT32 | EFI System Partition (ESP) |
| /dev/sda2 | LUKS | Encrypted container |
| → /dev/mapper/root | Btrfs | Root filesystem with subvolumes |

## Btrfs Subvolumes

- `@` — root filesystem
- `@home` — user home directories
- `@snapshots` — snapper snapshots
- `@swap` — swap file location

## mkinitcpio Hooks (Critical Order)

```
HOOKS=(base systemd autodetect microcode modconf kms keyboard sd-vconsole block sd-encrypt filesystems fsck)
```

The `sd-encrypt` hook provides systemd-based LUKS unlocking. It requires:

- `cryptsetup` binary in initramfs
- `dm-crypt.ko` and `dm-mod.ko` modules
- `cryptdevice=` kernel parameter

## Kernel Command Line

```
cryptdevice=PARTUUID=xxxx-xxxx-xxxx:root root=/dev/mapper/root rootflags=subvol=@ rw rootfstype=btrfs
```

## Common Pitfalls

1. **Missing dm-crypt in initramfs** — LUKS won't unlock, boot hangs
2. **Wrong PARTUUID** — cryptdevice not found, emergency shell
3. **Missing btrfs module** — root mount fails after unlock
4. **Wrong subvol** — system boots to snapshot instead of @

## Recovery

From emergency shell:

```bash
cryptsetup luksOpen /dev/sdXn root
mount -t btrfs -o subvol=@ /dev/mapper/root /mnt
```

## See Also

- [[macbook-air-5-2]] — Hardware using this setup
- [[kernel-module-install]] — Module installation for encrypted boot
- [[applesmc-driver]] — Module that must be in initramfs if loaded at boot
