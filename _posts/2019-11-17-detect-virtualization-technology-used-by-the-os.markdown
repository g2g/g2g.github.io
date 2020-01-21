---
title: Detect virtualization technology used by the OS
date: 2019-11-17T19:31:20+01:00
---

* detect virtualization technology

```shell
dmidecode -s system-product-name || systemd-detect-virt
```
* [source](https://www.dmo.ca/blog/detecting-virtualization-on-linux/)
