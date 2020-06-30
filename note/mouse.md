# Mouse

`xinput list` list the peripherals

`xinput list-props <device>` list for device

`xinput set-prop <device> <number_prop> <val>` set configuration


### Persist setting
```
/etc/X11/xorg.conf.d/90-touchpad.conf

Section "InputClass"
        Identifier "touchpad"
        MatchIsTouchpad "on"
        Driver "libinput"
        Option "Tapping" "on"
        Option "TappingButtonMap" "lrm"
        Option "NaturalScrolling" "on"
        Option "ScrollMethod" "twofinger"
EndSection

```
