# Setup LAMP Server Ubuntu

**Tested on Ubuntu 20.04 Focal**

# Table of Contents
1. [CREATING NEW USER](#creating-new-user)
2. [USER PERMISSION](#user-permission)
3. [INSTALLING UPDATE AND NECESSARY SOFTWARE](#installing-update-and-necessary-software)
4. [INSTALLING APACHE](#installing-apache)
5. [INSTALLING MYSQL](#installing-mysql)
6. [INSTALLING PHP](#installing-php)
7. [INSTALLING PHPMYADMIN](#installing-phpmyadmin)
8. [CONFIGURE PASSWORD FOR MYSQL ROOT ACCOUNT](#configure-password-for-mysql-root-account)
9. [CREATE USER & CONFIGURE PASSWORD FOR MYSQL](#create-user--configure-password-for-mysql)
10. [INSTALLING PYTHON ](#installing-python)
11. [NSTALLING NODEJS](#installing-nodejs)
12. [INSTALLING COMPOSER](#installing-composer)

## CREATING NEW USER
- \# adduser **aditya**
- \# usermod -aG sudo **aditya**

## USER PERMISSION

Add **user** into **www-data** group
- \# usermod -a -G **www-data** **aditya**

Ensure files in our web root are of group **www-data**
- \# chown -R www-data:www-data /var/www

Give user the ability to **rwx** web files
- \# setfacl -R -m u:**aditya**:rwx /var/www

Add group-based permissions, this allows anyone in group **www-data** to **rwx** web files
- \# setfacl -R -m g:**www-data**:rwx /var/www

View changes
- \# getfacl /var/www

If needed
- \# chmod -R 755 /var/www

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
- if needed (replace the PHP version used)
```
sudo apt-get install php5.6 libapache2-mod-php5.6 php5.6-common php5.6-mbstring php5.6-xmlrpc php5.6-soap php5.6-gd php5.6-xml php5.6-mysql php5.6-cli php5.6-mcrypt php5.6-zip
```
**Note:** php-mcrypt has been removed from php7.2

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
- mysql -u root -p

## CREATE USER & CONFIGURE PASSWORD FOR MYSQL
For access from localhost:
- CREATE USER '**aditya**'@'**localhost**' IDENTIFIED WITH *caching_sha2_password* BY '**password**';
- GRANT ALL PRIVILEGES ON \*.* TO '**aditya**'@'**localhost**' WITH GRANT OPTION;

For access from wildcard:
- CREATE USER '**aditya**'@'**%**' IDENTIFIED WITH *caching_sha2_password* BY '**password**';
- GRANT ALL PRIVILEGES ON \*.* TO '**aditya**'@'**%**' WITH GRANT OPTION;

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
