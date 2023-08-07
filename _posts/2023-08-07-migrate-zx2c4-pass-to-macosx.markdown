---
title: Migrate ZX2C4 pass to MacOSX
date: 2023-08-07T19:55:53+01:00
---
... or how to migrate your pass keys softly

## Source ##

```bash
for FOLDER in $HOME/.password-store $HOME/.gnupg ; do
  rsync -arv --delete ${FOLDER}/ macosx:${FOLDER}/;
done
```

## Target

```bash
brew install gnupg pass pinentry
gpg --list-key toto@perdu.com # ensure that gpg email user is the same as git email user
git config --global --edit    # ensure that gpg email user is the same as git email user

cat<<EOF>>$HOME/.bash_profile
eval "$(/opt/homebrew/bin/brew shellenv)"
[[ -f ~/.bashrc ]] && source ~/.bashrc
EOF

cat<<EOF>>$HOME/.bashrc
# password-store completion
for COMPLETION in /opt/homebrew/etc/bash_completion.d/* ; do
  source $COMPLETION;
done

[[ -z $(pgrep gpg-agent) ]] && gpg-agent --pinentry-program=/opt/homebrew/bin/pinentry-tty --daemon # for password-store
EOF
```