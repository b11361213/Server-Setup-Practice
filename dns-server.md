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

```