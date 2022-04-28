## [[Backup]] [[mediawiki]]
make a backup directory!
```
mkdir backup
```
### Backup Database
Get variables!
```bash
DBNAME="$(grep -oE '\$wgDBname = .*;' LocalSettings.php | tail -1 | sed 's/$wgDBname = \"//g;s/\";//g')"
DBUSER="$(grep -oE '\$wgDBuser = .*;' LocalSettings.php | tail -1 | sed 's/$wgDBuser = \"//g;s/\";//g')"
DBPASS="$(grep -oE '\$wgDBpassword = .*;' LocalSettings.php | tail -1 | sed 's/$wgDBpassword = \"//g;s/\";//g')"
DBSERVER="$(grep -oE '\$wgDBserver = .*;' LocalSettings.php | tail -1 | sed 's/$wgDBserver = \"//g;s/\";//g')"
```

Dump DB to gzip!

```bash
mysqldump -h $DBSERVER -u $DBUSER -p --default-character-set=binary $DBNAME | gzip > backup/wiki_backup-$(date '+%Y%m%d').sql.gz
```

add the `--xml` flag for xml backups!

### Backup Files

```bash
tar zcvhf backup/wiki_uploads.tar.gz images
tar zcvhf backup/wiki_extensions.tar.gz extensions
cp LocalSettings.php backup/

```

## Upgrade [[mediawiki]]

https://www.mediawiki.org/wiki/Manual:Upgrading

- Download and untar new mediawiki to new directory
- copy old files from old wiki
	- images
	- LocalSettings.php
	- logo
- Reinstall extensions
- 