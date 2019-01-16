---
title: Blogging with Minimal Mistakes Jekyll theme
date: 2019-01-16T01:16:46+01:00
---

* **PROS**:
  * Github / Gitlab Pages **compatible**  
    (host your **static blog** on Github )
  * all gems **embedded**  
    (good for migration / reinstallation / testing in local)
  * create **easily** new post with Octopress (embedded too)
* **CONS**:
  * bad performance for generating static pages  
    with big blogs (unlike with Hugo)
  * made in Ruby
  * CLI addicted :)

## Install in Github Pages mode ##

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
bundle exec jekyll serve --watch                 # run in reload mode

```

## Add new content with Octopress ##

* automate the creation of new posts and pages for easier management


```sh
bundle add jekyll-paginate octopress
bundle exec octopress new post "Blogging with Minimal Mistakes Jekyll theme"
# TIP: alias for octopress
cat << EOF >> $HOME/.bashrc
alias octopress='bundle exec octopress'
EOF
```
## Deploy to Github Pages ##

```sh
# NEED: create myrepo.github.io repository in your Github repo
cd myrepo.github.io
git remote set origin git@github.com:myrepo/myrepo.github.io.git
git remote add upstream git@github.com:mmistakes/minimal-mistakes.git
git add .
git commit -am "My first post"
git push -u origin --all
xdg-open https://myrepo.github.io  # access to your personal blog

```

## Sources ##

* [Minimal Mistakes documentation](https://mmistakes.github.io/minimal-mistakes/docs/docs-2-2/#new-page)
* [Github Pages dependencies and versions](http://pages.github.com/versions/)
* [Bundle with Jekyll](https://jekyllrb.com/tutorials/using-jekyll-with-bundler/)


