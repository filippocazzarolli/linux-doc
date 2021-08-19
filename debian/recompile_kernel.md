# Recompile kernel on Debian 11

```
$ wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.13.12.tar.xz
$ mkdir linux_kernel
$ tar xvf linux-* -C linux_kernel/ --strip-components=1
$
$ cd linux_kernel/
$ sudo apt install build-essential rsync gcc bc bison flex libssl-dev libncurses5-dev libefl-all-dev
$ 
$ cp /boot/config-$(uname -r) ./.config
$ 
$ make localmdconfig   <-- y/n
$ make menuconfig      <-- menu
$ 
$ make -j2 deb-pkg                <-- non funziona
$ fakeroot sudo make -j4 deb-pkg  <-- ???
$ 
$ cd ..
$ sudo dpkg -i linux-*.deb
$ 
$ 
```
