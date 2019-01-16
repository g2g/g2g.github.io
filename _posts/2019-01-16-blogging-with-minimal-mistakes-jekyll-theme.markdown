---
title: Blogging with Minimal Mistakes Jekyll theme
date: 2019-01-16T01:16:46+01:00
---

## Install with Github Pages compatibility ##

* use **bundle 2.0**
* **all gems** are embedded in repository's **./vendor/bundle** folder

```sh
git clone git@github.com:mmistakes/minimal-mistakes.git myrepo.github.io
cd myrepo.github.io/
rm Gemfile
bundle init
bundle install --path vendor/bundle              # embedded gems
bundle add github-pages --group=jekyll_plugins
bundle add minimal-mistakes-jekyll
bundle exec jekyll serve --watch                 # run jekyll locally in reload mode

```

## Add new content with Octopress ##

* automate the creation of new posts and pages for easier management


```
bundle add jekyll-paginate octopress
bundle exec octopress new post "Blogging with Minimal Mistakes Jekyll theme"

```

## Sources ##

* [Minimal Mistakes documentation](https://mmistakes.github.io/minimal-mistakes/docs/docs-2-2/#new-page)
* [Github Pages dependencies and versions](http://pages.github.com/versions/)
* [Bundle with Jekyll](https://jekyllrb.com/tutorials/using-jekyll-with-bundler/)


