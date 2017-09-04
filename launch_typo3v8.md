## Pre-launch
1) sites_conf

```
<virtualhost *:80>
ServerName hassleholmskolsida.typo3konsult.se
AssignUserId www_1008 www_1008

ServerAdmin webmaster@hassleholmskolsida.typo3konsult.se
DocumentRoot /mnt/persist/www/sites_docroot/hassleholmskolsida.typo3konsult.se/web

<DirectoryMatch /mnt/persist/www/sites_docroot/hassleholmskolsida.typo3konsult.se/web/>
    DirectoryIndex index.php index.html
    Options +FollowSymLinks -Indexes
    AllowOverride None
    Order allow,deny
    Allow from all
</DirectoryMatch>

ErrorLog /var/log/apache2/error_hassleholmskolsida.typo3konsult.se.log
CustomLog /var/log/apache2/access_hassleholmskolsida.typo3konsult.se.log combined

# Possible values include: debug, info, notice, warn, error, crit, alert, emerg.
LogLevel warn
#ServerSignature On
</VirtualHost>
```

Add
ServerAlias www.mittavtryck.se mittavtryck.se
ServerAlias www.sopsamlarmonster.se sopsamlarmonster.se
after AssignUserId

2) save
3) sevice apache2 restart
4) apache2ctl graceful

https://docs.google.com/document/d/19zGAWncWnYIv9TttwQRLXYi1JBlGggpxmRqS7JfWQcE/edit
5) In BE Check TYPO3 report

Reports > Status Reports
6) Check validation
7) Check scheduler
8) go to /mnt/persist/solr and edit solr.xml

## Post-launch
