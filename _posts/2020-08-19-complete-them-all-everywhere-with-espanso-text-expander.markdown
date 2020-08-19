---
title: Complete Them All Everywhere
date: 2020-08-19T10:42:03+01:00
---
...with Espanso text expander in Rust (works in Bash, Firefox,...)

## Getting Started ##

```bash
yay -S espanso-bin # install espanso package for archlinux
espanso status     # get espanso service status
espanso start      # start espanso service / create ~/.config/systemd/user/espanso.service if does not exist
espanso path       # list espanso config files
:date              # get current date from trigger :date config files
```

## Support ##

* fix X11 display context error with starting Espanso service

```bash
[[ -z $(grep DISPLAY $HOME/.config/systemd/user/espanso.service) ]] && \
  sed -i '/\[Service\]/aEnvironment="DISPLAY=:0"' $HOME/.config/systemd/user/espanso.service && \
  /usr/bin/systemctl --user daemon-reload  && \
  espanso start  # fix x11 display context error
```

## Sources ##

* [Getting Started](https://espanso.org/docs/get-started/)
* [Official Packages](https://hub.espanso.org/)
* [Offical Document](https://espanso.org/docs/)
* [Pour gagner du temps quand vous tapez au clavier](https://korben.info/espanso-gagner-temps-tapez-clavier.html) [in French]
* [Use Espanso Text Expander To Save Time And Increase Productivity](https://www.linuxuprising.com/2020/06/use-espanso-text-expander-to-save-time.html)
* [The Journey to My First 100 GitHub Stars](https://medium.com/@federicoterzi/the-journey-to-my-first-100-github-stars-aef05d796a18)
