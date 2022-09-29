Self-hosted [[git]] server

* https://docs.gitea.io/en-us/database-prep/
* https://docs.gitea.io/en-us/install-from-binary/
* https://computingforgeeks.com/install-gitea-git-service-on-debian-10-buster/
* https://blog.smoha.org/201810-gitea-nginx-lets-encrypt

# Setup on [[Debian]]
assuming you are already root...

## Install necessary packages
```shell
apt update && \
apt install -y \
  git \
  gpg \
  mariadb-server \
  nginx
```

## make user

```bash
adduser \
   --system \
   --shell /bin/bash \
   --gecos 'Gitea Server' \
   --group \
   --disabled-password \
   --home /home/gitea \
   gitea
```

## Create directories

```sh
mkdir -p /var/lib/gitea/{custom,data,log}
chown -R gitea:gitea /var/lib/gitea/
chmod -R 750 /var/lib/gitea/
mkdir /etc/gitea
chown root:gitea /etc/gitea
chmod 770 /etc/gitea
```

## Get the Binary

* wget the correct release & .asc file from the downloads page: 
	* https://dl.gitea.io/gitea/
* verify gpg key
```shell
gpg --keyserver keys.openpgp.org --recv 7C9E68152594688862D62AF62D9AE806EC1592E2
pg --verify gitea-1.17.1-linux-amd64.asc gitea-1.17.1-linux-amd64
```
* copy binary
```shell
cp gitea-1.17.2-linux-amd64 /usr/local/bin/gitea
```

It should asy something like `Good signature from Teabot` even if it has other warnings

## Create database

Do basic security stuff
```bash
mysql_secure_installation
```

Open sql prompt
```shell
mysql -u root -p
```

Make database user, replacing password as appropriate
```sql
SET old_passwords=0;
CREATE USER 'gitea' IDENTIFIED BY '<PASSWORD>';
```

Create and configure database
```SQL
CREATE DATABASE giteadb CHARACTER SET 'utf8mb4' COLLATE 'utf8mb4_unicode_ci';
GRANT ALL PRIVILEGES ON giteadb.* TO 'gitea';
FLUSH PRIVILEGES;
```

## Create service
create `/etc/systemd/system/gitea.service`:

```ini
[Unit]
Description=Gitea (Git with a cup of tea)
After=syslog.target
After=network.target
Wants=mariadb.service
After=mariadb.service
#Wants=memcached.service
#After=memcached.service
#Wants=redis.service
#After=redis.service
#
###
# If using socket activation for main http/s
###
#
#After=gitea.main.socket
#Requires=gitea.main.socket
#
###
# (You can also provide gitea an http fallback and/or ssh socket too)
#
# An example of /etc/systemd/system/gitea.main.socket
###
##
## [Unit]
## Description=Gitea Web Socket
## PartOf=gitea.service
##
## [Socket]
## Service=gitea.service
## ListenStream=<some_port>
## NoDelay=true
##
## [Install]
## WantedBy=sockets.target
##
###

[Service]
# Modify these two values and uncomment them if you have
# repos with lots of files and get an HTTP error 500 because
# of that
###
#LimitMEMLOCK=infinity
#LimitNOFILE=65535
RestartSec=2s
Type=simple
User=gitea
Group=gitea
WorkingDirectory=/var/lib/gitea/
# If using Unix socket: tells systemd to create the /run/gitea folder, which will contain the gitea.sock file
# (manually creating /run/gitea doesn't work, because it would not persist across reboots)
#RuntimeDirectory=gitea
ExecStart=/usr/local/bin/gitea web --config /etc/gitea/app.ini
Restart=always
Environment=USER=gitea HOME=/home/gitea GITEA_WORK_DIR=/var/lib/gitea
# If you install Git to directory prefix other than default PATH (which happens
# for example if you install other versions of Git side-to-side with
# distribution version), uncomment below line and add that prefix to PATH
# Don't forget to place git-lfs binary on the PATH below if you want to enable
# Git LFS support
#Environment=PATH=/path/to/git/bin:/bin:/sbin:/usr/bin:/usr/sbin
# If you want to bind Gitea to a port below 1024, uncomment
# the two values below, or use socket activation to pass Gitea its ports as above
###
#CapabilityBoundingSet=CAP_NET_BIND_SERVICE
#AmbientCapabilities=CAP_NET_BIND_SERVICE
###
# In some cases, when using CapabilityBoundingSet and AmbientCapabilities option, you may want to
# set the following value to false to allow capabilities to be applied on gitea process. The following
# value if set to true sandboxes gitea service and prevent any processes from running with privileges
# in the host user namespace.
###
#PrivateUsers=false
###

[Install]
WantedBy=multi-user.target
```

Enable and start
```shell
sudo systemctl enable gitea
sudo systemctl start gitea
```


## Setup [[nginx]]

Edit nginx conf `/etc/nginx/conf.d/gitea.conf` to be

### http

```
server {
    listen 80;
    server_name git.example.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;    }
}
```

### https
```
server {
    listen 80;
    server_name git.jon-e.net;
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name git.jon-e.net;
    ssl_certificate    /root/.acme.sh/git.jon-e.net/git.jon-e.net.cer;
    ssl_certificate_key /root/.acme.sh/git.jon-e.net/git.jon-e.net.key;
    ssl_protocols       TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers         HIGH:!aNULL:!MD5;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```


And then follow the instructions to configure [[acme.sh#nginx]]

## Complete Guided Install

Go to the site, or else to the ip:3000 URL, and finish the guided installation, using the values generated above!

## Modify app.ini
at `/etc/gitea/app.ini` enable ssh and other settings

```ini
[server]
PROTOCOL=https
DOMAIN=git.example.com
ENABLE_ACME=true
ACME_ACCEPTTOS=true
ACME_DIRECTORY=https
;; Email can be omitted here and provided manually at first run, after which it is cached
ACME_EMAIL=email@example.com
```


## Remove permissions
```sh
chmod 750 /etc/gitea
chmod 640 /etc/gitea/app.ini
```