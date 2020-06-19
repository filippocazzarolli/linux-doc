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
