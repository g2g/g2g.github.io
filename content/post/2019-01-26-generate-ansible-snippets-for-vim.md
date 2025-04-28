---
title: Generate Ansible snippets for VIm completion
aliases: 
categories:
  - dev
tags:
  - vim
  - ansible
  - config
description: 
author: 
image: 
date: 2019-01-26T01:50:11+01:00
#date modified: 2025-03-25
cover:
  image: <https://amown.cn/PicGo/cover.png>
  alt: <alt text>
  caption: text
  relative: false
---

With one python script, get an UltraSnips file for VIm Ansible modules completion from Ansible 2.2.1.0 and Python 2.7.13.

## Build A Debian 9 Stretch VM ##

```sh
mkdir debian && cd debian
vagrant init debian/stretch64
vagrant ssh
```

## Generate UltraSnips File ##

```sh
apt-get install -y ansible git
git clone https://github.com/z0mbix/ansible_snippet_generator /tmp/snippet_generator
/tmp/snippet_generator/snippet_generator.py --ultisnips /usr/lib/python2.7/dist-packages/ansible/modules > /vagrant/ansible.snippets
```

## Sources ##

* [Ansible Snippet Generator Git Repo](https://github.com/z0mbix/ansible_snippet_generator)

That's all !

