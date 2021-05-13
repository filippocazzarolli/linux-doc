## Configurare openvpn on arch

PS: mtu 1500 <--- si blocca tutto e non crea le regole di routing in maniera corretta


```
sudo pacman -Sy openvpn
pacman -Sy networkmanager-openvpn

nmcli connection import type openvpn file </etc/openvpn/client/file.ovpn>

nmcli connection modify aws-atena vpn.user-name <username>

nmcli connection up aws-atena --ask
```

