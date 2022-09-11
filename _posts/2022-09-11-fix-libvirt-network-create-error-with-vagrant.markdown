---
title: Fix libvirt network create error with vagrant
date: 2022-09-11T16:50:16+01:00
---

* when `vagrant up`

```
`create': Call to virD
omainCreateWithFlags failed: Network not found: no network with matching name 'vagrant-libvirt' (Libvirt::Error)
```

* fix it

```bash
cat <EOF> /var/tmp/vagrant-libvirt.xml
<!--
WARNING: THIS IS AN AUTO-GENERATED FILE. CHANGES TO IT ARE LIKELY TO BE
OVERWRITTEN AND LOST. Changes to this xml configuration should be made using:
  virsh net-edit default
or other application using the libvirt API.
-->

<network>
  <name>vagrant-libvirt</name>
  <uuid>17f365b0-4da6-4f19-91b6-c4dde30d6ac0</uuid>
  <forward mode='nat'/>
  <bridge name='virbr1' stp='on' delay='0'/>
  <mac address='52:54:00:0f:4f:10'/>
  <domain name='kvm' localOnly='yes'/>
  <ip address='192.168.122.1' netmask='255.255.255.0'>
    <dhcp>
      <range start='192.168.122.2' end='192.168.122.254'/>
    </dhcp>
  </ip>
</network>
EOF
virsh net-define /var/tmp/vagrant-libvirt.xml
virsh net-start vagrant-libvirt
virsh net-autostart vagrant-libvirt
virsh net-list
brctl show
```

* [create +libvirt +network](https://kashyapc.fedorapeople.org/virt/create-a-new-libvirt-bridge.txt)

