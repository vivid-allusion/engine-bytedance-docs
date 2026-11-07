---
title: "Setting up a LAMP environment (CentOS 8)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-an-LAMP-environment-CentOS-8"
---

A LAMP environment refers to a web application platform built on a Linux system, consisting of Linux, Apache, MySQL or MariaDB, and PHP. This topic describes how to deploy a LAMP environment on a CentOS 8.3 instance.

<span id=".6L2v5Lu254mI5pys"></span>
### Software versions


* Operating system: In the example provided in this topic, CentOS 8.3 is used.

* Apache: A web server with stable performance. In the example provided in this topic, Apache 2.4.37 is used.

* MySQL/MariaDB: A database management system. In the example provided in this topic, MariaDB 15.1 and MySQL 8.0.26 are used.

* PHP: A server\-side scripting language embedded in HTML documents. In the example provided in this topic, PHP 7.3.20 is used.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A Linux instance is purchased. For more information, see [Purchasing ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* An EIP is associated with the Linux instance, enabling the instance to connect to the Internet. For information about how to associate an EIP with an ECS instance, see [Associating EIPs](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).


<span id=".5q2l6aqk5LiA77ya5a6J6KOF5bm26YWN572uQXBhY2hl"></span>
## Step 1: Install and configure Apache


1. Remotely connect to and log in to the ECS instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to install Apache. In the example provided in this topic, Apache 2.4.6 is installed.

   ```Plain Text
   yum install httpd -y
   ```
   

3. Execute the following command to view the Apache version.

   ```Plain Text
   httpd -v
   ```
   

   If the following output is displayed, Apache is installed.

   ```Plain Text
   Server version: Apache/2.4.37 (centos)
   Server built:   Nov 16 2020 16:18:20
   ```
   

4. Execute the following command to start the Apache service.

   ```Plain Text
   systemctl start httpd
   ```
   

5. Execute the following command to specify that the Apache service automatically starts upon instance startup.

   ```Plain Text
   systemctl enable httpd
   ```
   

6. In the local browser, enter `http://<ECS instance EIP>/` to access Apache.

   If the following output is displayed, Apache is set up successfully.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_eec9d207fa0bcbc5e2d6c75ddf4ab1cd.png) </span>


<span id=".5q2l6aqk5LqM77ya5a6J6KOF5bm26YWN572uTWFyaWFEQi9NeVNRTA=="></span>
## Step 2: Install and configure MariaDB/MySQL

<span id=".5a6J6KOF5bm26YWN572uTWFyaWFEQg=="></span>
### Install and configure MariaDB


1. Execute the following command to install MariaDB.

   ```Plain Text
   dnf -y install @mariadb
   ```
   

2. Execute the following command to view the MariaDB version.

   ```Plain Text
   mysql -V
   ```
   

   If the following output is displayed, MariaDB is installed.

   ```Plain Text
   mysql Ver 15.1 Distrib 10.3.28-MariaDB, for Linux (x86_64) using readline 5.1
   ```
   

3. Execute the following command to start the MariaDB service and specify that it automatically starts upon instance startup.

   ```Plain Text
   systemctl enable --now mariadb
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

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Enter a password that meets the strength requirements of the password verification policy.      </div>
      

   5. Enter `y` and press the Enter key to remove the anonymous user.

   6. Enter `y` and press the Enter key to prohibit remote login by the root account.

   7. Enter `y` and press the Enter key to delete the `test` database and its access permission.

   8. Enter `y` and press the Enter key to reload the authorization table.


<span id=".5a6J6KOF5bm26YWN572uTXlTUUw="></span>
### Install and configure MySQL


1. Execute the following command to install MySQL.

   ```Plain Text
   dnf -y install @mysql
   ```
   

2. Execute the following command to view the MySQL version.

   ```Plain Text
   mysql -V
   ```
   

   If the following output is displayed, MySQL is installed.

   ```Plain Text
   mysql Ver 8.0.26 for Linux on x86_64 (Source distribution)
   ```
   

3. Execute the following command to start the MySQL service and specify that it

4.  automatically starts upon instance startup.

   ```Plain Text
   systemctl enable --now mysqld
   ```
   

4. Execute the following command to check whether the MySQL service is started.

   ```Plain Text
   systemctl status mysqld
   ```
   

   If `Active: active (running)` is displayed in the output, the MySQL service is started.

5. Execute the following command to perform MySQL security operations and specify the password.

   ```Plain Text
   mysql_secure_installation
   ```
   

   1. Enter `y` and press the Enter key to start the relevant configuration.

   2. Select the password verification policy strength, and enter `2` and press the Enter key. We recommend that you select a high\-strength verification policy. A value of 0 specifies low strength, 1 specifies medium strength, and 2 specifies high strength.

   3. Specify the new MySQL password and press the Enter key. The password you enter is not displayed by default.

   4. Enter the new password again and press `y` to confirm your new password.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Enter a password that meets the strength requirements of the password verification policy.      </div>
      

   5. Enter `y` and press the Enter key to remove the anonymous user.

   6. Specify whether to allow remote connections to MySQL:

      * To prohibit remote connections: Enter `y` and press the Enter key.

      * To allow remote connections: Enter `n` and press the Enter key.

   7. Enter `y` and press the Enter key to delete the `test` database and its access permission.

   8. Enter `y` and press the Enter key to reload the authorization table.


<span id=".5q2l6aqk5LiJ77ya5a6J6KOF5bm26YWN572uUEhQ"></span>
## Step 3: Install and configure PHP


1. Execute the following command to add and update the EPEL repository.

   ```Plain Text
   dnf -y install epel-release
   dnf -y update epel-release
   ```
   

2. Execute the following command to delete cached unused packages and update the software repository.

   ```Plain Text
   dnf clean all 
   dnf makecache
   ```
   

3. Execute the following command to enable the `php:7.3` module.

   ```Plain Text
   dnf -y module enable php:7.3
   ```
   

   In the example provided in this topic, `php:7.3` is used. If you want to use `php:7.4`, you need to first install the Remi repository and then start the PHP module. Command for installing the Remi repository: `dnf -y install https://rpms.remirepo.net/enterprise/remi-release-8.rpm`.

4. Execute the following command to install the corresponding PHP modules.

   ```Plain Text
   dnf -y install php php-curl php-dom php-exif php-fileinfo php-fpm php-gd php-hash php-json php-mbstring php-mysqli php-openssl php-pcre php-xml libsodium
   ```
   

5. Execute the following command to view the PHP version.

   ```Plain Text
   php -v
   ```
   

   If the following output is displayed, PHP is installed.

   ```Plain Text
   PHP 7.3.20 (cli) (built: Jul  7 2020 07:53:49) ( NTS )
   Copyright (c) 1997-2018 The PHP Group
   Zend Engine v3.3.20, Copyright (c) 1998-2018 Zend Technologies
   ```
   

6. Execute the following command to start the PHP\-FPM service.

   ```Plain Text
   systemctl start php-fpm
   ```
   

7. Execute the following command to specify that the PHP\-FPM service automatically starts upon instance startup.

   ```Plain Text
   systemctl enable php-fpm
   ```
   


<span id=".5q2l6aqk5Zub77ya6K6_6ZeuTEFNUA=="></span>
## Step 4: Access LAMP


1. Execute the following command to create a test file.

   ```Plain Text
   vim /var/www/html/phpinfo.php #/var/www/html/为Apache的网站根目录
   ```
   

2. Press the `i` key to enter edit mode, and then enter the following content.

   ```Plain Text
   <?php echo phpinfo(); ?>
   ```
   

3. Press `Esc`, enter `:wq`, and then press the `Enter` key to save the file and return to the CLI interface.

4. Execute the following command to restart the Apache service.

   ```Plain Text
   systemctl restart httpd
   ```
   

5. Enter `http://<ECS instance EIP>/phpinfo.php` in your local browser to access LAMP.
