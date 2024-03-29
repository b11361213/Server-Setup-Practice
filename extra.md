# Extra Content
## System Configuration
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

#### Network config
- [3.3.5. 使用 nmcli 建立和修改連接組態集 Red Hat Enterprise Linux 7 | Red Hat Customer Portal](https://access.redhat.com/documentation/zh-cn/red_hat_enterprise_linux/7/html/networking_guide/sec-creating_and_modifying_a_connection_profile_with_nmcli)
- [nmcli: NetworkManager Reference Manual](https://www.networkmanager.dev/docs/api/latest/nmcli.html#Examples)

#### Useful command
- [如何使用 SCP 安全傳輸檔案和目錄 | D棧 - Delft Stack](https://www.delftstack.com/zh-tw/howto/linux/how-to-securely-transfer-files-and-directories-using-scp/)