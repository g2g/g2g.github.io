---
title: View markdown pages with Firefox
date: 2020-08-07T12:16:00+01:00
---

With Markdown Viewer Addon by Simeon Velichkov.

## Install ##

* <https://addons.mozilla.org/en-US/firefox/addon/markdown-viewer-chrome/>
* <https://github.com/simov/markdown-viewer>

## View local markdown pages ##

* press  &nbsp; **![markdown viewer icon](https://raw.githubusercontent.com/simov/markdown-viewer/master/icons/icon19.png)** &nbsp; button from toolbar
* press **advanced options** 
    * **Allowed Origins >** select `*://*`
* (you may need to use special configuration)[https://github.com/KeithLRobertson/markdown-viewer#support-for-local-files-on-linux] (from [issue #131](https://github.com/simov/markdown-viewer/issues/131))

## View file with rst extension ##

* press  &nbsp; **![markdown viewer icon](https://raw.githubusercontent.com/simov/markdown-viewer/master/icons/icon19.png)** &nbsp; button from toolbar
* press **advanced options** 
    * **MATCH :** `\.(?:markdown|mdown|mkdn|md|mkd|mdwn|mdtxt|mdtext|text|rst)(?:#.*|\?.*)?$`

## Table of Contents ##

* press  &nbsp; **![markdown viewer icon](https://raw.githubusercontent.com/simov/markdown-viewer/master/icons/icon19.png)** &nbsp; button from toolbar
* press `CONTENT` tab
    * activate `TOC`

## Reload automatically page ##

* press  &nbsp; **![markdown viewer icon](https://raw.githubusercontent.com/simov/markdown-viewer/master/icons/icon19.png)** &nbsp; button from toolbar
* press `CONTENT` tab
    * activate `AUTORELOAD`
