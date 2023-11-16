---
title: Stream https flow with mpv and yt-dlp
date: 2023-11-16T18:34:22+01:00
---

## How to stream https flow with mpv and yt-dlp ?

```bash
yt-dlp -o - <url_to_stream> | mpv --demuxer-max-bytes=1G -
```

* with `--demuxer-max-bytes`, image stays sync with sound.
* to set specific configuration, you can use:
  * `~/.config/yt-dlp/config` 
  * `~/.config/mpv/mpv.conf`
