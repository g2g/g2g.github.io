---
title: Detect virtualization technology used by the OS
aliases: 
categories:
  - proc
tags:
  - vm
  - config
description: 
author: 
image: 
date: 2019-11-17T19:31:20+01:00
#date modified: 2025-03-25
cover:
  image: <https://amown.cn/PicGo/cover.png>
  alt: <alt text>
  caption: text
  relative: false
---

* detect virtualization technology

```shell
dmidecode -s system-product-name || systemd-detect-virt
```
* [source](https://www.dmo.ca/blog/detecting-virtualization-on-linux/)
