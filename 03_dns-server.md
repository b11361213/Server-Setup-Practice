# DNS Server
## Install bind, bind-utils
`dnf install bind bind-utils`

## Setup config & log file
### Config file
`/etc/named.conf`

### Root domain config
`/var/named.ca`

### Forward Lookup (正解, domain -> IP)
`/var/named.localhost`

### Reverse Lookup (反解, IP -> domain)
`/var/named.loopback`

### Custom Lookup
For specific domain forward lookup, or for specific IP reverse lookup

ex `domain A, B, C...` or IP `123.55.66.*`

---

`/var/named.<full domain name>`

`/var/named.s11361213.mcu.edu.tw`
```
; Record retention time in the cache
$TTL 86400

; [Domain Name]             [Network Class Type]    [Record Type]           [Record source]                     [Owner Mail]
s11361213.mcu.edu.tw.               IN                  SOA             dns.s11361213.mcu.edu.tw.       sysop.s11361213.mcu.edu.tw. ( ... )

s11361213.mcu.edu.tw.               IN                  NS              dns.s11361213.mcu.edu.tw.

dns                                 IN                  A               192.168.1.254
dns                                 IN                  A               192.168.2.254
router                              IN                  CNAME           dns

s11361213.mcu.edu.tw.               IN                  MX              10          dns
mail                                IN                  CNAME           router

s1                                  IN                  A               192.168.1.1
s2                                  IN                  A               192.168.2.1

www                                 IN                  A               192.168.2.1
phpmyadmin                          IN                  A               192.168.2.1

```

---

`/var/named.s11361213.mcu.edu.tw`
```
$TTL 3H

; [Domain Name]             [Network Class Type]    [Record Type]           [Record source]                     [Owner Mail]
@       IN      SOA     s1.s11361213.mcu.edu.tw.        sysop.s11361213.mcu.edu.tw.     (
                        20240319 ; Serial number
                        1D ; Refresh time
                        1H ; Retry time
                        1W ; Expire time
                        3H ) ; Minimum

        IN      NS      dns.s11361213.mcu.edu.tw.
1       IN      PTR     s1
254     IN      PTR     dns
254     IN      PTR     router

```

---

`/etc/named.conf` add
```
zone "s11361213.mcu.edu.tw" IN {
    type master;
    file "named.s11361213.mcu.edu.tw";
};

zone "1.168.192.in-addr-arpa" IN {
    type master;
    file "named.192.168.1";
};

zone "2.168.192.in-addr-arpa" IN {
    type master;
    file "named.192.168.2";
};
```

## Check config files & config status
### Check config files
`named-checkzone s11361213.mcu.edu.tw /var/named/named.s11361213.mcu.edu.tw`

`named-checkzone 192.168.1 /var/named/named.192.168.1`

`named-checkzone 192.168.2 /var/named/named.192.168.2`

### Check config status
- on router
```
$ nslookup

> server 127.0.0.1
> s1.s11361213.mcu.edu.tw
> s2.s11361213.mcu.edu.tw

> 192.168.1.1
> 192.168.2.1
```

### Check current DNS server
- add DNS server on client
```
nmcli con mod enp0s3 \
ipv4.dns 192.168.1.254
```

- DNS server record
`/etc/resolv.conf`