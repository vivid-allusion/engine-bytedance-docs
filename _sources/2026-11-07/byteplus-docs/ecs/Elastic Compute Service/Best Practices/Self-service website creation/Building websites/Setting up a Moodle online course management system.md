---
title: "Setting up a Moodle online course management system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-a-Moodla-online-course-management-system"
---

Moodle is a free, feature\-rich open\-source learning management system (LMS) that provides an IT platform to support curriculum design and teaching applications for educational informatization. It delivers a learning environment well\-suited for primary and secondary education.

<span id=".6L2v5Lu254mI5pys"></span>
## Software versions


* Operating system: In the example provided in this topic, CentOS 8.3 is used.

* Apache: A web server with stable performance. In the example provided in this topic, Apache 2.4.37 is used.

* MySQL/MariaDB: A database management system. In the example provided in this topic, MySQL 8.0.26 is used.

* PHP: A server\-side scripting language embedded in HTML documents. In the example provided in this topic, PHP 7.3.20 is used.

* Moodle: In the example provided in this topic, Moodle 3.11.6+ is used.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A Linux instance is purchased and a LAMP environment is set up. For more information, see [Setting up a LAMP environment (CentOS 8)](https://docs.byteplus.com/en/docs/ecs/Building-an-LAMP-environment-CentOS-8).

<span id=".56ys5LiA5q2l77ya5Yib5bu6TW9vZGxl5pWw5o2u5bqT"></span>
## Step 1: Create a database for Moodle


1. Execute the following command to access the MySQL database as the root user. The password of the root user is the one you specified during MySQL configuration.

   ```Plain Text
   mysql -u root -p
   ```
   

2. Execute the following command to create a database for Moodle.

   ```SQL
   create database database_name;
   ```
   

3. Create a user for the database created for Moodle.

   ```SQL
   create user username@'localhost' identified by Password;
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
   


<span id=".56ys5LqM5q2l77ya5LiL6L295bm26YWN572uTW9vZGxl"></span>
## Step 2: Download and configure Moodle


1. Download [Moodle 3.11.6+](https://download.moodle.org/download.php/stable311/moodle-latest-311.zip) to your local device.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can visit <a href="https://download.moodle.org/releases/latest/">the official Moodle website</a> to download the latest Moodle installation package.   </div>
   

2. Upload the local Moodle installation package to the ECS instance. For more information, see [Overview of local data upload](https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview).

3. Execute the following command to decompress the Moodle installation package.

   ```Plain Text
   unzip moodle-latest-311.zip
   ```
   

4. Execute the following command to move the Moodle files to the website root directory.

   ```Plain Text
   mv moodle/ /var/www/html/moodle
   ```
   

5. Execute the following command to enter the website root directory of Moodle.

   ```Plain Text
   cd /var/www/html/moodle
   ```
   

6. Execute the following command to specify write permissions for the `/var/www/` directory.

   ```Plain Text
   chown -R apache: /var/www/
   ```
   

7. Execute the following command to restart the Apache service.

   ```Plain Text
   systemctl restart httpd
   ```
   


<span id=".56ys5LiJ5q2l77ya5a6J6KOFUEhQ5omp5bGV"></span>
## Step 3: Install PHP extensions

Each Moodle release specifies minimum requirements for the PHP version and includes several required PHP extensions. A complete environment check is performed before each installation and upgrade.

In the example provided in this topic, Moodle 3.11.6 is used. You also need to execute the following commands in sequence to install the required PHP extensions.

```Plain Text
yum install php-pecl-zip
yum install php-intl
systemctl restart php-fpm 
```


<span id=".56ys5Zub5q2l77ya5a6J6KOFTW9vZGxl"></span>
## Step 4: Install Moodle


1. Enter `http://<ECS instance EIP>/moodle/install.php` in your local browser to access the Moodle website.

   The following output is displayed.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_87b3b62e1603c90b4d5951196cb68ab5.png) </span>

2. Select the installation language. After you select "English", click the "Next" button.

3. Retain the default value of the path, and click the "Next" button.

4. Retain the default value of the database type, and click the "Next" button.

5. Configure the database. Enter the database name, username, and password specified in [Step 1: Create a database for Moodle](https://docs.byteplus.com/en/docs/ecs/Building-a-Moodla-online-course-management-system#.56ys5LiA5q2l77ya5Yib5bu6TW9vZGxl5pWw5o2u5bqT), and set the port to `3306`. Click the "Save and Continue" button.

6. Confirm the copyright statement, and then click the "Continue" button.

7. Check the installation components, confirm that the minimum requirements have been met, and then click the "Continue" button.

8. Go to the installation system page. When the installation is complete, click the "Continue" button.

9. Enter the account information of the main administrator, and then click the "Update Profile" button.

10. Specify the website homepage and other information, and then click the "Save Changes" button.

11. Go to the website registration page. After the configuration is complete, click the "Register Your Website" button.

12. Click the "Continue" button or visit `http://<ECS instance EIP>/moodle/` to automatically log in to the homepage of the management backend.

   If the following page is displayed, the Moodle online course system is set up. You can manage the website and specify custom settings based on your business requirements.


<span id=".56ys5LqU5q2l77yI5Y-v6YCJ77yJ77ya6Kej5p6Q5Z-f5ZCN"></span>
## Step 5 (Optional): Resolve the domain name

You can configure a domain name for your website, eliminating the need to use a complex, less secure EIP to access it. You can perform the following steps to specify a domain name for the website.


1. Purchase a domain name.

2. Apply for an ICP filing for your domain name.

   If your domain name points to a server located in the Chinese mainland, you need to apply for an ICP filing for your domain name. Otherwise, the website is not accessible.

3. Configure domain name resolution.

   You need to resolve your domain name to the EIP to access your website.

4. After you complete the preceding steps, you can enter `http://<domain name>` in your local browser to access the Moodle website.


<span id=".56ys5YWt5q2l77yI5Y-v6YCJ77yJ77ya5Li6572R56uZ5ZCv55SoIEhUVFBT"></span>
## Step 6 (Optional): Enable HTTPS for the website

When a user accesses your website over the HTTP protocol, the browser warns the user that the connection is not secure. We recommend that you enable HTTPS secure communication for your website. This ensures encrypted data transmission between users and your website, effectively defending against network hijacking, information leakage, and other threats.

To enable HTTPS, you need to deploy an SSL certificate on your website.
