# Environment Setup Manual

## Environment list

### Router
- Hostname  
`router.s11361213.mcu.edu.tw`
- Network interface
```
## 01
Method: auto(DHCP)
---

## 02
Method: manual
IP: 192.168.1.254
Netmask: /24
---

## 03
Method: manual
IP: 192.168.2.254
Netmask: /24
---
```
- User  
`router-guest`, `root`
- Locale, Timezone
`en_US`, `Asia/Taipei`
---

### S1
- Network interface
```
## 01
Method: manual
IP: 192.168.1.1
Default Gateway: 192.168.1.254
Netmask: /24
---
```
- User  
`s1-guest`, `root`
- Locale, Timezone
`en_US`, `Asia/Taipei`
---

### S2
- Network interface
```
## 01
Method: manual
IP: 192.168.2.1
Default Gateway: 192.168.2.254
Netmask: /24
---
```
- User  
`s2-guest`, `root`
- Locale, Timezone
`en_US`, `Asia/Taipei`
---

## VirtualBox Setup Manual
```
Machine name: router-guest, s1-guest, s2-guest
ISO image: Rocky-Linux-9.3-x86-64-dvd

Memory: 1024MB (1GB)
CPU: 1

Hard disk: 100GB (Don't Pre-allocate Full Size)
```
---

### Machine setting
- Network
    - router
    ```
    Interface 1:
    NAT

    Interface 2, 3:
    Internal Network
    ```
    - S1, S2
    ```
    Interface 1:
    Internal Network
    ```
---

## Linux Configuration

### Interface config
`ifconfig [interface]`: check network interface  

`nmcli device`: check network devices  

`nmcli connection`: check network connection status  

- `nmcli connection modify <interface> >`
```
nmcli connection modify enp0s3 \
ipv4.address 192.168.1.1/24 \
ipv4.gateway 192.168.1.254 \
ipv4.method manual
```

- `nmcli connection show <interface> | grep ipv4`

- config location: `/etc/NetworkManager/system-connections/<interface>.nmconnectoin`

---

### Hostname config
`hostnamectl`: get hostname info

`hostname <hostname>`: get, set hostname

---

### System config


---

## Useful Command
| Keyboard Shortcut | Description |
| -- | -- |
| `Alt` + `F1`, `F2`... | Switch virtual console |
| `Alt` + `Right` | Switch to previous console |
| `Alt` + `Left` | Switch to next console |
| `Ctrl` + `Z` | Pauses current task |
| `Ctrl` + `C` | Kills current task |

---

| Keyboard Shortcut | Description |
| -- | -- |
| `vim` | Open vim editor |
| `cat` | Print text file content |
| `echo >` | Overwrite content to file |
| `echo >>` | Append content to file |
| `grep <keyword>` | Filter output |
| `more` | |
| `less` | |

---

#### Console command
- [Linux console - ArchWiki](https://wiki.archlinux.org/title/Linux_console)

#### Network command
- [鳥哥私房菜 - 第五章、建立與檢查網路連線 | 5.2.1、固定網路參數設定方式(manual)](https://linux.vbird.org/linux_server/rocky9/0160setnetwork.php#5.2.1)
- [nmcli 修改網卡設定](https://dywang.csie.cyut.edu.tw/dywang/rhel7/node21.html)