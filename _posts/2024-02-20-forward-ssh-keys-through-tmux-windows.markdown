---
title: Forward SSH keys through Tmux windows
date: 2024-02-20T10:44:05+01:00
---

* How to forward ssh public keys through Tmux windows?

```bash
cat<<~/.bashrc>>EOF
# forward ssh-agent
[[ -z $(pgrep ssh-agent) ]] && eval `ssh-agent` &>/dev/null
if [[ -S "$SSH_AUTH_SOCK" && ! -h "$SSH_AUTH_SOCK" ]]; then
    ln -sf "$SSH_AUTH_SOCK_LOCAL" ~/.ssh/ssh_auth_sock;
fi
export SSH_AUTH_SOCK=~/.ssh/ssh_auth_sock; # already in ~/.ssh/config
EOF
cat<<~/.ssh/config>>EOF
ForwardAgent yes
IdentityAgent ~/.ssh/ssh_auth_sock
EOF
```

## SOURCES

* [Martijnvermaat's gist](https://gist.github.com/martijnvermaat/8070533)
* [Stackoverflow](https://stackoverflow.com/questions/21378569/how-to-auto-update-ssh-agent-environment-variables-when-attaching-to-existing-tm)
* [Werat's post](https://werat.dev/blog/happy-ssh-agent-forwarding/)
* [Blogsystem5's post](https://blogsystem5.substack.com/p/ssh-agent-forwarding-and-tmux-done)
* [Ssh-agent Switcher tool](https://github.com/jmmv/ssh-agent-switcher/)
