---
title: Manage subtitles with mpv media player
date: 2020-02-12T10:11:15+01:00
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
