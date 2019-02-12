#mkdir in /var/www/html/

#create laravel project like laravelrest

#now copy 000-default conf like the following

#sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/laravelrestvue.com.conf

now edit the conf file like the following
```php

<VirtualHost *:80>
     
        ServerName laravelrestvue.com
        ServerAdmin webmaster@localhost
        DocumentRoot /home/shaikh/Desktop/larticles_api/public

	<Directory />
	    Options Indexes FollowSymLinks Includes ExecCGI
	    AllowOverride All
	    Require all granted
	    Allow from all
	</Directory>

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet


sudo a2ensite laravelrestvue.com

sudo service apache2 reload
sudo service apache2 restart

now create an entry point in the host file like the following
sudo nano /etc/hosts
127.0.0.1       laravelrestvue.com

```
