---
title: "Setting up a LAMP environment (CentOS 7)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-an-LAMP-environment-CentOS-7"
---

A LAMP environment refers to a web application platform built on a Linux system, consisting of Linux, Apache, MySQL or MariaDB, and PHP. This topic describes how to deploy a LAMP environment on a CentOS 7.6 instance.

<span id=".6L2v5Lu254mI5pys"></span>
### Software versions


* Operating system: In the example provided in this topic, CentOS 7.6 is used. You can also use CentOS 7.9, veLinux 1.0 (CentOS compatible version), or other CentOS 7 series images.

* Apache: A web server with stable performance. In the example provided in this topic, Apache 2.4.6 is used.

* MySQL/MariaDB: A database management system. In the example provided in this topic, MariaDB 15.1 and MySQL Community Edition 8.4.3 are used.

* PHP: A server\-side scripting language embedded in HTML documents. In the example provided in this topic, PHP 7.0.33 is used.


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
   Server version: Apache/2.4.6 (CentOS)
   Server built:   Mar 24 2022 14:57:57
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

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/6d64ec2244134f68b64cea957718bd47.png) </span>


<span id=".5q2l6aqk5LqM77ya5a6J6KOF5bm26YWN572uTWFyaWFEQi9NeVNRTA=="></span>
## Step 2: Install and configure MariaDB/MySQL

<span id=".5a6J6KOF5bm26YWN572uTWFyaWFEQg=="></span>
### Install and configure MariaDB


1. Execute the following command to install MariaDB.

   ```Plain Text
   yum -y install mariadb-server mariadb-client
   ```
   

2. Execute the following command to view the MariaDB version.

   ```Plain Text
   mysql -V
   ```
   

   If the following output is displayed, MariaDB is installed.

   ```Plain Text
   mysql Ver 15.1 Distrib 5.5.68-MariaDB, for Linux (x86_64) using readline 5.1
   ```
   

1. Execute the following command to start the MariaDB service and specify that it automatically starts upon instance startup.

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


1. Execute the following command to download the RPM package for the MySQL Community Edition repository configuration file.

   ```Plain Text
   wget https://dev.mysql.com/get/mysql84-community-release-el7-1.noarch.rpm
   ```
   

2. Execute the following command to install the MySQL 8.4 Community Edition software repository configuration file.

   ```Plain Text
   rpm -Uvh mysql84-community-release-el7-1.noarch.rpm
   ```
   

3. Execute the following command to install MySQL 8.4.

   ```Plain Text
   yum -y install mysql-community-server
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the <code>Failing package is: mysql-community-libs-compat-8.4.3-1.el7.x86_64</code> error occurs, the GPG key for MySQL is upgraded and needs to be retrieved again. In this case, execute the following commands in sequence: <code>rpm --import</code><code> https://repo.mysql.com/RPM-GPG-KEY-mysql-2022</code> and <code>yum -y install mysql-server</code>.   </div>
   

4. Execute the following command to view the MySQL version.

   ```Plain Text
   mysql -V
   ```
   

   If the following output is displayed, MySQL is installed.

   ```Plain Text
   mysql Ver 8.4.3 for Linux on x86_64 (MySQL Community Server - GPL)
   ```
   

5. Execute the following command to start the MySQL service and specify that it automatically starts upon instance startup.

   ```Plain Text
   systemctl enable --now mysqld
   ```
   

6. Execute the following command to check whether the MySQL service is started.

   ```Plain Text
   systemctl status mysqld
   ```
   

   If `Active: active (running)` is displayed in the output, the MySQL service is started.

7. Execute the following command to view the initial password that was automatically specified during MySQL installation.

   ```Plain Text
   grep 'temporary password' /var/log/mysqld.log
   ```
   

   Output similar to the following is displayed. In this example, the initial password is `0zNwvmpr:fOd`.

   ```Plain Text
   2021-09-17T09:31:12.142217Z 1 [Note] A temporary password is generated for root@localhost: 0zNwvmpr:fOd
   ```
   

8. Execute the following command to perform MySQL security operations and specify the password.

   ```Plain Text
   mysql_secure_installation
   ```
   

   1. Enter the initial password obtained in the previous step and press the Enter key.

   2. Specify the new MySQL password and press the Enter key. The password you enter is not displayed by default.

   3. Enter the new password again and press `y` to confirm your new password.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Enter a password that meets the strength requirements of the password verification policy.      </div>
      

   4. Repeat the preceding steps to specify the new password, and then enter `y` to confirm the new password.

   5. Enter `y` and press the Enter key to remove the anonymous user.

   6. Enter `y` and press the Enter key to prohibit remote login by the root account.

   7. Enter `y` and press the Enter key to delete the `test` database and its access permission.

   8. Enter `y` and press the Enter key to reload the authorization table.


<span id=".5q2l6aqk5LiJ77ya5a6J6KOF5bm26YWN572uUEhQ"></span>
## Step 3: Install and configure PHP


1. Execute the following command to add and update the EPEL repository.

   ```Plain Text
   wget -O /etc/yum.repos.d/epel.repo http://mirrors.ivolces.com/repo/epel-7.repo
   ```
   

2. Execute the following command to add the Remi repository.

   ```Plain Text
   rpm -Uvh http://rpms.remirepo.net/enterprise/remi-release-7.rpm
   ```
   

3. Execute the following command to install the yum\-config\-manager repository management tool.

   ```Plain Text
   yum -y install yum-utils
   ```
   

4. Execute the following command to enable the specified Remi PHP 7.0 repository by using yum\-config\-manager.

   ```Plain Text
   yum-config-manager --enable remi-php70
   ```
   

5. Execute the following command to install PHP 7.0 and common modules.

   ```Plain Text
   yum -y install php php-mysqlnd php-fpm
   ```
   

6. Execute the following command to start the PHP\-FPM service.

   ```Plain Text
   systemctl start php-fpm
   ```
   

7. Execute the following command to specify that the PHP\-FPM service automatically starts upon instance startup.

   ```Plain Text
   systemctl enable php-fpm
   ```
   

8. Execute the following command to view the PHP version.

   ```Plain Text
   php -v
   ```
   

   If the following output is displayed, PHP is installed.

   ```Plain Text
   PHP 7.0.33 (cli) (built: Jun 7 2022 14:11:00) ( NTS )
   Copyright (c) 1997-2017 The PHP Group
   Zend Engine v3.0.0, Copyright (c) 1998-2017 Zend Technologies
   ```
   


<span id=".5q2l6aqk5Zub77ya6K6_6ZeuTEFNUA=="></span>
## Step 4: Access LAMP


1. Execute the following command to create a test file.

   ```Plain Text
   vim /var/www/html/phpinfo.php
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><code>/var/www/html/</code> is the web root directory for Apache.   </div>
   

2. Press the `i` key to enter edit mode, and then enter the following content.

   ```Plain Text
   <?php echo phpinfo(); ?>
   ```
   

3. Press `Esc`, enter `:wq`, and then press Enter to save the modifications and close the file.

4. Execute the following command to restart the Apache service.

   ```Plain Text
   systemctl restart httpd
   ```
   

5. Enter `http://<ECS instance EIP>/phpinfo.php` in your local browser to access LAMP.

   If the following output is displayed, LAMP is set up successfully.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_5bcfe10c075b916e1e1f4b6030660dd8.png) </span>
