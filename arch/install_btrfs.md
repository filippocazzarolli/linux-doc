# Install Arch with BTRFS


```
$ timedatectl set-ntp true
$
$ reflector -c Italy -a 6 --sort rate --save /etc/pacman.d/mirrorlist
$ pacman -Syy
$
$ gdisk /dev/vda

# boot partition
n
<enter>
<enter>
+300M
ef00

# swap partition
n
<enter>
<enter>
+2G
8200

# os
n
<enter>
<enter>
<enter>
<enter>

w

$ 
$ mkfs.fat -F32 /dev/vda1
$
$ mkswap /dev/vda2
$ swapon /dev/vda2
$ 
$ mkfs.btrfs /dev/vda3
$ 
$ mount /dev/vda3 /mnt
$ btrfs su cr /mnt/@
$ btrfs su cr /mnt/@home
$ btrfs su cr /mnt/@snapshots
$ btrfs su cr /mnt/@var_log
$ umount /mnt
$ mount -o noatime,compress=lzo,space_cache=v2,subvol=@ /dev/vda3 /mnt
$ mkdir -p /mnt/{boot,home,.snapshots,var_log}
$ mount -o noatime,compress=lzo,space_cache=v2,subvol=@home /dev/vda3 /mnt/home
$ mount -o noatime,compress=lzo,space_cache=v2,subvol=@snapshots /dev/vda3 /mnt/.snapshots
$ mount -o noatime,compress=lzo,space_cache=v2,subvol=@var_log /dev/vda3 /mnt/var_log
$ mount /dev/vda1 /mnt/boot
$ 
$ pacstrap /mnt base linux linux-firmware vim intel-ucode
$ 
$ genfstab -U /mnt >> /mnt/etc/fstab
$ 
$ arch-chroot /mnt
$ 
$ ln -sf /usr/share/zoneinfo/Europe/Rome /etc/localtime
$ hwclock --systohc
$ vim /etc/locale.gen
$ locale-gen
$ echo "LANG=en_US.UTF-8" > /etc/locale.conf
$ 
$ echo "arch-btrfs" > /etc/hostname
$ 
$ vim /etc/hosts

127.0.0.1	localhost
127.0.1.1	arch-btrfs.localdomain	arch-brtfs

$ 
$ passwd
$ 
$ pacman -S grub efibootmgr networkmanager network-manager-applet dialog wpa_supplicant mtools dosfstools git reflector snapper bluez bluez-utils cups xdg-utils xdg-user-dirs alsa-utils pulseaudio pulseaudio-bluetooth base-devel linux-headers
$ 
$ vim /etc/mkinitcpio.conf

MODULES=(btrfs)

$
$ mkinitcpio -p linux
$ 
$ grub-install --target=/x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
$ grub-mkconfig -o /boot/grub/grub.cfg
$ 
$ systemctl enable NetworkManager
$ systemctl enable bluetooth
$ systemctl enable cups
$ 
$ useradd -mG wheel filippo
$ passwd filippo
$ 
$ EDITOR=vim visudo

# uncomment this line
%wheel ALL=(ALL) ALL

$ 
$ pacman -S bash-completion
$ exit
$ umount -a
$ reboot
$ 
$ sudo umount /.snapshots
$ sudo snapper -c root create-config /
$ sudo btrfs subvolume delete /.snapshots
$ sudo mkdir /.snapshots
$ sudo mkdir /.snapshots
$ sudo chmod 750 /.snapshots
$ sudo vim /etc/snapper/configs/root

# users and groups allowed to work with config
ALLOW_USERS="filippo"

# limits for timeline cleanup
TIMELINE_MIN_AGE="1800"
TIMELINE_LIMIT_HOURLY="5"
TIMELINE_LIMIT_DAILY="7"
TIMELINE_LIMIT_WEEKLY="0"
TIMELINE_LIMIT_MONTHLY="0"
TIMELINE_LIMIT_YEARLY="0"

$ sudo systemctl enable --now snapper-timeline.timer
$ sudo systemctl enable --now snapper-cleanup.timer
$ 
$ 
$ 
$ 
$ 
$ 
$ 
$  
```
