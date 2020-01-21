---
title: Get captions from Youtube video
date: 2020-01-21T02:12:23+01:00
---

(...not video's subtitle)

```
youtube-dl --o "%(title)s.%(id)s.%(ext)s" $URL;  # first stop
youtube-dl --sub-lang en --write-auto-sub --sub-format srt --skip-download -o "%(title)s.%(id)s.%(ext)s" $URL;  # and finally

```

* if you're using mpv as video player, use v to display captions.
