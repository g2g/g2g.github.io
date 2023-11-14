---
title: Mount ISO file on MACOS
date: 2023-11-14T10:08:13+01:00
---

* how to mount an iso file on MACOS ?

```bash
[[ -d tmp ]] && mkdir tmp
hdiutil attach -nomount debian-12.2.0-arm64-netinst.iso && \
  mount -t cd9660 /dev/disk5 ./tmp/
```
