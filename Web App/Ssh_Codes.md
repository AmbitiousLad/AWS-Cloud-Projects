### 1. To install Apache to the virtual machine

```
 sudo apt install apache2
```

### 2. To install PHP and related modules on a Linux system.

 ```
sudo apt install php libapache2-mod-php php-mysql
```
### 3. Installing mysql Server
```
sudo apt install mysql-server
```

### 4. Making some modifications in Data Base with password and Username
```
sudo mysql -u root


ALTER USER 'root'@localhost IDENTIFIED WITH mysql_
native_password BY 'Demopassword@123';


CREATE USER 'wp_user'@localhost IDENTIFIED BY 'Dem
opassword@123';

CREATE DATABASE wp;

GRANT ALL PRIVILEGES ON wp.* TO 'wp_user'@localhos
t;

```
### 5. Installing WordPress in the EC2 Instance
```
 cd /tmp
wget https://wordpress.org/la
test.tar.gz
tar xvf latest.tar.gz
```

### 6. Moving Wordpress file to HTML folder
```
 sudo mv wordpress/ /var/www/html/
 cd /var/www/html/
```

### 7. Setting root address of the website to Wordpress by changing in the wp-config.php.
```
 nano wp-config.php
 nano 000-default.conf
 sudo !!
```
