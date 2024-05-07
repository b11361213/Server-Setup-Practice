# NFS Server
`dnf install -y rpcbind nfs-utils`

## Config NFS
`etc/exports`

```
/tmp  *(rw,no_root_squash)
```

---

`systemctl start nfs-server`

- `exportfs -arv`: export fs

- `exportfs -s`: show exported fs

- on client  
`showmount -e <host IP>`

add mount
```
mkdir -p /mnt/tmp

mount -t nfs 192.168.1.1:/tmp /mnt/tmp
```

check mount  
`mount | grep nfs`