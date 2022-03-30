# Setting up a Mediawiki Instance from Scratch
[Mediawiki Installation Guide](https://www.mediawiki.org/wiki/Manual:Installation_guide)


## Install Ubuntu Server
https://ubuntu.com/download/server

### Mac
* Download the .iso file
* Plug in a flash drive!
* Open a Terminal, and find the device number
	* `sudo diskutil list`
* Unmount the disk!
	* `sudo diskutil unmountDisk /dev/disk*`
* Use `dd` to flash the image
	* `sudo dd if=/location/of/the.iso of=/dev/rdisk* bs=1m`
* Boot from the flash drive and install!

## Enable SSH Access
[SSH on autopilot wiki](https://wiki.auto-pi-lot.com/index.php/SSH)


## Install Mediawiki
* Install prereqs
	* `sudo apt-get install php php-apcu php-intl php-mbstring php-xml php-mysql mariadb-server apache2`
* Download mediawiki
	* Get link from [download page](https://www.mediawiki.org/wiki/Download)
	* Download with wget `wget https://releases.wikimedia.org/mediawiki/1.37/mediawiki-1.37.1.tar.gz`
* Unzip mediawiki into location of server (for example `/var/www/html`)
	* If the archive unzips to a subdirectory, just move its contents where they need to be
	* `mv mediawikiversion/* ./`
* Open page (either the IP address of the server (get with `ip address` in command line) or a domain) to begin installation process
	* You may need to manually make the database and user, you can follow [these instructions](https://www.mediawiki.org/wiki/Manual:Installing_MediaWiki#MariaDB/MySQL)
```sql
CREATE DATABASE wikidb;
CREATE USER 'wikiuser'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON wikidb.* TO 'wikiuser'@'localhost' WITH GRANT OPTION;
```

## Configure [[DNS]]


## Configure [[SSH]] with [[apache2]]
[Apache2 Guide](https://www.arubacloud.com/tutorial/how-to-enable-https-protocol-with-apache-2-on-ubuntu-20-04.aspx)
* acme.sh issue certs*
* acme.sh install certs to a different location
* edit `/etc/apache2/sites-available/default-ssl.conf`
* (where are the freaking .conf files)



```xml
      
<VirtualHost *:443>

 ServerName my-domain.com
 DocumentRoot /var/www/html
 SSLEngine on
 SSLCertificateFile /etc/ssl/localcerts/cert.pem
 SSLCertificateKeyFile /etc/ssl/localcerts/key.pem
 SSLCertificateChainFile /etc/ssl/localcerts/fullchain.pem

</VirtualHost>
```

And then in /conf-available/ssl-params.conf

```
SSLCipherSuite EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH

	SSLProtocol All -SSLv2 -SSLv3 -TLSv1 -TLSv1.1
	
	SSLHonorCipherOrder On
	
	
	Header always set X-Frame-Options DENY
	
	Header always set X-Content-Type-Options nosniff
	
	# Requires Apache >= 2.4
	
	SSLCompression off
	
	SSLUseStapling on
	
	SSLStaplingCache "shmcb:logs/stapling-cache(150000)"
	
	
	# Requires Apache >= 2.4.11
	
	SSLSessionTickets Off
```


```bash
sudo a2enmod ssl
sudo a2enmod headers
sudo a2enconf ssl-params
sudo a2ensite default-ssl
sudo apache2ctl configtest
```

If the message "Syntax OK" appears on the screen, proceed by restarting Apache:

```bash
systemctl restart apache2
```

