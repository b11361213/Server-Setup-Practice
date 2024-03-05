# Additional Guest Setup Manual
## Install Kernal
`dnf install epel-release -y`

`dnf update --refresh -y`

```sh
dnf install dkms kernel-devel kernel-headers \
    gcc make bzip2 perl \
    elfutils-libelf-devel
```

`rpm -q kernel-devel`: get installed kernal version

`uname -r`: get current running kernel version


---

`df -h`: check disk mount info

`/run/media/<>/VBox_GA... .run`