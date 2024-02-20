---
title: Forward SSH keys through Tmux windows
date: 2024-02-20T10:44:05+01:00
---

* how to forward ssh public keys through Tmux windows

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
* https://gist.github.com/martijnvermaat/8070533 / https://stackoverflow.com/questions/21378569/how-to-auto-update-ssh-agent-environment-variables-when-attaching-to-existing-tm
* https://werat.dev/blog/happy-ssh-agent-forwarding/
* https://blogsystem5.substack.com/p/ssh-agent-forwarding-and-tmux-done / https://github.com/jmmv/ssh-agent-switcher/
