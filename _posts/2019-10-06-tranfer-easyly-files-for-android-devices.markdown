---
title: Transfer easyly files for Android devices in SFTP mode
date: 2019-10-06T01:50:11+01:00
---

Transfer files for Android devices with Primitive FTPd server (ftp/sftp)

## Download Primitive FTPd server App at FDroid MarketPlace ##

* From Fdroid app or https://f-droid.org/en/packages/org.primftpd/

## Configure Primitive FTPd  ##

* set a password for user (Primitive FTPd default username)
* disable ftp server (SFTP only) 
* launch Primitive FTPd server
* upload authorized_keys

```
cat <<EOF> authorized_keys
ssh-rsa ...my super secure rsa pubkey
EOF
chmod 0700 authorized_keys
sftp -P 1234 user@<ip_displayed_by_primitive_ftpd>
> mkdir .ssh
> put authorized_keys
```

* enable "Authentication Public Key"
* restart Primitive FTPd server

## Configure your machine ##

* mount it for test purpose (or temporarily)
```
mkdir $HOME/droid
sshfs user@<ip_displayed_by_primitive_ftpd>: $HOME/droid  # mount
fusermount3 -u $HOME/droid
```
* mount it via fstab [BE ROOT]

```
cat <<EOF>> /etc/fstab
user@<ip_displayed_by_primitive_ftpd>: /home/user/droid  fuse.sshfs noauto,x-systemd.automount,_netdev,users,IdentityFile=/home/user/.ssh/id_rsa,allow_other,reconnect 0 0
EOF
```

That' s all !
