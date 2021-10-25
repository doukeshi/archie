# QEMU

```
# pacman -S qemu edk2-ovmf
$ cd /opt/vms/
$ qemu-img create -f qcow2 arch.img 32G
```

## Virtual Network

```
# ip link add br0 type bridge
# ip link set dev br0 up
# ip addr add 10.2.2.2/24 brd + dev br0

# dnsmasq --interface=br0 --bind-interfaces --dhcp-range=10.2.2.15,10.2.2.254

# sysctl -w net.ipv4.ip_forward=1
# iptables -t nat -A POSTROUTING -o wlan0 -j MASQUERADE
```

## Minimal Boot

### nic tap0

```
# ip tuntap add dev tap0 mode tap group kvm
# ip link set dev tap0 up
# ip link set dev tap0 master br0
```

### qemu boot

```
$ qemu-system-x86_64 -daemonize -enable-kvm -boot menu=on \
-bios /usr/share/edk2-ovmf/x64/OVMF_CODE.fd \
-cpu host -m 4096 \
-nic tap,ifname=tap0,script=no,downscript=no,vhost=on,model=virtio-net-pci \
-device virtio-vga-gl -display gtk,gl=on \
-drive file=/opt/vms/arch.img,if=virtio
```

## cdrom option

```
-cdrom /opt/vms/archlinux-2021.10.01-x86_64.iso
```

## Folder Sharing

```
host # /usr/lib/qemu/virtiofsd --socket-path=/var/run/qemu-virtiofs.sock -o source=/share -o cache=always
host # chown x:kvm /var/run/qemu-virtiofs.sock

guest # mount -t virtiofs vfs /mnt/vfs
```

### qemu options:

```
-object memory-backend-memfd,id=mem,size=4G,share=on \
-numa node,memdev=mem \
-chardev socket,id=char0,path=/var/run/qemu-virtiofs.sock \
-device vhost-user-fs-pci,chardev=char0,tag=vfs \
```
