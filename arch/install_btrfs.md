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
$ 
$ 
$ 
$ 
$ 
$ 
```
