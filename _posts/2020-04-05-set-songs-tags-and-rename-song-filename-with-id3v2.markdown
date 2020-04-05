---
title: Set songs tags and rename song filename with id3v2
date: 2020-04-05T09:21:34+01:00
---

in **oneliner mode**

* get tags information with **exiftool** and copy tags /rename mp3 file with **id3v2**

```shell
IFS=$'\n';for MP3_NAME in *mp3; do \
ARTIST=$(exiftool -artist "$MP3_NAME" | awk -F': ' '{print $2}');\
SONG=$(exiftool -title "$MP3_NAME" | awk -F': ' '{print $2}');\
ALBUM=$(exiftool -album "$MP3_NAME" | awk -F': ' '{print $2}');\
id3v2 -a "$ARTIST" -t "$SONG" -A "$ALBUM" --genre 45  "$MP3_NAME" ;\
mv -vi "$MP3_NAME" "${ARTIST} - ${SONG}.mp3" ;\
done\
IFS=$' \t\n'
```
* **id3v2** commands that may help

```shell
id3v2 -h
id3v2 --list-frames  # list id3v2 frames
id3v2 --list-genres  # list id3v1 genres
id3v2 --delete-all   # remove all tags from mp3 file
```
