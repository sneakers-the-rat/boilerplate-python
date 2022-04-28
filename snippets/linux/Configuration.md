## List all user-modified configuration files on [[Debian]]

https://serverfault.com/a/90401

```bash
dpkg-query -W -f='${Conffiles}\n' '*' | \
  awk 'OFS="  "{print $2,$1}' | \
  md5sum -c 2>/dev/null | \
  awk -F': ' '$2 !~ /OK/{print $1}'
```

# [[Localization]]

##  [[Time Zone]]
* See time zone
	`timedatectl`
* See available time zone names
	`timedatectl list-timezones`
* Set timezone
	`sudo timedatectl set-timezone your_time_zone`