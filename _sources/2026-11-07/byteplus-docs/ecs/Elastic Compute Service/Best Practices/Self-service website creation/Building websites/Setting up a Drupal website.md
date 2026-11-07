---
title: "Setting up a Drupal website"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-Drupal-website"
---

Drupal is an open\-source content management framework written in PHP, consisting of a content management system and a PHP development framework. Drupal integrates powerful and freely configurable features, supporting website projects ranging from personal blogs to large community\-driven sites and other various application types.

<span id=".6L2v5Lu254mI5pys"></span>
## Software versions


* Operating system: In the example provided in this topic, CentOS 7.6 is used.

* Apache: A web server with stable performance. In the example provided in this topic, Apache 2.4.6 is used.

* MySQL/MariaDB: A database management system. In the example provided in this topic, MySQL 14.14 is used.

* PHP: A server\-side scripting language embedded in HTML documents. In the example provided in this topic, PHP 7.0.33 is used.

* Drupal: In the example provided in this topic, Drupal 8.1.1 is used.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A Linux instance is purchased and a LAMP environment is set up. For more information, see [Setting up a LAMP environment (CentOS 7)](https://docs.byteplus.com/en/docs/ecs/Building-an-LAMP-environment-CentOS-7).

<span id=".56ys5LiA5q2l77ya5Yib5bu6RHJ1cGFs5pWw5o2u5bqT"></span>
## Step 1: Create a database for Drupal


1. Execute the following command to access the MySQL database as the root user. The password of the root user is the one you specified during MySQL configuration.

   ```Plain Text
   mysql -u root -p
   ```
   

2. Execute the following command to create a database for Drupal.

   ```SQL
   create database database_name;
   ```
   

3. Create a user for the database created for Drupal.

   ```SQL
   create user 'username'@'localhost' identified by 'Password';
   ```
   

4. Grant all permissions to the user.

   ```SQL
   grant all privileges on database name.* to 'username'@'localhost';
   ```
   

5. Execute the following command to make the preceding commands take effect.

   ```SQL
   flush privileges;
   ```
   

6. Execute the following command to exit the MySQL database.

   ```SQL
   exit
   ```
   


<span id=".56ys5LqM5q2l77ya5LiL6L295bm26YWN572uRHJ1cGFs"></span>
## Step 2: Download and configure Drupal


1. Execute the following command to download Drupal.

   ```Plain Text
   wget http://ftp.drupal.org/files/projects/drupal-8.1.1.zip
   ```
   

2. Execute the following command to decompress the Drupal installation package.

   ```Plain Text
   unzip drupal-8.1.1.zip
   ```
   

3. Execute the following command to move the Drupal files to the website root directory.

   ```Plain Text
   mv drupal-8.1.1/ /var/www/html/drupal
   ```
   

4. Execute the following command to enter the website root directory of Drupal.

   ```Plain Text
   cd /var/www/html/drupal
   ```
   

5. Execute the following command to download the Chinese translation package.

   ```Plain Text
   wget -P sites/default/files/translations https://ftp.drupal.org/files/translations/8.x/drupal/drupal-8.7.8.zh-hans.po
   ```
   

6. Modify the Drupal configuration file.

   1. Execute the following command, and press the `i` key to enter the edit mode.

      ```Plain Text
      vim /etc/httpd/conf/httpd.conf
      ```
      

   2. Change the `AllowOverride None` setting in the specified location in the following figure to `AllowOverride All`.

      <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_f17c908f1411a93a38c84cc3dbf99552.png) </span>

   3. Press `Esc`, enter `:wq`, and press Enter to save and exit the file.

7. Execute the following command to modify user permissions on the website root directory.

   ```Plain Text
   chown -R apache:apache /var/www/html/drupal
   ```
   

8. Execute the following command to restart the Apache service.

   ```Plain Text
   systemctl restart httpd
   ```
   


<span id=".56ys5LiJ5q2l77ya5a6J6KOFRHJ1cGFs"></span>
## Step 3: Install Drupal


1. In your local browser, enter `http://<ECS instance EIP>/drupal` to access the Drupal website.

2. Select the installation language, and click the "Save and Continue" button.

3. Select the standard installation method, and click the "Save and Continue" button.

4. Configure the database, enter the database name, username, and password specified in [Step 2: Download and configure Drupal](https://docs.byteplus.com/en/docs/ecs/Building-Drupal-website#.56ys5LqM5q2l77ya5LiL6L295bm26YWN572uRHJ1cGFs). Then, click the "Save and Continue" button.

5. Wait until the website and the translation package are installed. Then, configure the website information based on your business requirements and click the "Save and Continue" button.

6. After the installation is complete, you are automatically logged in to the website. You can specify custom settings for the website based on your business requirements.


<span id=".56ys5Zub5q2l77yI5Y-v6YCJ77yJ77ya5Li6572R56uZ5ZCv55SoIEhUVFBT"></span>
## Step 4 (Optional): Enable HTTPS for the website.

When a user accesses your website over the HTTP protocol, the browser warns the user that the connection is not secure. We recommend that you enable HTTPS secure communication for your website. This ensures encrypted data transmission between users and your website, effectively defending against network hijacking, information leakage, and other threats.

To enable HTTPS, you need to deploy an SSL certificate on your website.
