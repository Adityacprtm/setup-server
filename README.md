# Setup Server Ubuntu

Tested on Ubuntu 20.04 Focal

## CREATING NEW USER
- adduser **aditya**
- usermod -aG sudo **aditya**

## INSTALLING UPDATE AND NECESSARY SOFTWARE
- sudo apt update
- sudo apt upgrade
- sudo apt install build-essential
- sudo apt install software-properties-common

## INSTALLING APACHE
- sudo apt update
- sudo apt install apache
- sudo service apache2 start

## INSTALLING MYSQL
- sudo apt update
- sudo apt install mysql-server

## INSTALLING PHP
- sudo apt update
- sudo apt install php libapache2-mod-php php-mysql
- sudo nano /etc/apache2/mods-enabled/dir.conf
```
<IfModule mod_dir.c>
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```


## INSTALLING PHPMYADMIN
- sudo apt update
- sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl
- sudo phpenmod mbstring
- sudo service apache2 restart

## CONFIGURE PASSWORD FOR MYSQL ROOT ACCOUNT
 - sudo mysql
 - SELECT user,authentication_string,plugin,host FROM mysql.user;
 - ALTER USER '**root**'@'localhost' IDENTIFIED WITH *caching_sha2_password* BY '**password**';
if any error with password encryption (depending on the php version), use this:
	 - ALTER USER '**root**'@'localhost' IDENTIFIED WITH *mysql_native_password* BY '**password**';
- SELECT user,authentication_string,plugin,host FROM mysql.user;
mysql -u root -p

## CREATE USER & CONFIGURE PASSWORD FOR MYSQL
For access from localhost:
- CREATE USER '**aditya**'@'**localhost**' IDENTIFIED WITH *caching_sha2_password* BY '**password**';
- GRANT ALL PRIVILEGES ON *.* TO '**aditya**'@'**localhost**' WITH GRANT OPTION;

For access from wildcard:
- CREATE USER '**aditya**'@'**%**' IDENTIFIED WITH *caching_sha2_password* BY '**password**';
- GRANT ALL PRIVILEGES ON *.* TO '**aditya**'@'**%**' WITH GRANT OPTION;

Reloads the grant tables:
- FLUSH PRIVILIGES;

## INSTALLING PYTHON
- sudo apt update
- sudo apt install python3
- sudo apt install python2

## INSTALLING NODEJS
- sudo apt update
- sudo apt install nodejs
- sudo apt install npm

## INSTALLING COMPOSER
- sudo apt update
- sudo apt install php-cli unzip
- cd ~
- curl -sS https://getcomposer.org/installer -o composer-setup.php
- sudo php composer-setup.php --install-dir=**/usr/local/bin** --filename=**composer**
