---
title: "Setting up an LNMP environment (CentOS 7)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-an-LNMP-environment-CentOS-7"
---

An LNMP environment refers to a web application platform built on a Linux system, consisting of Linux, Nginx, MySQL or MariaDB, and PHP. This topic describes how to deploy an LNMP environment on a CentOS 7.6 instance.

<span id=".6L2v5Lu254mI5pys"></span>
### Software versions


* Operating system: In the example provided in this topic, CentOS 7.6 is used. You can also use CentOS 7.9, veLinux 1.0 (CentOS compatible version), or other CentOS 7 series images.

* Nginx: A high\-performance, lightweight web server that supports HTTP and reverse proxy. In the example provided in this topic, Nginx 1.22.0 is used.

* MySQL/MariaDB: A database management system. In the example provided in this topic, MariaDB 15.1 and MySQL Community Edition 8.4.3 are used.

* PHP: A server\-side scripting language embedded in HTML documents. In the example provided in this topic, PHP 7.0.33 is used.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A Linux instance is purchased. For more information, see [Purchasing ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* An EIP is associated with the Linux instance, enabling the instance to connect to the Internet. For information about how to associate an EIP with an ECS instance, see [Associating EIPs](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).


<span id=".5q2l6aqk5LiA77ya5a6J6KOF5bm26YWN572uTmdpbng="></span>
## Step 1: Install and configure Nginx


1. Remotely connect to and log in to the ECS instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to install Nginx.

   ```Plain Text
   yum install -y https://mirrors.ivolces.com/nginx_all/centos/7/x86_64/RPMS/nginx-1.22.0-1.el7.ngx.x86_64.rpm
   ```
   

3. Execute the following command to view the Nginx version.

   ```Plain Text
   nginx -v
   ```
   

   If the following output is displayed, Nginx is installed.

   ```Plain Text
   nginx version: nginx/1.22.0
   ```
   

4. Execute the following command to view the path of the Nginx configuration file.

   ```Plain Text
   cat /etc/nginx/nginx.conf
   ```
   

   In the following output, the `include` configuration item indicates the path of the file.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f8ceb58341ac4f618765b6c14ed59e6b.png) </span>

5. Execute the following command to back up the configuration file in the configuration file directory.

   ```Plain Text
   cd /etc/nginx/conf.d 
   cp default.conf default.conf.bak
   ```
   

6. Execute the following command to modify the original configuration file.

   ```Plain Text
   vi default.conf
   ```
   

7. Press the `i` key to enter edit mode and modify the following content in `location`.

   ```Plain Text
   location / {
           root /usr/share/nginx/html; #Replace this path with your website root directory. In this document, /usr/share/nginx/html is used as an example, which you may reuse directly; however, in actual business scenarios, it is recommended that you replace it with your own website root directory.
           index  index.html index.htm index.php; #Add index.php as the default homepage information.
   }
   ```
   

8. Remove the comment markers at the beginning of the lines inside the curly braces of `location ~ \.php$`, `#`and modify the following content.

   ```Plain Text
   location ~ \.php$ { 
           root /usr/share/nginx/html; #Replace this path with your website root directory. In this document, /usr/share/nginx/html is used as an example. You may reuse it directly; however, in actual business scenarios, it is recommended that you replace it with your own website root directory.
           fastcgi_pass  127.0.0.1:9000;   #Nginx forwards PHP requests to PHP-FPM for processing via the 9000 port on the local machine.
           fastcgi_index index.php; 
           fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name; #Change /scripts$fastcgi_script_name to $document_root$fastcgi_script_name.
           include fastcgi_params;
   }
   ```
   

9. Press the `Esc` key, enter `:wq`, and then press Enter to save the modifications and close the file.

10. Execute the following command to start the Nginx service.

   ```Plain Text
   systemctl start nginx
   ```
   

11. Execute the following command to specify that the Nginx service automatically starts upon instance startup.

   ```Plain Text
   systemctl enable nginx
   ```
   

12. In the local browser, enter `http://<ECS instance EIP>/` to access Nginx.

   The following output indicates that Nginx is set up successfully.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5f4db1fcf8425b64df04ff7ba44e8efb.png) </span>


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
   

3. Execute the following command to start the MariaDB service and specify that the MariaDB service automatically starts upon instance startup.

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
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the <code>Failing package is: mysql-community-libs-compat-8.4.3-1.el7.x86_64</code> error occurs, the GPG key for MySQL is upgraded and needs to be retrieved again. In this case, execute the following commands in sequence: <code>rpm --import </code><code>https://repo.mysql.com/RPM-GPG-KEY-mysql-2022</code> and <code>yum -y install mysql-server</code>.   </div>
   

4. Execute the following command to view the MySQL version.

   ```Plain Text
   mysql -V
   ```
   

   If the following output is displayed, MySQL is installed.

   ```Plain Text
   mysql Ver 8.4.3 for Linux on x86_64 (MySQL Community Server - GPL)
   ```
   

5. Execute the following command to start the MySQL service and specify that the MySQL service automatically starts upon instance startup.

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
   rpm -Uvh https://mirrors.ivolces.com/remi/enterprise/remi-release-7.rpm
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
   


<span id=".5q2l6aqk5Zub77ya6K6_6ZeuTE5NUA=="></span>
## Step 4: Access LNMP


1. Execute the following command to create a test file.

   ```Plain Text
   vim <Website root directory>/phpinfo.php
   ```
   

   Replace `<website root directory>` in the command with the website root directory that you configured in the Nginx configuration file default.conf. In the example provided in this topic, /usr/share/nginx/html is used. The command used in this topic is `vim /usr/share/nginx/html/phpinfo.php`.

2. Press the `i` key to enter edit mode, and then enter the following content.

   ```Plain Text
   <?php echo phpinfo(); ?>
   ```
   

3. Press `Esc`, enter `:wq`, and then press the `Enter` key to save the file and return to the CLI interface.

4. In your local browser, enter `http://<ECS instance EIP>/phpinfo.php` to access LNMP.
