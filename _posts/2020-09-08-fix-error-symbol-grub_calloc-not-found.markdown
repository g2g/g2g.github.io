---
title: Fix error symbol grub_calloc not found
date: 2020-09-08T20:56:06+01:00
---
... by restoring GRUB for crypted disks

After system update and reboot, GRUB failed with this error **`symbol 'grub_calloc' not found`**.

* fix it with these commands

```bash
fsck /dev/nvme0n1p*
efibootmgr -c --disk /dev/nvme0n1
efibootmgr -v /dev/nvme0n1
```

* check in your BIOS if EFI boot is always configured (link to /boot/efi/EFI/arch/grubx64.efi)

* in bonus, if you want to mount your crypted system

```bash
cryptsetup open /dev/nvme0n1p3 data
pvs
vgs
vgchange -ay
lsblk -fs
mount /dev/mapper/arch-root /mnt/
mount /dev/mapper/arch-home /mnt/home/
mount /dev/nvme0n1p2 /mnt/boot/
mount /dev/nvme0n1p1 /mnt/boot/efi/                                                # for UEFI systems
arch-chroot /mnt
```

* [GRUB by Archlinux Wiki](https://wiki.archlinux.org/index.php/GRUB)
