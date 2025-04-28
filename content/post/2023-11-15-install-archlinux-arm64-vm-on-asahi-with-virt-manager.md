---
title: Install Archlinux arm64 VM on Asahi with Virt-manager
aliases: 
categories:
  - unix
tags:
  - vm
  - tool
description: 
author: 
image: 
date: 2023-11-15T16:06:47+01:00
#date modified: 2025-03-25
cover:
  image: <https://amown.cn/PicGo/cover.png>
  alt: <alt text>
  caption: text
  relative: false
---

* `libvirtd` is used to manage VMs
* `libvirt` and `dnsmasq` are installed on the host
* `virt-manager` is running from Apple MBP M2 laptop

## ON LAPTOP

```bash
brew install virt-manager
```

* add connection 
  * File > Add connection > tick "Connect to remote host over SSH"
  * fill "Username" and "Hostname"
  * tick "Autoconnect"

## ON HOST

* install for uefi support

```bash
## from https://archlinux.org/packages/extra/any/edk2-aarch64/
wget https://mirror.sunred.org/archlinux/extra/os/x86_64/edk2-aarch64-202308-3-any.pkg.tar.zst
pacman -U edk2-aarch64-202308-3-any.pkg.tar.zst
```

## ARCHLINUX ARM64 ISO

* [download archboot arm64 iso](https://archboot.com/iso/aarch64/latest/)

## INSTALLATION

* install with grub uefi
* because of weird characters at reboot, connect with `virsh` command

* from laptop

```bash
cat<<EOF>>~/.config/libvirt/libvirt.conf
uri_default=qemu+ssh://<user>@<server_host>/system
EOF
virsh console --domain <archlinux_arm64>
```

## SOURCES

* [Ubuntu Asahi Qemu](https://github.com/AsahiLinux/docs/wiki/SW%3AUbuntu-Asahi-Qemu)
* [Windows vm on Asahi Qemu/kvm Virtmanager](https://www.reddit.com/r/AsahiLinux/comments/107m4nb/windows_vm_on_asahi_qemukvm_virtmanager/)
* [Virtual Machines on Asahi Linux](https://www.reddit.com/r/AsahiLinux/comments/y6hplo/virtual_machines_on_asahi_linux/)


* ENJOY !
