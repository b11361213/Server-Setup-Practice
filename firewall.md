# Firewall
## firewalld
- Based on iptables

- Can be categorized into several `Zones`

`/usr/lib/firewalld/*`: system config

`etc/firewalld/*`: custom config

## Start firewalld service

`systemctl start firewalld`

`systemctl restart firewalld`

`systemctl status firewalld`

---

### firewall-cmd

`firewall-cmd ...`

- **`--reload`**: reload firewall config

- `--state`: get current firewall state

---

- `--get-default-zone`, `--set-default-zone`

- **`--permanent`: let config be permanent**

- **`--get-active-zones`: list all active interface's zone**

---

#### get zone rules, list zone

- `--get-zones`: list avabile zones

- `--list-all`: list zone rules

- `--list-all-zones`: list all zones rules

- **`--zone=<zone>`: specific zone**

- **`--zone=<zone> --change-interface=<interface>`: change interface firewall zone**

---

#### firewall services
- `--get-services`: list all availble services

- `--list-services`: list zone available services

- `--add-service=<service>`

---

#### firewall port
- `--add-port=<port>/[tcp/udp]`

- `--list-ports`

---

#### IP masquerading, port forwarding
- `--add-masquerade`

- `--query-masquerade`

```sh
--add-forward-port= \
port=<port>: \
proto=<protocol>: \

toaddr=<addr>
```
```sh
--add-forward-port= \
port=<port>: \
proto=<proto>: \

toaddr=<addr>: \
toport=<port>:
```
---
add NAT (Network Address Translation) to sub machine
```
$ firewall-cmd --permanent --add-masquerade

$ firewall-cmd --permanent --zone=public --add-source=192.168.1.0/24
$ firewall-cmd --permanent --zone=public --add-source=192.168.2.0/24

$ firewall-cmd --reload
```

---
add DNS service to home zone
```
$ firewall-cmd --permanent --zone=home --add-service=dns
```

---

### systemctl

`systemctl [option]`
- start

- stop

- restart

- reload

- enable

- disable

- status