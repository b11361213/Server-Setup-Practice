# iSCSI
## Install iSCSI
`dnf install -y targetcli`

```
$ mkdir /var/targetdisk_1

$ targetcli

$ cd /backstores/fileio
$ create targetdisk /var/targetdisk_1/targetdisk_1.img 5G

$ cd /iscsi
$ create iqn.2024-06.s11361213.mcu.edu.tw:target_1

$ cd iqn.2024-06.s11361213.mcu.edu.tw:target_1/tpg1/luns
$ create /backstores/fileio/targetdisk_2

```

鳥哥私房菜 - 第十八章、網路磁碟裝置： iSCSI 伺服器  
https://linux.vbird.org/linux_server/centos6/0460iscsi.php