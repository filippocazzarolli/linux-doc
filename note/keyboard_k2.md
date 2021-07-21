## Setup keyboard keycron k2

`
echo "options hid_apple fnmode=0" > /etc/modprobe.d/hid_apple.conf

# this is better for me
echo 0 | sudo tee /sys/module/hid_apple/parameters/fnmode
`


