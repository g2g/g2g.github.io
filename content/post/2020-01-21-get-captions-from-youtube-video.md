---
title: Get captions from Youtube video
aliases: 
categories:
  - user
tags:
  - media
description: 
author: 
image: 
date: 2020-01-21T02:12:23+01:00
#date modified: 2025-03-25
cover:
  image: <https://amown.cn/PicGo/cover.png>
  alt: <alt text>
  caption: text
  relative: false
---

(...not video's subtitle)

```shell
youtube-dl --o "%(title)s.%(id)s.%(ext)s" $URL;  # first stop
youtube-dl --sub-lang en --write-auto-sub --sub-format srt --skip-download -o "%(title)s.%(id)s.%(ext)s" $URL;  # and finally

```

* if you're using mpv as video player, use v to display captions.
