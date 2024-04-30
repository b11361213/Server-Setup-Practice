# vsFTPd FTP Server
`dnf install -y vsftpd`

`/etc/vsptpd/`: vsftpd config  

## Config vsFTPd
`/etc/vsftpd/vsftpd.conf`
```
listen=YES
=> start as standalone mode
# listen_ipv6=YES
```

## Login FTP from remote
other PC
```
ftp <remote FTP IP>

Enter Name(remote username)
Enter Password(remote user pwd)
```

### FTP Command
- `open <remote IP>` reconnect to ftp