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

$ 
```



