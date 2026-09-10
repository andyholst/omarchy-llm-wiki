---
title: Kernel Module Installation
created: 2026-09-10
updated: 2026-09-10
type: concept
tags: [kernel, module, build, arch-linux]
sources: []
confidence: high
---

# Kernel Module Installation

Proper procedure for building and installing custom kernel modules on Arch Linux.

## Correct Procedure

### 1. Build the Module

```bash
cd /usr/lib/modules/$(uname -r)/build
make -j$(nproc) M=drivers/hwmon
```

### 2. Install the Module

```bash
sudo cp drivers/hwmon/applesmc.ko /lib/modules/$(uname -r)/updates/drivers/hwmon/
```

### 3. Update Dependencies

```bash
sudo depmod -a
```

### 4. Load the Module

```bash
sudo modprobe applesmc
```

### 5. Verify

```bash
lsmod | grep applesmc
ls /sys/class/power_supply/BAT0/charge_control_end_threshold
```

## Common Mistakes

| Mistake | Symptom | Fix |
|---------|---------|-----|
| Wrong path (`/usr/lib/modules/.old/`) | Module not found on boot | Use `/lib/modules/<ver>/` |
| Missing `depmod` | Module dependencies not resolved | Run `depmod -a` after install |
| Wrong kernel version | Module won't load | Build against running kernel |
| Missing firmware | Hardware not detected | Install firmware package |
| Wrong kernel source tree | Version mismatch errors | Build against the actual kernel you'll boot |

## Auto-Load on Boot

Create `/etc/modules-load.d/applesmc.conf`:

```
applesmc
```

Or use `modules-load.d` + `mkinitcpio` to include in initramfs.

## Version Matching

Modules must be built against the exact kernel version they'll run on. The kernel checks `vermagic` at load time:

```
applesmc: version magic '7.2.3 SMP preempt mod_unload' should be '7.2.3-arch1-3...'
```

This error means the module was built against a different kernel. Rebuild from the correct source tree.

## Relationships

- Used to install [[applesmc-driver]] patched module
- Required for [[macbook-air-5-2]] custom kernel support
- Part of [[luks-btrfs-boot]] when modules go in initramfs
- Manages [[bq20z451-battery]] when driver is properly installed

## See Also

- [[applesmc-driver]] — The module in question
- [[macbook-air-5-2]] — Hardware using this module
- [[luks-btrfs-boot]] — Boot setup requiring correct module install
- [[bq20z451-battery]] — Battery managed by the patched module
