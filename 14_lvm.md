# LVM
- Physical Volume (PV)
- Volume Group (VG)
- Logical Volume (LG)

```
PV + PV... ==> VG
VG ==> LG + LG...
```

---

## Commands
#### `df -h`
#### `lsblk`: show disk info
#### `gdisk`: create disk partition
- `p`: show partitoin
- `n`: create partition
- `w`: save changes
- `d`: delete partition

disk location 
`/dev/sd...`

```
mount [source_path] [target_path]
```

---

## LVM usage
### LVM create PV, VG, LV

Use gdisk create 4 section
```
$ gdisk /dev/sdb
> n
> (partition num): default
> (start): default
> (end): +300M
> (disk type GUID): 8e00 (Linux LVM)
```

Create PV
```
$ pvcreate /dev/sdb{1..4}
$ pvdisplay / pvscan
```

Create VG
```
$ vgcreate -s 16M myvg_1 /dev/sdb{1..4}
$ vgdisplay / vgscan
```

Create LV
```
$ lvcreate -L 500M -n mylv_1 myvg_1
$ lvdisplay /dev/myvg_1/mylv_1
```
```
$ mkfs.xfs /dev/myvg_1/mylv_1
$ mkdir /srv/lvm
$ vim /etc/fstab
```
`/etc/fstab`
```
/dev/myvg_1/mylv_1      /srv/lvm        xfs         defaults        0 0
```

---

### Create LVM ext4 disk
```
$ lvcreate -L 300M -n mylv_2 myvg_1
$ mkfs.ext4 /dev/myvg_1/mylv_2
$ mkdir /srv/lvm_ext4
$ vim /etc/fstab
```
`/etc/fstab`
```
/dev/myvg_1/mylvm_2         /srv/lvm_ext4       ext4        defaults        0 0
```
```
mount -a
systemctl daemon-reload
```

---

### LV resize add volume
```
$ lvscan
$ vgdisplay myvg_1
$ lvresize -l +21 /dev/myvg_1/mylv_2
$ resize2fs /dev/myvg_1/mylv_2
```

### LV resize reduce volume
```
lvreduce --resizefs -L 256M /dev/myvg_1/mylv_2
```

---

### Extend VG size
```
$ gdisk /dev/sdc
+500M
8e00

$ pvcreate /dev/sdc1
$ vgextend myvg_1 /dev/sdc1
$ vgdisplay myvg_1
```

---

### Disable and remove LVM
1. `/etc/fstab`: comment or delete auto mount record
2. umount `/srv/lvm`
3. `vgchange --activate n myvg_1`, and `lvscan` confirm that the VG has been deactivated
4. `vgremove myvg_1`
6. `pvscan`, `pvremove /dev/sdb{1..4}`