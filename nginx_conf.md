#HOW TO SETUP VIRTUAL HOST IN UBUNTU LINUX FOR PHP
```bash
sudo apt update
sudo apt upgrade

sudo apt install nginx -y

sudo service nginx start


sudo add-apt-repository ppa:ondrej/php

sudo apt update

sudo apt install php7.2 php7.2-curl php7.2-common php7.2-cli php7.2-mysql php7.2-mbstring php7.2-fpm php7.2-xml php7.2-zip php7.2-gd php7.2-common php7.2-intl php7.2-bcmath -y

```


#now open php fpm ini file and search for cgi.fix_pathinfo and make it 0 from 1

```javascript

sudo gedit /etc/php/7.2/fpm/php.ini

//restart php fpm 

sudo service php7.2-fpm start

[if php 7.4 only option then sudo gedit /etc/php/7.4/fpm/php.ini change cgi.fix_pathinfo=0 then sudo service php7.4-fpm start]

sudo gedit /etc/php/7.2/fpm/php.ini

change cgi.fix_pathinfo=0

sudo apt install mysql-server [php7.4-mysql]

sudo service nginx restart
sudo service nginx reload

```


#Then copy the default conf to your desired conf name

```javascript

sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/production_app.conf

then past the following configuration [ your confirured php7.x-fpm.sock connection  ]

server {
    listen 80;

    server_name production_app.com www.production_app.com;

    root /var/www/html/production_app/public;

    index index.php;

    access_log /var/log/nginx/production_app_access.log;
    error_log /var/log/nginx/production_app_error.log;

    location = /favicon.ico {
        log_not_found off;
        access_log off;
    }

    location = /robots.txt {
        allow all;
        log_not_found off;
        access_log off;
    }

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        #include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.2-fpm.sock;
    }

    location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg)$ {
        expires max;
        log_not_found off;
    }

}

```


#Then create a simlink for your configuration using the following command
```javascript

sudo ln -s /etc/nginx/sites-available/opencart.conf /etc/nginx/sites-enabled/ 

sudo service nginx restart
sudo service nginx reload

now edit your host file give a localhost ip and yourdomainname

```


#File and folder permission for php in root

```javascript
https://stackoverflow.com/questions/30639174/how-to-set-up-file-permissions-for-laravel

sudo chown -R www-data:www-data /var/www/html/

sudo usermod -a -G www-data samin

sudo find /var/www/html/ -type f -exec chmod 644 {} \;

sudo find /var/www/html/ -type d -exec chmod 755 {} \;

sudo chown -R samin:www-data /var/www/html/

sudo chgrp -R www-data storage bootstrap/cache
sudo chmod -R ug+rwx storage bootstrap/cache

```
