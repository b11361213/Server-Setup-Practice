# Firewall
## firewalld
- Based on iptables

- Can be categorized into several `Zones`

`/usr/lib/firewalld/*`: system config

`etc/firewalld/*`: custom config

## Start firewalld service

`systemctl start firewalld`

`systemctl status firewalld`

### firewall-cmd

`firewall-cmd ...`

#### get interface zone
- `--state`: get current firewall state

- `--get-default-zone`

- **`--get-active-zones`**: list all active interface's zone

---

#### get zone rules, list zone
- `--get-zones`: list avabile zones

- `--zone=<zone> --list-all`: list specific zone rules

- `--list-all-zones`: list all zones rules

---

#### change interface firewall zone
- **`--zone=<zone> --change-interface=<interface>`**

### systemctl

`systemctl [option]`
- start

- stop

- restart

- reload

- enable

- disable

- status