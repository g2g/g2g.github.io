---
title: TLDR as customizable collaborative cheatsheets tool
date: 2023-01-21T09:26:49+01:00
---

**[tldr-pages](https://github.com/tldr-pages/tldr)** project contains a lot of Linux commands cheatsheets.
But you can [easily contribute with pull requests](https://github.com/tldr-pages/tldr/blob/main/CONTRIBUTING.md) [(1)](https://github.com/tldr-pages/tldr/blob/main/contributing-guides/git-terminal.md) to customize it.
In this case, follow the guide below.

```bash
# install tldr rust client
paru -S tealdeer
# fork tldr-pages project from your user github repo
git clone git@github.com:my_user/tldr.git ~/.cache/tealdeer/tldr-pages
```

By this way, you can :
- get locally your modifications with `tldr command`
- modify markdown pages inside `~/.cache/tealdeer/tldr-pages/`
- contribute with PR to the project
