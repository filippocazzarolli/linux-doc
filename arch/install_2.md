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
# fdisk /dev/sda
```
| Mount point | Partition | Partition type | Suggested size
| ----------  | --------- | -------------- | --------- 
| /mnt/boot or /mnt/efi |	/dev/efi_system_partition	| EFI system partition |	At least 260 MiB
| [SWAP]| /dev/swap_partition	| Linux swap	| More than 512 MiB (RAM*2)
| /mnt |	/dev/root_partition	| Linux x86-64 root (/)	| Remainder of the device
