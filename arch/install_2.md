# Install Arch with uefi

#### Verify the boot mode
To verify the boot mode, list the efivars directory:
```
# ls /sys/firmware/efi/efivars
```
If the command shows the directory without error, then the system is booted in UEFI mode. If the directory does not exist, the system may be booted in BIOS (or CSM) mode. If the system did not boot in the mode you desired, refer to your motherboard's manual.

#### Verify the boot mode
Use timedatectl(1) to ensure the system clock is accurate:
```
# timedatectl set-ntp true
```
To check the service status, use timedatectl status.

#### Partition the disks
When recognized by the live system, disks are assigned to a block device such as /dev/sda, /dev/nvme0n1 or /dev/mmcblk0. To identify these devices, use lsblk or fdisk.
```
# fdisk -l
```
**Example layouts**
|partition number | Mount point | Partition | Partition type | Suggested size
| ---- | ----------  | --------- | -------------- | --------- 
| 1 | /mnt/boot or /mnt/efi |	/dev/efi_system_partition	| EFI system partition |	At least 260 MiB
| 2 | [SWAP]| /dev/swap_partition	| Linux swap	| More than 512 MiB (RAM*2)
| 3 | /mnt |	/dev/root_partition	| Linux x86-64 root (/)	| Remainder of the device

```
# fdisk /dev/sda
#
# (init GPT)
# g (create GPT disklabel)
#
# (EFI partition)
# n (new partition)
# 1 (partition number)
# <default> (first sector)
# +550M (last sector)
#
# (SWAP partition)
# n (new partition)
# 2 (partition number)
# <default> (first sector)
# +4096M (last sector)
#
# (/ partition)
# n (new partition)
# 3 (partition number)
# <default> (first sector)
# <default> (last sector)
#
# (partition type)
# t (partition efi)
# 1 (partion number)
# 1 (EFI System)
#
# t (partition swap)
# 2 (partion number)
# 19 (SWAP Linux)
# 
# w (write table)
```

#### Format the partitions
Once the partitions have been created, each newly created partition must be formatted with an appropriate file system. 
```
# (format efi partition)
# mkfs.fat -F32 /dev/sda1
#
# (swap partition)
# swapon /dev/sda2
# 
# (format root partition)
# mkfs.ext4 /dev/sda3
```

#### Mount the file systems
Mount the root volume to /mnt. For example, if the root volume is /dev/root_partition:
```
# mount /dev/sda3 /mnt
```
Create any remaining mount points (such as /mnt/efi) using mkdir(1) and mount their corresponding volumes.
If you created a swap volume, enable it with swapon(8):
```
# swapon /dev/sda2
```

#### Install essential packages
Use the pacstrap(8) script to install the base package, Linux kernel and firmware for common hardware:
```
# pacstrap /mnt base linux linux-firmware vim
```

#### Fstab
Generate an fstab file (use -U or -L to define by UUID or labels, respectively):
```
# genfstab -U /mnt >> /mnt/etc/fstab
```
Check the resulting /mnt/etc/fstab file, and edit it in case of errors.

#### Chroot
Change root into the new system:
```
# arch-chroot /mnt
```

#### Time zone
Set the time zone:
```
# ln -sf /usr/share/zoneinfo/Europe/Rome /etc/localtime
```
Run hwclock(8) to generate /etc/adjtime:
```
# hwclock --systohc
```
This command assumes the hardware clock is set to UTC. See System time#Time standard for details.

#### Localization
Edit /etc/locale.gen and uncomment en_US.UTF-8 UTF-8 and other needed locales. Generate the locales by running:
```
# locale-gen
```
Create the locale.conf(5) file, and set the LANG variable accordingly:
```
echo LANG=en_US.UTF-8 > /etc/locale.conf
export LANG=en_US.UTF-8
```

#### Network configuration
Create the hostname file:
```
/etc/hostname
myhostname
```
Add matching entries to hosts(5):
```
/etc/hosts
127.0.0.1	localhost
::1		localhost
127.0.1.1	myhostname.localdomain	myhostname
```
If the system has a permanent IP address, it should be used instead of 127.0.1.1.
Complete the network configuration for the newly installed environment, that may include installing suitable network management software.

#### Root password
Set the root password:
```
# passwd
```

#### Add user and sudo
```
# useradd -m filippo
# passwd filippo
# usermod -aG wheel
# pacman -S sudo
```

#### Grub
```
# pacman -S grub 
# pacman -S efibootmgr dosfstools os-prober mtools
#
# mkdir /boot/EFI
# mount /dev/sda1 /boot/EFI
# grub-install --target=

```


