with [[apache]]
https://www.mediawiki.org/wiki/Manual:Short_URL/Apache

for a wiki in the `/wiki` directory and urls like `/wiki/Page_Name`. 
In the `.htaccess` file in the parent directory of the wiki:

```apache
RewriteEngine On
RewriteCond %{DOCUMENT_ROOT}%{REQUEST_URI} !-f
RewriteCond %{DOCUMENT_ROOT}%{REQUEST_URI} !-d
RewriteRule ^/?wiki(/(?:(?!rest.php/).)*)?$ /wiki/index.php [L]
RewriteRule ^/*$ /wiki/index.php [L]
```

The modification to exclude `rest.php` allows [[Visual Editor]] to be used with short urls.