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

### qemu uefi boot

```
$ qemu-system-x86_64 -daemonize -enable-kvm -cpu host -m 4096 \
-bios /usr/share/edk2-ovmf/x64/OVMF_CODE.fd \
-drive file=/usr/share/edk2-ovmf/x64/OVMF_CODE.fd,if=pflash,format=raw,unit=0,readonly=on \
-drive file=/usr/share/edk2-ovmf/x64/OVMF_VARS.fd,if=pflash,format=raw,unit=1,readonly=on \
-nic tap,ifname=tap0,script=no,downscript=no,vhost=on,model=virtio-net-pci \
-device virtio-vga-gl -display gtk,gl=on \
-drive file=/opt/vms/arch.img,if=virtio
```

## Folder Sharing

```
host qemu > -virtfs local,path=/opt,mount_tag=vfs,security_model=passthrough
guest # mount -t 9p -o trans=virtio,version=9p2000.L vfs /mnt/vfs
```
