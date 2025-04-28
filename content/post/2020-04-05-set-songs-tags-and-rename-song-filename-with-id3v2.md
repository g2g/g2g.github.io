---
title: Set songs tags and rename songs filename with id3v2
aliases: 
categories:
  - user
tags:
  - media
  - config
description: 
author: 
image: 
date: 2020-04-05T09:21:34+01:00
#date modified: 2025-03-25
cover:
  image: <https://amown.cn/PicGo/cover.png>
  alt: <alt text>
  caption: text
  relative: false
---

in **oneliner and mass renaming** mode

* get tags information with **exiftool** and copy tags /rename mp3 file with **id3v2**

```shell
IFS=$'\n';for MP3_NAME in *mp3; do
  ARTIST=$(exiftool -artist "$MP3_NAME" | awk -F': ' '{print $2}');
  SONG=$(exiftool -title "$MP3_NAME" | awk -F': ' '{print $2}');
  ALBUM=$(exiftool -album "$MP3_NAME" | awk -F': ' '{print $2}');
  id3v2 -a "$ARTIST" -t "$SONG" -A "$ALBUM" --genre 45  "$MP3_NAME" ;
  mv -vi "$MP3_NAME" "${ARTIST} - ${SONG}.mp3" ;
done;
IFS=$' \t\n'
```

* tags based on mp3 filename if some mp3 files are no tags with **exiftool**

```shell
# move mp3 files without tags in 3mpty directory
IFS=$'\n';for SONG in *mp3; do
  [ -z "$(exiftool -artist "$SONG")" ] && \
  mv -vi "$SONG" 3mpty/ ;
done
cd 3mpty

# set tags on mp3 files from filename with this format "artist - title.mp3"
IFS=$'\n'; for SONG_FILENAME in *mp3; do
  ARTIST=$(echo "$SONG_FILENAME" | sed 's/ - .*$//');
  TITLE=$(echo "$SONG_FILENAME" | sed 's/^.*- \(.*\)\..*$/\1/');
  id3v2 -a "$ARTIST" -t "$TITLE" "$SONG_FILENAME";
done;
IFS=$' \t\n'
```

* **id3v2** commands that may help

```shell
id3v2 -h
id3v2 --list-frames  # list id3v2 frames
id3v2 --list-genres  # list id3v1 genres
id3v2 --delete-all   # remove all tags from mp3 file
```
