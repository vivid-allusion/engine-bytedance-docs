---
title: "Setting up a Joomla basic management platform"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-a-Joomla-basic-management-platform"
---

Joomla is an open\-source content management system that allows you to build personal websites, enterprise websites, or powerful online applications on ECS instances that support PHP and MySQL databases.

<span id=".6L2v5Lu254mI5pys"></span>
## Software versions


* Operating system: In the example provided in this topic, CentOS 7.8 is used.

* Apache: A web server with stable performance. In the example provided in this topic, Apache 2.4.6 is used.

* MySQL/MariaDB: A database management system. In the example provided in this topic, MySQL 14.14 is used.

* PHP: A server\-side scripting language embedded in HTML documents. In the example provided in this topic, PHP 7.0.33 is used.

* Joomla: In the example provided in this topic, Joomla 3.6.0 is used.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A Linux instance is purchased and a LAMP environment is set up. For more information, see [Setting up a LAMP environment (CentOS 7)](https://docs.byteplus.com/en/docs/ecs/Building-an-LAMP-environment-CentOS-7).

<span id=".56ys5LiA5q2l77ya5Yib5bu6Sm9vbWxh5pWw5o2u5bqT"></span>
## Step 1: Create a Joomla database


1. Execute the following command to access the MySQL database as the root user. The password of the root user is the one you specified during MySQL configuration.

   ```Plain Text
   mysql -u root -p
   ```
   

2. Execute the following command to create a database for Joomla.

   ```SQL
   create database database_name;
   ```
   

3. Create a user for the database created for Joomla.

   ```SQL
   create user 'username'@'localhost' identified by 'Password';
   ```
   

4. Grant all permissions to the user.

   ```SQL
   grant All permissions on the database.* to 'username'@'localhost';
   ```
   

5. Execute the following command to make the preceding commands take effect.

   ```SQL
   flush privileges;
   ```
   

6. Execute the following command to exit the MySQL database.

   ```SQL
   exit
   ```
   


<span id=".56ys5LqM5q2l77ya5LiL6L295bm26YWN572uSm9vbWxh"></span>
## Step 2: Download and configure Joomla


1. Execute the following command to download the Joomla installation package. In the example provided in this topic, Joomla 3.6.0 is downloaded.

   ```Plain Text
   wget https://github.com/joomla/joomla-cms/releases/download/3.6.0/Joomla_3.6.0-Stable-Full_Package.zip
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also visit the <a href="https://github.com/joomla/joomla-cms/releases/">Joomla code repository</a> to download installation packages for other versions.   </div>
   

2. Execute the following command to move the installation package to the website root directory.

   ```Plain Text
   mv Joomla_3.6.0-Stable-Full_Package.zip /var/www/html/
   ```
   

3. Execute the following command to enter the website root directory.

   ```Plain Text
   cd /var/www/html/
   ```
   

4. Execute the following command to decompress the installation package.

   ```Plain Text
   unzip Joomla_3.6.0-Stable-Full_Package.zip
   ```
   

5. Execute the following command to change directory permissions.

   ```Plain Text
   chown -R apache:apache /var/www/html/
   ```
   

6. Execute the following command to restart the httpd service.

   ```Plain Text
   systemctl restart httpd.service
   ```
   


<span id=".56ys5LiJ5q2l77ya5a6J6KOFSm9vbWxh"></span>
## Step 3: Install Joomla


1. Enter `http://<ECS instance EIP>/` in your local browser to access the Joomla website.

   If the following output is displayed, the Joomla website is set up successfully.

2. Select a language, enter the configuration information, and click the "Next" button.

3. Configure the database, enter the database name, username, and password specified in [Step 1: Create a database for Joomla](https://docs.byteplus.com/en/docs/ecs/Building-a-Joomla-basic-management-platform#.56ys5LiA5q2l77ya5Yib5bu6Sm9vbWxh5pWw5o2u5bqT), and click the "Next" button.

4. Confirm the configuration information and click the "Install" button.

5. After the installation is complete, click "Delete installation directory" to delete the installation directory.

6. At this point, the Joomla basic management platform is set up.

   * Click the "Website" button or visit `http://<ECS instance EIP>/` to access the Joomla homepage.

      <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_a5394cc48856eba8cc0099c9c8cb1e7b.png) </span>

   * Click "Backend management" or visit `http://<ECS instance EIP>/administrator` to access the Joomla backend management page.

      <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_15d7c75be5e4233618a58477ca32733b.png) </span>


<span id=".56ys5Zub5q2l77yI5Y-v6YCJ77yJ77ya6Kej5p6Q5Z-f5ZCN"></span>
## Step 4 (Optional): Resolve the domain name

You can configure a domain name for your website, eliminating the need to use a complex, less secure EIP to access it. You can perform the following steps to specify a domain name for the website.


1. Purchase a domain name.

2. Apply for an ICP filing for your domain name.

   If your domain name points to a server located in the Chinese mainland, you need to apply for an ICP filing for your domain name. Otherwise, the website is not accessible.

3. Configure domain name resolution.

   You need to resolve your domain name to the EIP to access your website.

4. After you complete the preceding steps, you can enter `http://<domain name>` in your local browser to access the WordPress website.


<span id=".56ys5LqU5q2l77yI5Y-v6YCJ77yJ77ya5Li6572R56uZ5ZCv55SoIEhUVFBT"></span>
## Step 5 (Optional): Enable HTTPS for the website

When a user accesses your website over the HTTP protocol, the browser warns the user that the connection is not secure. We recommend that you enable HTTPS secure communication for your website. This ensures encrypted data transmission between users and your website, effectively defending against network hijacking, information leakage, and other threats.

To enable HTTPS, you need to deploy an SSL certificate on your website.
