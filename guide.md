# Guide

## Bootstrap

```
# dd bs=512M status=progress if=img.iso of=/dev/xxxx
# pacstrap /mnt base linux (linux-firmware)
```

**`# arch-chroot /mnt`**

## X

```
# pacman -S intel-ucode/amd-ucode iwd base-devel vi
# pacman -S noto-fonts (noto-fonts-cjk noto-fonts-emoji noto-fonts-extra)

// Timezone
# ln -sf /usr/share/zoneinfo/UTC /etc/localtime

// Localization
# echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
# locale-gen
# echo "LANG=en_US.UTF-8" >> /etc/locale.conf

// Network
# echo "arch" > /etc/hostname

// User
# passwd root
# useradd -G kvm,wheel -m -s /bin/bash x
# passwd x
```

## Bootloader

```
# cd /boot
# bootctl install
# cp /usr/share/systemd/bootctl/arch.conf /boot/loader/entries/
# cat /boot/loader/entries/arch.conf
title   Arch Linux
linux   /vmlinuz-linux
initrd  /intel-ucode.img
initrd  /initramfs-linux.img
options root=/dev/xxxx
```

**`# reboot`**

## Wireless: iwd + systemd-resolved

```
# ln -sf /run/systemd/resolve/stub-resolv.conf /etc/resolv.conf
$ cat /etc/iwd/main.conf
[General]
EnableNetworkConfiguration=true
[Network]
NameResolvingService=systemd
```

### Ethernet: systemd-networkd + systemd-resolved

```
$ cat /etc/systemd/network/eth0.network
[Match]
Name=eth0
[Network]
DHCP=yes
```
