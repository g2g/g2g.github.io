---
title: Archlinux install with UEFI / BTRFS
date: 2021-01-29T20:13:52+01:00
---
... in UNATTENDED mode

## PRE-INSTALL ##

* [download Archlinux ISO](https://archlinux.org/download/)

```bash
aria2c 'https://archlinux.org/releng/releases/2021.01.01/torrent/'
sha1sum archlinux-2021.01.01-x86_64.iso
gpg --receive-keys 0x4AA4767BBC9C4B1D18AE28B77F2D434B9741E8AC
gpg --verify archlinux-2021.01.01-x86_64.iso.sig
```

## INSTALL FROM LIVECD ##

**! CAUTION !**

> IT WILL DELETE ALL DATA FROM YOUR **FIRST HDD DEVICE**
> ( SATA or SSD )

```bash
MY_DEVICE="$(awk '/ sd| vd| nvme/{print $4}' /proc/partitions | head -1)"

timedatectl set-ntp true

parted /dev/${MY_DEVICE} -s mklabel gpt mkpart ESP fat32 1M 128M set 1 boot on mkpart primary ext4 128M 100%

mkfs.vfat -n ESP /dev/${MY_DEVICE}1
mkfs.btrfs -f -L ROOT /dev/${MY_DEVICE}2

mount -t btrfs /dev/${MY_DEVICE}2 /mnt/
btrfs subvolume create /mnt/@root
btrfs subvolume create /mnt/@var
btrfs subvolume create /mnt/@home
btrfs subvolume create /mnt/@snapshots

umount /mnt
mount -o subvol=@root /dev/${MY_DEVICE}2 /mnt
mkdir /mnt/{var,home,.snapshots}
mount -o subvol=@var /dev/${MY_DEVICE}2 /mnt/var
mount -o subvol=@home /dev/${MY_DEVICE}2 /mnt/home/
mount -o subvol=@snapshots /dev/${MY_DEVICE}2 /mnt/.snapshots

mkdir /mnt/boot
mount /dev/${MY_DEVICE}1 /mnt/boot

pacstrap /mnt base linux linux-firmware base-devel make binutils btrfs-progs zsh vim git sudo efibootmgr wpa_supplicant dialog iw bash-completion

genfstab -L /mnt >> /mnt/etc/fstab
```

## INSTALL FROM CHROOT ##

```bash
HOST_NAME='archlinux'
MY_PUBKEY='<my_ssh_pubkey>'
MY_USER='<my_user>'
MY_USER_PASS='<my_password>'
ROOT_PASS='<root_password>'
arch-chroot /mnt /bin/bash <<EOF
ln -sv /usr/share/zoneinfo/Europe/Paris /etc/localtime
hwclock --systohc
sed -i '/^#fr_FR.UTF-8\|^#en_US.UTF-8/{s/^#//}' /etc/locale.gen
locale-gen
echo 'LANG=en_US.UTF-8' > /etc/locale.conf
echo 'KEYMAP=us' > /etc/vconsole.conf
echo 'FONT=latarcyrheb-sun32' >> /etc/vconsole.conf
echo ${HOST_NAME} > /etc/hostname
cat <<HOSTS>> /etc/hosts
127.0.0.1       localhost
::1             localhost
127.0.1.1       ${HOST_NAME}.localdomain ${HOST_NAME}
HOSTS

echo 'root:${ROOT_PASS}' | chpasswd
useradd -m -g users -G wheel -s /bin/bash ${MY_USER}
echo '${MY_USER}:${MY_USER_PASS}' | chpasswd
sed -i.BKP '/HOOKS=/{s/=.*/=(base systemd autodetect modconf block keyboard sd-vconsole sd-encrypt filesystems)/}' /etc/mkinitcpio.conf
grep HOOKS /etc/mkinitcpio.conf
mkinitcpio -p linux
bootctl --path=/boot install

pacman-key --init
pacman-key --populate archlinux

pacman -Syu --noconfirm
pacman -S base-devel gnu-netcat intel-ucode ncdu openssh --noconfirm

timedatectl set-ntp true

systemctl enable sshd systemd-networkd systemd-resolved systemd-timesyncd

git clone https://aur.archlinux.org/yay.git /usr/src/yay
chmod -R ${MY_USER}: /usr/src/yay
su - ${MY_USER} -c 'cd /usr/src/yay/ && makepkg -si'

cat <<BOOT_ARCH> /boot/loader/entries/arch.conf
title		Arch Linux
linux		/vmlinuz-linux
initrd		/intel-ucode.img
initrd		/initramfs-linux.img
options		rw root=/dev/${MY_DEVICE}2 rootflags=subvol=@root
BOOT_ARCH

cat <<BOOT_LOAD> /boot/loader/loader.conf
default    arch
BOOT_LOAD

networkctl list

cat <<NETWORKD_LAN> /etc/systemd/network/lan.network
[Match]
Name=e*
[Network]
DHCP=ipv4
NETWORKD_LAN

cat <<RESOLVED> /etc/systemd/resolved.conf.d/dns_servers.conf
[Resolve]
DNS=9.9.9.9
Domains=~.
RESOLVED

# USERS #

cat <<USER_SUDO> /etc/sudoers.d/${MY_USER}
${MY_USER} ALL=(ALL) NOPASSWD: ALL
USER_SUDO

mkdir /root/.ssh /home/${MY_USER}/.ssh

cat <<ROOT_AUTH> /root/.ssh/authorized_keys
${MY_PUBKEY}
ROOT_AUTH

cat <<USER_AUTH> /home/${MY_USER}/.ssh/authorized_keys
${MY_PUBKEY}
USER_AUTH

chmod -Rc 0700 /root/.ssh /home/${MY_USER}/.ssh
chown -Rc ${MY_USER}: /home/${MY_USER}/.ssh/

# VIRTUALIZATION #

pacman -S dmidecode dnsmasq docker-compose ebtables libvirt qemu vagrant --noconfirm

systemctl enable docker libvirtd

usermod -aG docker,libvirt,kvm ${MY_USER}

su - ${MY_USER} -c 'vagrant plugin install vagrant-libvirt'

exit
EOF
reboot
```

## SOURCES ##

* [Official ArchLinux Installation](https://wiki.archlinux.org/index.php/Installation_guide)
* Main references for this article:
  * [Archlinux install on XPS 13 9360](https://gist.github.com/njam/85ab2771b40ccc7ddcef878eb82a0fe9)
  * [ArchLinux step-by-step installation on btrfs](https://gist.github.com/idvoretskyi/9a516921fab0ad4e3ea0)
* See more...
  * [Minimal instructions for installing ArchLinux](https://gist.github.com/mattiaslundberg/8620837)
  * [Archlinux install from Artizirk](https://gist.github.com/artizirk/e4a83f19f0879fd60e22fdc683dd246c)
  * [Efficient Encrypted UEFI-Booting Arch Installation](https://gist.github.com/HardenedArray/31915e3d73a4ae45adc0efa9ba458b07)
