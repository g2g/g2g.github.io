---
title: Increase VM ZVOL for TrueNAS
aliases: 
categories:
  - proc
tags:
  - lvm
description: 
author: 
image: 
date: 2022-10-06T20:29:50+01:00
#date modified: 2025-03-25
cover:
  image: <https://amown.cn/PicGo/cover.png>
  alt: <alt text>
  caption: text
  relative: false
---
... to resize Debian VM Logical Volume

## Resize Linux VM's LLVM Virtual Disk on a ZVOL for TrueNAS ##

### Increase Zvol via UI

* increase ZFS disk size in TrueNAS UI
  * Storage tab > edit your zvol > modify "Size for this zvol" field value > Save

### Resize disk

* resize Debian VM disk
```bash
reboot
# fdisk mode
apt install gdisk -y
cfdisk /dev/sda # extends /dev/sda5 partition > write > quit
# parted mode
parted /dev/sda # print > resizepart 2 100% (extended) > resizepart 5 100% (logical) > quit
# for both
pvresize /dev/sda5
pvs
lvs
lvextend --resizefs serv0-vg/root /dev/sda5
```

* [source](https://www.truenas.com/community/resources/howto-resize-a-linux-vms-llvm-virtual-disk-on-a-zvol.174/)
