# How to setup t3kit on TYPO3 8. Server - Shared 05

1. Create a new repo for your project with the name of the site for example: "thesitename.com"

2. Connection to ssh server.
	* ssh root@theserver
	* cd ```/mnt/persist/www/sites_docroot```

	### Check if there is the server script.
	cd ```/mnt/persist/www/server-script-essentials```

	If yes, there is a server script, use it and skip all these other steps.
	If no, proceed to follow the list.

3. Clone the main repo of t3kit into ```sites_docroot```
	* git clone git@github.com:t3kit/t3kit.git thesitename.com
	* the last "thesitename.com" is the folder which it is created into, if not set, then the folder name will be "t3kit". 
	* Change directory to ```/sites_docroot/thesitename.com```
	* Run ```composer install --no-dev```
	* Then we will need to change the remote url repository
	* ```git remote set-url origin git@github.com:pixelant/thesitename.com.git```
	* (to check url: ```git remote -v```)

4. Create database
	* Change directory to ```mtn/persist/www``` and check that there is a folder named ```t3kit_db```
	* Change directory to ```t3kit_db```and make a git pull to get the latest database
	* then run:
	* mysql
	* ```CREATE DATABASE thesitename_com;```
	* ```GRANT ALL PRIVILEGES ON thesitename\_com .* TO 'thesitename_com'@'localhost' IDENTIFIED BY 'GENERATE A PASSWORD THAT IS GOOD';```
	* ```exit```
	* then run:
	* ```mysql -u thesitename_com -p thesitename_com < t3kit8.sql```

5. 	Create user and group
	* Check which groups are assigned:
	* ```cat /etc/group```
	* find the highest ```www_####``` and then create a group and add 1 to it, for example: if the highest group is ```www_1005``` then add ```www_1006```
	* ```groupadd www_####```
	* then create user in group
	* ```useradd -g www_#### www_####```

6. Change directory to ```/mnt/persist/www/sites_docroot/nameofsite.com/web/typo3conf```
	* Edit the file ```LocalConfiguration.php```
	* Change the credentials for the database that was created previously:

	```
	'DB' => [
        'Connections' => [
            'Default' => [
                'charset' => 'utf8',
                'dbname' => 'nameofsite_com, (CHANGE)
                'driver' => 'mysqli',
                'host' => 'localhost',
                'password' => 'THE GENERATED PASSWORD THAT IS GOOD', (CHANGE)
                'port' => 3306,
                'user' => 'nameofsite_com', (CHANGE)
            ],
        ],
    ]
```
7.	Change directory to ```/mnt/persist/www/sites_conf/```
	* Copy an existing host config:
	* ```cp OTHERnameofsite.com nameofsite.com```
	* Edit the ```nameofsite.com``` file
	* Make the necessary changes:

	```<virtualhost *:80>
ServerName nameofsite.com    (CHANGE)
ServerAlias www.nameofsite.com nameofsite.typo3konsult.se (CHANGE)
AssignUserId www_5002 www_5002 (CHANGE)
Include /mnt/persist/www/apache2_common.conf 
 
ServerAdmin webmaster@pixelant.se (change if not already webmaster@pixelant.se)
DocumentRoot /mnt/persist/www/sites_docroot/nameofsite.com (CHANGE)
 
<DirectoryMatch /mnt/persist/www/sites_docroot/nameofsite.com/> (CHANGE)
    DirectoryIndex index.php index.html
    Options +FollowSymLinks -Indexes
    AllowOverride None
    Order allow,deny
    Allow from all
</DirectoryMatch>
 
ErrorLog /var/log/apache2/error_nameofsite.com.log (CHANGE)
CustomLog /var/log/apache2/access_nameofsite.com.log combined (CHANGE)
```

8. Assign usergroup to site
	* Change directory to ```/mnt/persist/www/sites_docroot/```
	* ```chown -R www_####:www_#### nameofsite.com```
	* check the group and user:
	* ```ls -lah nameofsite.com```
	* check if syntax is OK:
	* ```apachectl configtest```
	* Reload the configuration:
	* ```service apache2 graceful```
