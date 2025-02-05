---
title: ubuntu(debain) Apache2多端口部署
tags:
 - Linux
 - Apache2
categories:
 - 服务器部署
---

Linux Apache2多端口部署

<!-- more -->

### Linux Apache2多端口部署

#### 安装Apache2

```bash
sudo apt update
sudo apt install apache2
```

#### 找到ports.conf文件

```bash
cd /etc/apache2
ls
```

```bash
root@nine:~# cd /etc/apache2/
root@nine:/etc/apache2# ls
apache2.conf    conf-enabled  magic           mods-enabled  sites-available
conf-available  envvars       mods-available  ports.conf    sites-enabled
```

#### 编辑ports.conf文件

```bash
vim ports.conf
```

#### 添加端口，如下

```bash
# If you just change the port or add more ports here, you will likely also
# have to change the VirtualHost statement in
# /etc/apache2/sites-enabled/000-default.conf

# sports-memory
Listen 23106
# blog
Listen 23107
# wprdpress
Listen 23108

<IfModule ssl_module>
        Listen 443
</IfModule>

<IfModule mod_gnutls.c>
        Listen 443
</IfModule>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
~                                                                                                           ~     
```

添加后，保存退出（`:wq`）

#### 添加站点（sites.available）

```bash
cd sites-available/
```

```bash
root@nine:/etc/apache2# cd sites-available/
root@nine:/etc/apache2/sites-available# ls
000-default.conf  default-ssl.conf
```

编辑站点

```bash
 vim 000-default.conf
```

```bash
<VirtualHost *:23106>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

<VirtualHost *:23107>
        ServerAdmin webmaster2@localhost
        DocumentRoot /var/www/blog/dist
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

<VirtualHost *:23108>
        ServerAdmin webmaster3@localhost
        DocumentRoot /var/www/wordpress
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
编辑完成后，保存退出（`:wq`）

#### 重启Apache2服务

```bash
systemctl restart apache2
```

#### 卸载apache2
```
apt remove apache2
```

