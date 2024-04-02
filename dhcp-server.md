# DHCP Server
## Install bind, bind-utils
`dnf install dhcp-server`  

`/etc/dhcp/dhcpd.conf`  
```
# example file at: /usr/share/doc/dhcp-server/dhcpd.conf.example

option domain-name          "s11361213";

subnet 192.168.1.0      netmask     255.255.255.0   {
    option routers                  192.168.1.254;
    optoin domain-name-servers      192.168.1.254;

    range   192.168.1.101   192.168.1.150;
}

subnet 192.168.2.0      netmask     255.255.255.0   {
    option routers                  192.168.2.254;
    optoin domain-name-servers      192.168.2.254;

    range   192.168.2.101   192.168.2.150;
}
```