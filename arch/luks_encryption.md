# Setup LUKS Encryption on Arch Linux

#### Configuring LUKS Encryption on the Disk
First load kernel module with the following command:
```
modprobe dm-crypt
modprobe dm-mod
```

Now you can encrypt the root partition (in my case /dev/sda3) with LUKS with the following command:
```
cryptsetup luksFormat -v -s 512 -h sha512 /dev/sda3
```

Now open the /dev/sda3 device with the following command, so we can install Arch Linux on it.
```
cryptsetup open /dev/sda3 luks_root
```

#### Formatting and Mounting the Partitions
Run the following command to format the LUKS encrypted root partition /dev/mapper/luks_root:
```
mkfs.ext4 -L root /dev/mapper/luks_root
```
Now mount /dev/mapper/luks_root in /mnt directory:
```
mount /dev/mapper/luks_root /mnt
```

Continue to install arch....
