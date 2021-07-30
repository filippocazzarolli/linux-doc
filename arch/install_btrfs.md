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
$ 
```
