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

---

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
/dev/myvg_1/mylv_2      /srv/lvm_ext4       xfs         defaults        0 0
```

---

```
mount -a
mount [source_path] [target_path]
control-deamon
```