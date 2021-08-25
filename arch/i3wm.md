#### Installing YAY
```
mkdir sources && \
cd sources && \
git clone https://aur.archlinux.org/yay.git && \
cd yay && \
makepkg -si
```
#### Installing YAY
```
sudo pacman -S qemu libvirt edk2-ovmf virt-manager ebtables dnsmasq

sudo systemctl enable libvirtd.service
sudo systemctl start libvirtd.service

sudo systemctl enable virtlogd.socket
sudo systemctl start virtlogd.socket
```

#### Install Drivers
You might find that you need video drivers. Depending on what hardware you are running, install the driver for your system. You might not need these at all. It is possible that your system will work completely OK out of the box.
```
sudo pacman -S nvidia nvidia-utils    # NVIDIA 
sudo pacman -S xf86-video-amdgpu mesa   # AMD
sudo pacman -S xf86-video-intel mesa    # Intel
sudo pacman -S xf86-video-qxl mesa    # virt-manager
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
