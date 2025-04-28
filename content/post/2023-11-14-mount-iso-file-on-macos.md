---
title: Mount ISO file on MACOS
aliases: 
categories:
  - sys
tags:
  - mount
  - macos
description: 
author: 
image: 
date: 2023-11-14T10:08:13+01:00
#date modified: 2025-03-25
cover:
  image: <https://amown.cn/PicGo/cover.png>
  alt: <alt text>
  caption: text
  relative: false
---

* how to mount an iso file on MACOS ?

```bash
[[ -d tmp ]] && mkdir tmp
hdiutil attach -nomount debian-12.2.0-arm64-netinst.iso && \
  mount -t cd9660 /dev/disk5 ./tmp/
```
