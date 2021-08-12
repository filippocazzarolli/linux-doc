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

$ cryptsetup -y -u luksFormat /dev/vda2
$ cryptsetup luksOpen /dev/vda2 cryptroot
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

$ ls -sf /usr/share/zonefile/Europe/Rome /etc/localtime
$ hwclock --systohc
$ vim /etc/locale.gen

it_IT.UTF-8

$ locale-gen
$ 
$ 
$ 
$ 
$ 
$ 
$ 
$ 
$ 
$ 
$ 
```



