# Server-Setup-Practice
36363-36465開源網路伺服器架設實務 

## Architecture Diagram

```mermaid
flowchart RL
    net-1 <-- DHCP relay \n DNS query --> router-n1
    router-n1 -- DHCP request --> S1
    net-2 <-- DHCP relay <br> DNS query --> router-n2
    bridge-1 <--> router-b0

    bridge-1(
        bridge)
    
    subgraph router-0
    router(
        DNS, DHCP Relay
        cent router)
    router-b0(
        enp0s3
        FW public
        bridge-0)
    router-n1(
        enp0s8
        FW home
        net-1)
    router-n2(
        enp0s9
        FW home
        net-2)
    router-b0 <--> router
    router-n1 <--> router <--> router-n2
    end
    
    subgraph net-1
    S1(
        DHCP, vsFTPd
        S1)
    C1(
        C1)
    end

    subgraph net-2
    S2(
        Apache
        S2)
    C2(
        C2)
    end
```

## Service list
| Host | Service | Service name |
| -- |-- | -- |
| Router | Firewall, DNS, DHCP Relay | `firewalld`, `named`, `dhcrelay` |`
| S1 | DHCP vsFTPd | `dhcpd` `vsftpd` |
| S2 | Apache, PHP, MariaDB | `httpd`, `php-fpm`, `mariadb` |
| C1 | None (client) | |
| C2 | None (client) | |
