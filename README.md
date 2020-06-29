# htaccesspseudodocroot
.htaccess rules for a domain pseudo document root using centos8 and apache without (additional) editing the httpd.conf and adding virtual hosts.

## Prerequisites
* CentOS8 
* Apache (httpd)
* .htaccess enabled (**httpd.conf**) in (*/etc/httpd/*), **AllowOverride All** for your **DocumentRoot** (*/var/www/html/*):
```
<Directory "/var/www/html">
    #
    # AllowOverride controls what directives may be placed in .htaccess files.
    # It can be "All", "None", or any combination of the keywords:
    #   Options FileInfo AuthConfig Limit
    #
    AllowOverride All
</Directory>
```

*Last revision: 06-29-2020*

## Create virtual hosts with .htaccess

Assuming you created a subdirectory in your **DocumentRoot** for each (sub)domain your folder structure should look like this:
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

1. Alter the content of the .htaccess to fit your (local) configuration
2. Copy/Paste or upload the .htaccess to your **DocumentRoot**
3. ???
