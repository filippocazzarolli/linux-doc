# Install Arch with uefi and encrypt

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


