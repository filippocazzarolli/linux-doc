#### Installing YAY
```
mkdir sources && \
cd sources && \
git clone https://aur.archlinux.org/yay.git && \
cd yay && \
makepkg -si
```

#### bash completion
`sudo pacman -S bash-completion`

#### font
`pacman -S fontconfig`

`fc-list` show install font

`sudo pacman -S noto-fonts ttf-ubuntu-font-family ttf-dejavu ttf-freefont ttf-liberation ttf-droid ttf-inconsolata ttf-roboto terminus-font ttf-font-awesome`

#### sound drivers and tools
`sudo pacman -S alsa-utils alsa-plugins alsa-lib pavucontrol`

`lspci -knn | grep -iA2 audio` list audio pci

```
sudo vim /etc/modprobe.d/alsa-base.conf

options snd_hda_intel index=1
```

`reboot`

`speaker-test` audio test

#### extra
`sudo pacman -S alacritty ranger rofi dmenu`

#### Xorg server
`sudo pacman -S xorg-server xorg-xinit`

`sudo pacman -S xorg-apps` 

#### i3 vm
`sudo pacman -S i3`

#### lighhdm
`sudo pacman -S lightdm lightdm-webkit2-greeter`

```
vim /etc/lightdm/lightdm.conf

...
[Seat:*]
...
greater-session = lightdm-webkit2-greeter
...


systemctl enable lightdm.service
systemctl start lightdm.service
reboot

```
