---
title: Fix error symbol grub_calloc not found
date: 2020-09-08T20:56:06+01:00
---
... by restoring GRUB for crypted disks

After system update and reboot, GRUB failed with this error **`symbol 'grub_calloc' not found`**.

* fix it with these commands

```bash
cryptsetup open /dev/nvme0n1p3 data
pvs
vgs
vgchange -ay
lsblk -fs
mount /dev/mapper/arch-root /mnt/
mount /dev/mapper/arch-home /mnt/home/
mount /dev/nvme0n1p2 /mnt/boot/
mount /dev/nvme0n1p1 /mnt/boot/efi/
grub-install --root-directory=/mnt/  /dev/nvme0n1
# not necessary
arch-chroot /mnt/
```
