# APP

## GUI

### Deps

```
# pacman -S xorg-server xorg-xinit (xorg-xrandr)
# pacman -S noto-fonts
# pacman -S libxft libxinerama    // deps by dwm
```

### suckless

```
$ cd /opt/suckless
$ git clone https://git.suckless.org/dwm    --depth=1
$ git clone https://git.suckless.org/st     --depth=1
$ git clone https://git.suckless.org/dmenu  --depth=1

$ cd dwm
$ sudo make clean install

$ echo 'exec dwm' > ~/.xinitrc
$ startx
```

## yay

```
$ cd /opt/lib
$ git clone https://aur.archlinux.org/yay --depth=1
$ cd yay
$ make -si    // deps golang
```
