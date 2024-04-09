# Server-Setup-Pratice
36363-36465開源網路伺服器架設實務 

## Structure Diagram

```mermaid
flowchart RL
    net-1 <-- DHCP relay \n DNS query --> router-n1
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
        bridge-0)
    router-n1(
        enp0s8
        net-1)
    router-n2(
        enp0s9
        net-2)
    router-b0 <--> router
    router-n1 <--> router <--> router-n2
    end
    
    subgraph net-1
    S1(
        DHCP
        S1)
    C1(
        C1)
    end

    subgraph net-2
    S2(
        S2)
    C2(
        C2)
    end
```

## Service list
| Host | Service | Service name |
| -- |-- | -- |
| Router | DNS, DHCP Relay | `named`, `dhcrelay` |`
| S1 | DHCP | `dhcpd` |
| S2 | | |
| C1 | | |
| C2 | | |
