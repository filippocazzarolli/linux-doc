# Install arch - luks


```
$ pacman -Syy reflector
$ reflector -c Italy -a 6 --sort rate --save /etc/pacman.d/mirrorlist
$ gdisk /dev/vda
n
<enter>
<enter>
+300M
ef00
n
<enter>
<enter>
<enter>
<enter>
w

$ cryptsetup -y -v luksFormat /dev/vda2
$ cryptsetup open /dev/vda2 cryptroot
$ mkfs.ext4 /dev/mapper/cryptroot
$ mkfs.fat -F32 /dev/vda1
$ 
$ mount /dev/mapper/cryptroot /mnt
$ mkdir /mnt/boot
$ mount /dev/vda1 /mnt/boot
$ 
$ pacstrap /mnt base linux linux-firmware vim intel-ucode
$ 
$ genfstab -U /mnt >> /mnt/etc/fstab
$ arch-chroot /mnt
$ 
$ fallocate -l 32GB /swapfile
$ chmod 600 /swapfile
$ mkswap /swapfile
$ swapon /swapfile
$ 
$ vim /etc/fstab

/swapfile none swap defaults 0 0 

$ ln -sf /usr/share/zonefile/Europe/Rome /etc/localtime
$ hwclock --systohc
$ vim /etc/locale.gen

it_IT.UTF-8

$ locale-gen
$ 
$ echo LANG=it_IT.UTF-8 >> /etc/locale.conf
$
$ echo "fc-work-desktop" > /etc/hostname
$ 
$ vim /etc/hosts
127.0.0.1      localhost
::1            localhost
127.0.1.1      fc-work-desktop.localdomain fc-work-desktop

$ 
$ passwd
$ 
$ pacman -S grub efibootmgr networkmanager network-manager-applet wireless_tools wpa_supplicant dialog os-prober mtools dosfstools base-devel linux-header reflector git bluez bluez-utils pulseaudio-bluetooth cups xdg-utils xdg-user-dirs
$ 
$ vim /etc/mkinitcpio.conf

HOOKS=(base udev autodetect modconf block encrypt ...)

$ mkinitcpio -p linux
$ 
$ grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
$ grub-mkconfig -o /boot/grub/grub.cfg
$ blkid <--- get id of crupt, insert into grub configuration 
$ vim /etc/default/grub

GRUB_CMDLINE_LINUX="cryptdevice=UUID=<UUID>:cryptroot root=/dev/mapper/cryptroot"

$ grub-mkconfig -o /boot/grub/grub.cfg
$ 
$ pacman -S bash-completion
$ 
$ systemctl enable NetwokManager
$ systemctl enable bluetooth
$ systemctl enable org.cup.cupsd
$ 
$ useradd -mG wheel filippo
$ passwd filippo
$ 
$ EDITOR=vim visudo

%wheel ALL=(ALL) ALL

$ exit
$ umount -a
$ reboot
$
$ git clone https://aur.archlinux.org/yay.git
$ cd yay
$ makepkg -si PKBUILD
$ 
$ 
$ sudo pacman -S xf86-video-intel
$ sudo pacman -S xf86-video-amdgpu
$ sudo pacman -S nvidia nvidia-utils nvidia-settings
```



