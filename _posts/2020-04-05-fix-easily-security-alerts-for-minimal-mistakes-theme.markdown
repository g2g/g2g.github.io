---
title: Fix easily security alerts for Minimal Mistakes theme
date: 2020-04-05T11:00:19+01:00
---

with **git** command

* **prerequisites**

```shell
git remote add upstream git@github.com:mmistakes/minimal-mistakes.git  # in your github repository
git fetch --all
```

* **update files** from mmistakes v.4.19.1 according to **Github network alerts**

```shell
git checkout 4.19.1 -- minimal-mistakes-jekyll.gemspec package.json package-lock.json
git commit -m "[update] from minimal mistakes 4.19.1 release"
```
