## Fixing Microsoft MIME type mismatch
[Reference](https://www.mediawiki.org/wiki/Manual_talk:MIME_type_detection)

If you get `File extension ".pptx" does not match the detected MIME type of the file (application/zip).`

Edit `mediawiki/includes/mime.types`
like
```
application/zip zip jar xpi  sxc stc  sxd std   sxi sti   sxm stm   sxw stw  doc docx ppt pptx
```


## Increase max upload size

* in `LocalSettings.php`

```php
# 1024 * 1024 * 1024 = 1GB
$wgMaxUploadSize = 1073741824;
```

* In `php.ini` (see [[php]] for how to locate)...
	* Note: there may be two `ini` files. There might be one for base php and another for apache, which is typically in `/etc/php/8.0/apache2/php.ini`

```ini
upload_max_filesize = 1073741824
post_max_size = 1073741824
```

* restart apache `sudo systemctl restart apache2`
* 