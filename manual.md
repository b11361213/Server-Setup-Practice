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