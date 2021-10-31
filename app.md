# APP

## X

```
# pacman -S chromium
# pacman -S alsa-utils mpv
# pacman -S git zsh tmux emacs dnsmasq openssh

$ yay -S vscodium-bin
```

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

## fcitx5

```
# pacman -S fcitx5-im fcitx5-chinese-addons (fcitx5-material-color)
$ echo "fcitx5 -d" >> ~/.xinitrc     // before `exec dmw`

$ cat ~/.pam_environment
GTK_IM_MODULE   DEFAULT=fcitx
QT_IM_MODULE    DEFAULT=fcitx
XMODIFIERS      DEFAULT=@im=fcitx
INPUT_METHOD    DEFAULT=fcitx
SDL_IM_MODULE   DEFAULT=fcitx

$ fcitx5-configtool
```

## yay

```
$ cd /opt/lib
$ git clone https://aur.archlinux.org/yay.git --depth=1
$ cd yay
$ makepkg -si    // deps golang
```

## Scripts

```
$ setxkbmap -option ctrl:nocaps
$ iwctl [--passphrase xxxx] station wlan0 connect SSID

// ssh-agent
$ echo 'eval "$(ssh-agent -s)"' >> ~/.zshrc
$ echo 'ssh-add ~/.ssh/xxxx'    >> ~/.zshrc
```
