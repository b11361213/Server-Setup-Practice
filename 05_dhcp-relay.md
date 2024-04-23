# DHCP Relay
## Install DHCP relay
`dnf install dhcp-relay`  

## Config DHCP relay
cp `/usr/lib/systemd/system/dhcrelay.service` to `/etc/systemd/system/`  

```
ExecStart=... 192.168.1.1
# -> dhcp server location

StandardError=journal
# send error msg to /var/log/messages

StandardOutput=journal
# send output msg to /var/log/messages

SyslogFacility=local5
# set log source name
```