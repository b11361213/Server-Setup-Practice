# Apache HTTP Server
## install httpd, httpd-tools
`dnf install -y httpd httpd-tools`

`systemctl enable httpd`

`/var/www/html/`

---

`curl localhost | head -15`  
`curl www.s11361213.mcu.edu.tw | head -15`

---

## Config firewall on router
### Add service
```
firewall-cmd --permanent --zone=public --add-service=http
firewall-cmd --permanent --zone=public --add-service=https
```

---

### Config port forward
```
firewall-cmd --permanent --zone=public --add-forward-port=\
port=80:\
proto=tcp:\

toaddr=192.168.2.1:\
toport=80
```

---

### Config VBox port forward
```
router --> Interface 1 --> NAT -->
Port forwarding -->
```
| Neme | Protocol | Host IP | Host Port | Client IP | Cilent Port |
| -- | -- | -- | -- | -- | -- |
| http | TCp | 127.0.0.1 | 80 | 10.0.2.15 | 80 |

---

### Install PHP
```
dnf install php php-fpm php-mysqlnd php-opcache \
php-gd php-ldap php-odbc php-pear php-xml php-mbstring \
php-snmp php-soap curl curl-devel
```

#### Test PHP
`/var/www/html/info.php`
```php
<?php
phpinfo();
>
```

---

### Install MariaDB
`dnf install mariadb-server mariadb`
`mysql_secure_installation`

#### Test MariaDB
`mysql -u root -p`

---

### Install phpMyAdmin
- wget [phpmyadmin](https://www.phpmyadmin.net/files/)

- `tar -vxzf <phpMyAdmin>.tar.gz`

- `mv <phpMyAdmin> /usr/share/phpmyadmin/`
