# htaccesspseudodocroot
.htaccess rules for a domain pseudo document root using centos8 and apache without editing the httpd.conf and adding virtual hosts.

Assuming you created a subdirectory in your **DocumentRoot** (*/var/www/html/*) for each (sub)domain your folder structure should look like this:
```
var/www/html
 - var/www/html/domain1.com/
 - var/www/html/domain2.com/
 - var/www/html/domain3.com/
```

Requests to **domain1.com**/**domain2.com**/**domain3.com**/etc. will be redirected to the appropriate subdirectory. Bear in mind to also rewrite the base in order to make them static assets/links to further subdirectories/files work!

```
RewriteEngine on

RewriteBase /

# Redirect Request domain1.com to subdir /domain1.com
RewriteCond %{HTTP_HOST} ^domain1\.com$ [NC]
RewriteRule !^domain1\.com /domain1.com%{REQUEST_URI} [L,NC,QSA]

# Redirect Request domain2.com to /domain2.com
RewriteCond %{HTTP_HOST} ^domain2\.com$ [NC]
RewriteRule !^domain2\.com /domain2.com%{REQUEST_URI} [L,NC,QSA]

# Redirect Request domain3.com to /domain3.com
RewriteCond %{HTTP_HOST} ^domain3\.com$ [NC]
RewriteRule !^domain3\.com /domain3.com%{REQUEST_URI} [L,NC,QSA]
```
