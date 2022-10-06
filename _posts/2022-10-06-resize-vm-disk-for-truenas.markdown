---
title: Increase VM ZVOL for TrueNAS
date: 2022-10-06T20:29:50+01:00
---
... to resize Debian VM Logical Volume

## Resize Linux VM's LLVM Virtual Disk on a ZVOL for TrueNAS ##

* increase ZFS disk size in TrueNAS UI
  * Storage tab > edit your zvol > modify "Size for this zvol" field value > Save

* resize Debian VM disk
```bash
reboot
apt install gdisk -y
cfdisk /dev/sda # extends /dev/sda5 partition > write > quit
pvresize /dev/sda5
pvs
lvs
lvextend --resizefs serv0-vg/root /dev/sda5
```

* [source](https://www.truenas.com/community/resources/howto-resize-a-linux-vms-llvm-virtual-disk-on-a-zvol.174/)
