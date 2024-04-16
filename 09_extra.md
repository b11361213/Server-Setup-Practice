# Extra Content
## System Configuration
### System config
#### systemctl
`systemctl start [service]`  

`systemctl restart [service]`  

`systemctl status [service]`  

`systemctl enable [service]`: default enable service when boot up  

---

`/etc/systemd/system`: when a service is located in this directory, it will be automatically started at boot time (equivalent to systemctl enable [service]).  
`/usr/lib/systemd/system/*.service`: services file

---

installed, using service list:  
```
firewalld ->
named ->
dhcp, dhcrelay, rsyslog
```

---

#### rsyslog
`/etc/rsyslog.conf`: setting the location of log messages  

```
... ;local5.none    /var/log/messages

local5.*        /var/log/dhcrelay.log
```

- `tail -f /var/log/dhcrelay.log`: live monitoring dhcp relay agent log  

---

### Network config
#### nmcli
delete connection
```
nmcli con del [interface]
```

add connection
```
nmcli con add \
type ethernet \
ifname <device> \
con-name <display name> \
autoconnect yes
```

## Useful command
- `ssh`

    - path  
        `/etc/ssh/sshd_config`, `/etc/ssh/ssh_config`  

```
>> it is very easy (o'_'b)

ssh [username] @ [IP address]
```

---

- `scp`
    - local to remote  
    ```
    scp [file] [username] @ [IP address] : /path/to/directory/
    ```

---

- `vim`
    - `:voh`: turn off highlighting  
    [highlight - Vim clear last search highlighting - Stack Overflow](https://stackoverflow.com/questions/657447/vim-clear-last-search-highlighting/657457#657457)

    - `:set nu`: turn on number display

---

- `dnf`  
    - `install`: install packages  
    - `-y`: automatically answer yes for all questions  

---

#### Network config
- [3.3.5. 使用 nmcli 建立和修改連接組態集 Red Hat Enterprise Linux 7 | Red Hat Customer Portal](https://access.redhat.com/documentation/zh-cn/red_hat_enterprise_linux/7/html/networking_guide/sec-creating_and_modifying_a_connection_profile_with_nmcli)
- [nmcli: NetworkManager Reference Manual](https://www.networkmanager.dev/docs/api/latest/nmcli.html#Examples)

#### Useful command
- [如何使用 SCP 安全傳輸檔案和目錄 | D棧 - Delft Stack](https://www.delftstack.com/zh-tw/howto/linux/how-to-securely-transfer-files-and-directories-using-scp/)