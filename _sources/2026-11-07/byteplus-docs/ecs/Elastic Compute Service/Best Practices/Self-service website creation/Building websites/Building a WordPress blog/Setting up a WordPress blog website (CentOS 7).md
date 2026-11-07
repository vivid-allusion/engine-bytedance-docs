---
title: "Setting up a WordPress blog website (CentOS 7)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-a-WordPress-blog-CentOS-7"
---

WordPress is a blogging platform developed by using PHP. It can be deployed on an ECS instance that supports PHP and MySQL databases to create your own website or function as a content management system.

<span id=".6L2v5Lu254mI5pys"></span>
### Software versions


* Operating system: In the example provided in this topic, CentOS 7.6 is used. You can also use CentOS 7.9, veLinux 1.0 (CentOS compatible version), or other CentOS 7 series images.

* WordPress: In the example provided in this topic, WordPress 5.8.1 is used.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A Linux instance is purchased and a LAMP or LNMP environment is set up. For more information, see [Setting up a LAMP environment (CentOS 7)](https://docs.byteplus.com/en/docs/ecs/Building-an-LAMP-environment-CentOS-7) and [Setting up an LNMP environment (CentOS 7)](https://docs.byteplus.com/en/docs/ecs/Building-an-LNMP-environment-CentOS-7).

<span id=".56ys5LiA5q2l77ya6YWN572uV29yZFByZXNz5pWw5o2u5bqT"></span>
## Step 1: Configure a database for WordPress


1. Remotely connect to and log in to the ECS instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to access the MySQL/MariaDB database as the root user. The password of the root user is the one you specified during the configuration of MySQL/MariaDB.

   ```Plain Text
   mysql -u root -p
   ```
   

3. Execute the following command to create a database for the WordPress blogging platform.

   ```SQL
   create database database_name;
   ```
   

4. Create a user for the database created for WordPress.

   ```SQL
   create user 'username'@'localhost' identified by 'Password';
   ```
   

5. Grant all permissions to the user.

   ```SQL
   grant all privileges on database name.* to 'Username'@'localhost';
   ```
   

6. Execute the following command to make the preceding commands take effect.

   ```SQL
   flush privileges;
   ```
   

7. Execute the following command to exit the MySQL/MariaDB database.

   ```SQL
   exit
   ```
   


<span id=".56ys5LqM5q2l77ya5pCt5bu6V29yZFByZXNz572R56uZ"></span>
## Step 2: Set up a WordPress website


1. Execute the following command to download WordPress to the website root directory of Nginx. Visit the [official WordPress website](https://cn.wordpress.org/) to obtain the download path.

   ```Plain Text
   cd /var/www/html
   wget https://cn.wordpress.org/wordpress-5.8.1-zh_CN.tar.gz
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>/var/www/html</code> with the website root directory you specified when you set up LNMP or LAMP.   </div>
   

2. Execute the following command to decompress the installation package.

   ```Plain Text
   tar -vzxf wordpress-5.8.1-zh_CN.tar.gz
   ```
   

3. Modify the WordPress configuration file.

   1. Back up the configuration file in the configuration file directory.

      ```Plain Text
      cd wordpress
      cp wp-config-sample.php wp-config.php
      ```
      

   2. Execute the following command to modify the configuration file.

      ```Plain Text
      vim wp-config.php
      ```
      

   3. Press the `i` key to enter edit mode and modify the following content in the `MySQL` section.

      ```Plain Text
      // ** MySQL settings - You can get this info from your web host ** //
      /** The name of the database for WordPress */
      define('DB_NAME', 'WordPress_database_name');
      
      /** MySQL database username */
      define('DB_USER', 'MySQL_name');
      
      /** MySQL database password */
      define('DB_PASSWORD', 'MySQL_password');
      
      /** MySQL hostname */
      define('DB_HOST', 'localhost');
      ```
      

   4. Press `Esc`, enter `:wq`, and then press Enter to save the modifications and close the file.


<span id=".56ys5LiJ5q2l77ya55m75b2VV29yZFByZXNz572R56uZ"></span>
## Step 3: Log in to the WordPress website


1. Enter `http://<ECS instance EIP>/wordpress` in your local browser to access the WordPress website.

   If the following output is displayed, WordPress is set up successfully.

2. Enter the basic information of the website, and then click the "Install WordPress" button.

   
   |Information |Description |
   |---|---|
   |Site name |The name of the WordPress website. |
   |Username |The username for logging in to the WordPress website. |
   |Password |The password for logging in to the WordPress website. |
   |Your email address |The email address for receiving notifications. |
   

3. Click the "Log in" button.

4. Enter your username and password to log in to the WordPress website.

   The following output is displayed.


<span id=".56ys5Zub5q2l77yI5Y-v6YCJ77yJ77ya6Kej5p6QV29yZFByZXNz5Z-f5ZCN"></span>
## Step 4 (Optional): Resolve the WordPress domain name

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
