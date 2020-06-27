# Install Arch with uefi

#### Network without DHCP
```
ifconfig eno16777736 192.168.1.52 netmask 255.255.255.0 
route add default gw 192.168.1.1
echo “nameserver 8.8.8.8” >> /etc/resolv.conf
```

#### Partition (GPT)
For a basic partition, the layout table uses the following structure.

- EFI System partition (/dev/sda1) with 300M size, FAT32 formatted (*EFI System*).
- Swap partition (/dev/sda2) with 2xRAM recommended size, Swap On (*Linux swap*).
- Root partition (/dev/sda3) with at least 20G size or rest of HDD space, ext4 formatted (*Linux filesystem*).

Now let’s actually start creating disk layout partition table by running cfdisk command against machine hard drive, select **GPT** label type, then select **Free Space** then hit on **New** from the bottom menu.

```
cfdisk /dev/sda
fdisk -l

mkfs.fat -F32 /dev/sda1
mkfs.ext4 /dev/sda3
mkswap /dev/sda2
```

#### Install Arch Linux
```
mount /dev/sda3 /mnt
swapon /dev/sda2
```
To increase installation packages download speed you can edit /etc/pacman.d/mirrorlist file and select the closest mirror website (usually choose your country server location) on top of the mirror file list.
```
vim /etc/pacman.d/mirrorlist
```
You can also enable Arch Multilib support for the live system by uncommenting the following lines from /etc/pacman.conf file.
```
[multilib]
Include = /etc/pacman.d/mirrorlist
```
start installing Arch Linux by issuing the following command
```
pacstrap /mnt base base-devel linux linux-firmware vim
```

Generate fstab file for your new Arch Linux system by issuing the following command
```
genfstab -U -p /mnt >> /mnt/etc/fstab

cat /mnt/etc/fstab
```

#### Arch Linux System Configuration

```
arch-chroot /mnt
echo "LNX-dev" > /etc/hostname
```

configure your system Language
```
pacman -S vim
vim /etc/locale.gen
locale-gen
ln -s /usr/share/zoneinfo/Aisa/Kolkata /etc/localtime
hwclock --systohc --utc
passwd
```


#### Network
```
pacman -S wpa_supplicant
pacman -S wireless_tools
pacman -S networkmanager

systemctl enable NetworkManager.service
systemctl enable wpa_supplicant.service
systemctl start NetworkManager.service
systemctl start wpa_supplicant.service
```


#### Boot loader
To install the GRUB boot loader in UEFI machines on the first hard-disk and also detect Arch Linux and configure the GRUB boot loader file, run the following commands as illustrated in the following screenshots.
```
pacman -S grub efibootmgr

mkdir /boot/efi
mount /dev/sda1 /boot/efi

grup-install --target=x86_64-efi --bootloader-id=GRUB --efi-directory=/boot/efi
grub-mkconfig -o /boot/grub/grub.cfg

mkdir /boot/efi/EFI/BOOT
cp /boot/efi/EFI/GRUB/grubx64.efi /boot/efi/EFI/BOOT/BOOTX64.EFI

echo "bcf boot add 1 fs0:\EFI\GRUB\grubx64.efi \"My GRUB bootloader\"" > /boot/efi/startup.nsh
echo "exit" > /boot/efi/startup.nsh

```

#### Finish
```
exit
umount -R /mnt
reboot
```
