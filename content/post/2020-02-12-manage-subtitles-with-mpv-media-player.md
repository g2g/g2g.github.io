---
title: Manage subtitles with mpv media player
aliases: 
categories:
  - user
tags:
  - media
  - config
description: 
author: 
image: 
date: 2020-02-12T10:11:15+01:00
#date modified: 2025-03-25
cover:
  image: <https://amown.cn/PicGo/cover.png>
  alt: <alt text>
  caption: text
  relative: false
---

with hotkeys

* add custom hotkeys to increase / decrease subtitle size

```shell
cat <EOF>> ~/.config/mpv/input.conf
# increase subtitle font size
ALT+k add sub-scale +0.1

# decrease subtitle font size
ALT+j add sub-scale -0.1

```

* *HOTKEYS*
  * *v*     => show/hide subtitle
  * *ALT+k* => increase subtitle size
  * *ALT+j* => decrease subtitle size
