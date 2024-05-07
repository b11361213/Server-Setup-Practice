# Samba Server
`dnf install -y samba samba-client`

`systemctl status smb`

`/etc/samba/smb.conf`
```
[global]
        workgroup = mcu
        security = user

        netbios name = s1

[temp]
        path = /tmp
        browseable = yes
        writeable = yes
        guest ok = yes
```

- `testparm`

---

## Samba account
`smbpasswd -a s1-guest`  

`smbclient -L //127.0.0.1`  

`smbclient //192.168.1.1 -U s1-guest`  