---
title: "Setting up an LNMP environment (Ubuntu 18.04)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-an-LNMP-environment-Ubuntu-18"
---

An LNMP environment refers to a web application platform built on a Linux system, consisting of Linux, Nginx, MySQL or MariaDB, and PHP. This topic describes how to deploy an LNMP environment on an Ubuntu 18.04 instance.

### Software versions

* Operating system: In the example provided in this topic, Ubuntu 18.04 is used.

* Nginx: A high\-performance, lightweight web server that supports HTTP and reverse proxy. In the example provided in this topic, Nginx 1.14.0 is used.

* MySQL/MariaDB: A database management system. In the example provided in this topic, MariaDB 15.1 is used.

* PHP: A server\-side scripting language embedded in HTML documents. In the example provided in this topic, PHP 7.2.24 is used.

## Prerequisites

* A Linux instance is purchased. For more information, see [Purchasing ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* An EIP is associated with the Linux instance, enabling the instance to connect to the Internet. For information about how to associate an EIP with an ECS instance, see [Associating EIPs](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).

## Step 1: Install and configure Nginx

1. Remotely connect to and log in to the ECS instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to update the package repository.

   ```Plain Text
   apt update && apt upgrade -y
   ```

3. Execute the following command to install Nginx.

   ```Plain Text
   apt install -y nginx
   ```

4. Execute the following command to view the Nginx version.

   ```Plain Text
   nginx -v
   ```

   If the following output is displayed, Nginx is installed.

   ```Plain Text
   nginx version: nginx/1.14.0 (Ubuntu)
   ```

5. Execute the following command to specify that the Nginx service automatically starts upon instance startup.

   ```Plain Text
   systemctl enable nginx
   ```

6. In the local browser, enter `http://<ECS instance EIP>/` to access Nginx.

   If the following output is displayed, Nginx is set up successfully.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2092c5cd86b315927f09d4c2e8608571.png)

## Step 2: Install and configure MariaDB

1. Execute the following command to install MariaDB.

   ```Plain Text
   apt install -y mariadb-server mariadb-client
   ```

2. Execute the following command to view the MariaDB version.

   ```Plain Text
   mysql -V
   ```

   If the following output is displayed, MariaDB is installed.

   ```Plain Text
   mysql Ver 15.1 Distrib 10.1.48-MariaDB, for debian-linux-gnu (x86_64) using readline 5.2
   ```

3. Execute the following command to specify that the MariaDB service automatically starts upon instance startup.

   ```Plain Text
   systemctl enable mariadb
   ```

4. Execute the following command to check whether the MariaDB service is started.

   ```Plain Text
   systemctl status mariadb
   ```

   If `Active: active (running)` is displayed in the output, the MariaDB service is started.

5. Execute the following command to perform MariaDB security operations and specify the password.

   ```Plain Text
   mysql_secure_installation
   ```

   1. Press the Enter key to confirm the password.

   2. Enter `y` and press the Enter key to confirm modification of the database password for the root user.

   3. Specify the MariaDB password and press the Enter key. The password you enter is not displayed by default.

   4. Enter the new password again and press the Enter key to confirm your new password.

      > **tip**

      > Enter a password that meets the strength requirements of the password verification policy.

   5. Enter `y` and press the Enter key to remove the anonymous user.

   6. Enter `y` and press the Enter key to prohibit remote login by the root account.

   7. Enter `y` and press the Enter key to delete the `test` database and its access permission.

   8. Enter `y` and press the Enter key to reload the authorization table.

## Step 3: Install and configure PHP

1. Execute the following command to install PHP.

   ```Plain Text
   apt install -y php php-fpm php-mysql
   ```

2. Execute the following command to view the PHP version.

   ```Plain Text
   php -v
   ```

   If the following output is displayed, PHP is installed.

   ```Plain Text
   PHP 7.2.24-0ubuntu0.18.04.13 (cli) (built: Jul  6 2022 12:23:22) ( NTS )
   Copyright (c) 1997-2018 The PHP Group
   Zend Engine v3.2.0, Copyright (c) 1998-2018 Zend Technologies
    with Zend OPcache v7.2.24-0ubuntu0.18.04.13, Copyright (c) 1999-2018, by Zend Technologies
   ```

   > By default, PHP starts automatically upon instance startup. You do not need to perform any additional configuration.

3. Execute the following command to view the path of the Nginx configuration file.

   ```Plain Text
   cat /etc/nginx/nginx.conf
   ```

   In the following output, the `include` configuration item indicates the path of the file.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e7e57578d55895a94a8258bc6dcbd707.png)

4. Execute the following command to back up the configuration file in the configuration file directory.

   > **tip**

   > Nginx loads configuration files with any names in the `/sites-enabled` directory, causing conflicts. Do not back up the configuration file in the `/etc/nginx/sites-enabled/` directory.

   ```Plain Text
   cd /etc/nginx/sites-enabled/ 
   cp default /tmp/default.conf
   ```

5. Execute the following command to modify the original configuration file.

   ```Plain Text
   vim default
   ```

6. Press the `i` key to enter edit mode and modify the following content in `index`.

   ```Plain Text
   root /var/www/html;#Set this path as the default website root directory for Nginx, which you can change as needed.
   # Add index.php to the list if you are using PHP
   index index.php index.html index.htm index.nginx-debian.html;
   ```

7. Remove the comment markers `#`at the beginning of the lines inside the curly braces of `location ~ \.php$` and modify the following content.

   ```Plain Text
   location ~ \.php$ {
               include snippets/fastcgi-php.conf;
               fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;#Modify the PHP version to the installed PHP version, in this example, it is 7.2.
                   }
   ```

8. Press the `Esc` key, enter `:wq`, and then press Enter to save the modifications and close the file.

9. Execute the following command to restart the Nginx service.

   ```Plain Text
   systemctl restart nginx
   ```

## Step 4: Access LNMP

1. Execute the following command to create a test file.

   ```Plain Text
   vim <website root directory>/phpinfo.php #Replace <website root directory> with the website root directory you configured in the Nginx configuration file default.conf.
   ```

   In the example provided in this topic, the `vim /var/www/html/phpinfo.php` command is executed.

2. Press the `i` key to enter edit mode, and then enter the following content.

   ```Plain Text
   <?php echo phpinfo(); ?>
   ```

3. Press `Esc`, enter `:wq`, and then press Enter to save the modifications and close the file.

4. In your local browser, enter `http://<ECS instance EIP>/phpinfo.php` to access LNMP.

   If the following output is displayed, LNMP is set up successfully.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_44c4d8ab04bf264c7dd1980c23db8d43.png)
