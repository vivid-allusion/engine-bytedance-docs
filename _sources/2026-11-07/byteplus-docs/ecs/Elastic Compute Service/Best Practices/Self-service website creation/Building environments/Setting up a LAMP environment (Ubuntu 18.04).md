---
title: "Setting up a LAMP environment (Ubuntu 18.04)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-an-LAMP-environment-Ubuntu-18"
---

A LAMP environment refers to a web application platform built on a Linux system, consisting of Linux, Apache, MySQL or MariaDB, and PHP. This topic describes how to deploy a LAMP environment on an Ubuntu 18.04 instance.

<span id=".6L2v5Lu254mI5pys"></span>
### Software versions


* Operating system: In the example provided in this topic, Ubuntu 18.04 is used.

* Apache: A web server with stable performance. In the example provided in this topic, Apache 2.4.29 is used.

* MySQL/MariaDB: A database management system. In the example provided in this topic, MariaDB 15.1 is used.

* PHP: A server\-side scripting language embedded in HTML documents. In the example provided in this topic, PHP 7.2.24 is used.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A Linux instance is purchased. For more information, see [Purchasing ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* An EIP is associated with the Linux instance, enabling the instance to connect to the Internet. For information about how to associate an EIP with an ECS instance, see [Associating EIPs](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).


<span id=".5q2l6aqk5LiA77ya5a6J6KOF5bm26YWN572uQXBhY2hl"></span>
## Step 1: Install and configure Apache


1. Remotely connect to and log in to the ECS instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to update the package repository.

   ```Plain Text
   apt update && apt upgrade -y
   ```
   

3. Execute the following command to install Apache. In the example provided in this topic, Apache 2.4.29 is installed.

   ```Plain Text
   apt install -y apache2
   ```
   

4. Execute the following command to view the Apache version.

   ```Plain Text
   apache2 -v
   ```
   

   If the following output is displayed, Apache is installed.

   ```Plain Text
   Server version: Apache/2.4.29 (Ubuntu)
   Server built:  2022-06-23T12:51:37
   ```
   

5. Execute the following command to specify that the Apache service automatically starts upon instance startup.

   ```Plain Text
   systemctl enable apache2
   ```
   

6. In the local browser, enter `http://<ECS instance EIP>/` to access Apache.

   If the following output is displayed, Apache is set up successfully.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_41b38b40b0d0f9da0bc38df724f8be81.png) </span>


<span id=".5q2l6aqk5LqM77ya5a6J6KOF5bm26YWN572uTWFyaWFEQg=="></span>
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

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Enter a password that meets the strength requirements of the password verification policy.      </div>
      

   5. Enter `y` and press the Enter key to remove the anonymous user.

   6. Enter `y` and press the Enter key to prohibit remote login by the root account.

   7. Enter `y` and press the Enter key to delete the `test` database and its access permission.``

   8. Enter `y` and press the Enter key to reload the authorization table.


<span id=".5q2l6aqk5LiJ77ya5a6J6KOF5bm26YWN572uUEhQ"></span>
## Step 3: Install and configure PHP


1. Execute the following command to install PHP.

   ```Plain Text
   apt install -y php php-mysql
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
   

<span id=".5q2l6aqk5Zub77ya6K6_6ZeuTEFNUA=="></span>
## Step 4: Access LAMP


1. Execute the following command to create a test file.

   ```Plain Text
   vim /var/www/html/phpinfo.php
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"> <code>/var/www/html/</code> is the web root directory for Apache.   </div>
   

2. Press the `i` key to enter edit mode, and then enter the following content.

   ```Plain Text
   <?php echo phpinfo(); ?> 
   ```
   

3. Press `Esc`, enter `:wq`, and then press Enter to save the modifications and close the file.

4. Execute the following command to restart the Apache service.

   ```Plain Text
   systemctl restart apache2
   ```
   

5. Enter `http://<ECS instance EIP>/phpinfo.php` in your local browser to access LAMP.

   If the following output is displayed, LAMP is set up successfully.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_86dcd04a24be01dba3c6842abed2e815.png) </span>
