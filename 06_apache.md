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

- `mv <phpMyAdmin> /var/www/html/phpMyAdmin`

config.inc.php
```
$cfg['blowfish_secret'] = 'passwd';
```

#### Create Database for phpMyAdmin
Enter mysql shell  
`mysql -u root -p`

Create DB  
`CREATE DATABASE phpmyadmin;`

Create Table  
`mysql -u root -p phpmyadmin < [phpmyadmin/sql/]create_tables.sql`

---

## Apache phpMyAdmin config
`/etc/httpd/conf.d/phpmyadmin.conf`  
```
Alias /phpmyadmin /var/www/html/phpMyAdmin

<Directory /var/www/html/phpMyAdmin>
  AddDefaultCharset UTF-8

  <IfModule mod_authz_core.c>
    <RequireAny>
      Require all granted
    </RequireAny>
  </IfModule>
  
  <IfModule !mod_authz_core.c>
    Order Deny,Allow
    Deny from all
    Allow from 127.0.0.1
  </IfModule>

</Directory>

```

`/etc/httpd/virtualhost.conf`  
```
<VirtualHost *.80>

  ServerAdmin webmaster@s11361213.mcu.edu.tw
  DocumentRoot /var/www/html/phpMyAdmin
  ServerName phpmyadmin.s11361213.mcu.edu.tw
  ErrorLog logs/phpmyadmin-error_log
  CustomLog logs/phpmyadmin-access_log common

</VirtualHost>
```

`/etc/httpd/conf.d/userdir.conf`  
```
UserDir www
```