### ARP - Branch

- basic installation
- import mysql
- set settings.php credentials
- if the .htaccess file is missing in "arp-vm/drupal/drupal" import the default drupal7 htaccess or following

```
<FilesMatch "\.(engine|inc|info|install|make|module|profile|test|po|sh|.*sql|theme|tpl(\.php)?|xtmpl)(~|\.sw[op]|\.bak|\.orig|\.save)?$|^(\.(?!well-known).*|Entries.*|Repository|Root|Tag|Template|composer\.(json|lock)|web\.config)$|^#.*#$|\.php(~|\.sw[op]|\.bak|\.orig\.save)$">
  <IfModule mod_authz_core.c>
    Require all denied
  </IfModule>
  <IfModule !mod_authz_core.c>
    Order allow,deny
  </IfModule>
</FilesMatch>

Options -Indexes

Options +FollowSymLinks

ErrorDocument 404 /index.php

DirectoryIndex index.php index.html index.htm

<IfModule mod_php5.c>
  php_flag magic_quotes_gpc                 off
  php_flag magic_quotes_sybase              off
  php_flag register_globals                 off
  php_flag session.auto_start               off
  php_value mbstring.http_input             pass
  php_value mbstring.http_output            pass
  php_flag mbstring.encoding_translation    off
</IfModule>

<IfModule mod_expires.c>
  ExpiresActive On
  ExpiresDefault A1209600

  <FilesMatch \.php$>
    ExpiresActive Off
  </FilesMatch>
</IfModule>

<IfModule mod_rewrite.c>
  RewriteEngine on

  RewriteRule ^ - [E=protossl]
  RewriteCond %{HTTPS} on
  RewriteRule ^ - [E=protossl:s]

  RewriteRule ^ - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]

  RewriteRule "/\.|^\.(?!well-known/)" - [F]

  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteCond %{REQUEST_URI} !=/favicon.ico
  RewriteRule ^ index.php [L]

  <IfModule mod_headers.c>
    RewriteCond %{HTTP:Accept-encoding} gzip
    RewriteCond %{REQUEST_FILENAME}\.gz -s
    RewriteRule ^(.*)\.css $1\.css\.gz [QSA]

    RewriteCond %{HTTP:Accept-encoding} gzip
    RewriteCond %{REQUEST_FILENAME}\.gz -s
    RewriteRule ^(.*)\.js $1\.js\.gz [QSA]

    RewriteRule \.css\.gz$ - [T=text/css,E=no-gzip:1]
    RewriteRule \.js\.gz$ - [T=text/javascript,E=no-gzip:1]

    <FilesMatch "(\.js\.gz|\.css\.gz)$">
      Header set Content-Encoding gzip
      Header append Vary Accept-Encoding
    </FilesMatch>
  </IfModule>
</IfModule>

<IfModule mod_headers.c>
  Header always set X-Content-Type-Options nosniff
</IfModule>
```
