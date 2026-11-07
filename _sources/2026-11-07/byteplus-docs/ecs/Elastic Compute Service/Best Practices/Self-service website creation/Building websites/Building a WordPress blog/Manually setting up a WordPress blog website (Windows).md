---
title: "Manually setting up a WordPress blog website (Windows)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Manually_building_a_WordPress_blog_site"
---

WordPress is a blogging platform developed with PHP. It is suitable for building various types of websites, including personal blogs, corporate sites, and e\-commerce platforms. You can set up and run a website on an ECS instance with a web server, PHP, and a database installed.

<span id=".6L2v5Lu254mI5pys"></span>
## Software versions


* Operating system: In the example provided in this topic, Windows Server 2022 is used.

* Web server: In the example provided in this topic, Apache HTTP Server 2.4.58 is used.

* Database: In the example provided in this topic, MySQL 8.0.36 is used.

* Programming language: In the example provided in this topic, PHP 8.3.1 is used.

* WordPress: In the example provided in this topic, WordPress 5.8.1 is used.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A Windows instance is purchased and a web environment is set up. For more information, see [Purchasing instances](https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances) and [Setting up a web environment (Windows)](https://docs.byteplus.com/en/docs/ecs/Manually_build_a_Web_Environment).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572uV29yZFByZXNz5pWw5o2u5bqT"></span>
### Step 1: Configure a database for WordPress


1. Log in to the target Windows instance. For more information, see [Logging in to Windows instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Windows-instance).

2. Click the "Start" icon in the lower\-left corner, and click "MySQL \> MySQL 8.0 Command line Client".

3. In the MySQL command line tool, enter the login password of the `root` account.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_29a3894a8ee2da2b7320669b8a8b57ef.png) </span>

4. Execute the following command to create a database for WordPress.

   > In the command, `wordpress` is the database name. Change it to the name you require.   
   

   ```SQL
   CREATE DATABASE wordpress;
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d1ac580a955c13d0ca96b1d1387b4ed9.png) </span>

5. Execute the following command to grant the user permission to perform operations on the database.

   ```SQL
   GRANT ALL PRIVILEGES ON wordpress.* TO 'yourusername'@'localhost';
   ```
   

   Parameter descriptions:

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |yourusername |The database username you want to use. |root |
   |yourpassword |The login password for the user. |8s1I\*\*\* |
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f7b35d6ab43e87e13174b152b8c25343.png) </span>


<span id=".5q2l6aqk5LqM77ya5a6J6KOFV29yZFByZXNz"></span>
### Step 2: Install WordPress


1. Log in to the target Windows instance. For more information, see [Logging in to Windows instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Windows-instance).

2. In the instance browser, visit [the WordPress download page](https://wordpress.org/download/) and download WordPress.

3. After the download is complete, right\-click the package and select "Extract All(T)...".

4. In the pop\-up window, select a storage path, select the Apache htdocs directory as the extraction location for WordPress, and click the "Extract" button.

   The following figure shows the directory structure after extraction:

5. After extraction is complete, right\-click the wp\-config\-sample.php file in the folder obtained from the extraction and click the "Copy" button. Then, right\-click any blank area in the current folder window and click the "Paste" button to create a copy of the file.

6. Right\-click the copied file, click the "Rename" button, and change the file name to wp\-config.php.

7. Right\-click the wp\-config.php file, select "Open with", and open the configuration file by using Notepad.

   1. In the configuration file, find the database configuration information.

   2. Modify information such as the database name, username, and password.

      Parameter descriptions:

      
      |Parameter |Description |Sample value |
      |---|---|---|
      |DB_NAME |Enter the name of the database created in [Step 1](https://docs.byteplus.com/en/docs/ecs/Manually_building_a_WordPress_blog_site#.5q2l6aqk5LiA77ya6YWN572ud29yZHByZXNz5pWw5o2u5bqT) to specify the database used by WordPress. |wordpress |
      |DB_USER |Enter the name of the account authorized in [Step 1](https://docs.byteplus.com/en/docs/ecs/Manually_building_a_WordPress_blog_site#.5q2l6aqk5LiA77ya6YWN572ud29yZHByZXNz5pWw5o2u5bqT) to specify the user that performs WordPress operations. |root |
      |DB_PASSWORD |The login password of the account. |ssi423\*\*\* |
      |DB_HOST |The address for accessing the database. |localhost |
      

   3. Save and exit the file.

8. Go to the Apache installation directory, right\-click the httpd.conf file in the conf folder, select "Open with", and open the httpd.conf file with Notepad.

   1. Find the `DocumentRoot` parameter and the `Directory` module in the configuration file.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_99bed8937886f8e86378e1cb3bf5fcef.png) </span>

   2. Change the values of the parameter and the module to the website root directory path, and press `Ctrl` +`S`to save the change.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Replace <code>C:/Users/Administrator/Downloads/httpd-2.4.58-win64-VS17/Apache24/htdocs/</code> with the actual path, and replace backslashes <code>\</code> with forward slashes <code>/</code> in the original Windows path.      </div>
      

      ```Plain Text
      C:/Users/Administrator/Downloads/httpd-2.4.58-win64-VS17/Apache24/htdocs/
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d2bcaf1174fcb1bde552d632dbe1b17a.png) </span>


<span id=".5q2l6aqk5LiJ77ya6YWN572uV29yZFByZXNz"></span>
### Step 3: Configure WordPress


1. Log in to the target Windows instance. For more information, see [Logging in to Windows instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Windows-instance).

2. Click the "Start" icon in the lower\-left corner, select "Windows System", right\-click "Command Prompt", and then select "More \> Run as administrator".

3. In the Command Prompt dialog box, execute the following command to enter the directory where the Apache HTTP Server files are located.

   > Replace `httpd-2.4.58-win64-VS17\Apache24\bin` with the actual path to the Apache HTTP Server bin folder after extraction.   
   

   ```Plain Text
   cd httpd-2.4.58-win64-VS17\Apache24\bin
   ```
   

4. Execute the following command to start the server.

   ```Plain Text
   httpd.exe
   ```
   

5. In the address bar of the instance browser, enter the following address and press the Enter key.

   ```Plain Text
   http://localhost/wordpress/
   ```
   

6. Enter the basic information of the website, and then click the "Install WordPress" button.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Site Title |The name of the WordPress website. |WordPress |
   |Username |The username for logging in to the WordPress website. |Test_1 |
   |Password |The password for logging in to the WordPress website. |Logxxxx |
   |Your Email |The email address for receiving notifications. |test@xx.com |
   

7. Click the "Install WordPress" button to install WordPress.

8. After the installation is complete, click the "Log In" button to go to the login page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bfdf35f8381d2cbbff4a4bc475c13ff7.png) </span>

9. Enter the username and password created in Step 6, and then click the "Log In" button to log in to WordPress.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_45a5fd027dcae663530fa652c7426ddc.png) </span>

   You have successfully logged in to your WordPress site.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1d25f6f27c613a7b6d24417362411a5a.png) </span>

10. For future access to WordPress, use the following address.

   * Access the WordPress homepage as a user.

      ```Plain Text
      http://localhost/wordpress/
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8cd0692e22a10803e2ba47675661b59d.png) </span>

   * Log in to the WordPress backend as an administrator.

      ```Plain Text
      http://localhost/wordpress/wp-login.php
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f71e798a5908b8f25a78d67414e8ef89.png) </span>


<span id=".56ys5Zub5q2l77yI5Y-v6YCJ77yJ77ya6Kej5p6QV29yZFByZXNz5Z-f5ZCN"></span>
### Step 4 (Optional): Resolve the WordPress domain name

You can configure a domain name for your website, eliminating the need to use a complex, less secure EIP to access it. You can perform the following steps to specify a domain name for the website.


1. Purchase a domain name.

2. Apply for an ICP filing for your domain name.

   If your domain name points to a server located in the Chinese mainland, you need to apply for an ICP filing for your domain name. Otherwise, the website is not accessible. 

3. Configure domain name resolution.

   You need to resolve your domain name to the EIP to access your website.

4. Modify the Apache configuration file

   1. Go to the Apache installation directory and locate the httpd.conf configuration file in the conf folder.

   2. Right\-click the httpd.conf file, select "Open with", and open the httpd.conf file by using Notepad.

   3. In the configuration file, locate the `ServerName` module and add a domain name parameter.

      > Replace `www.example.com` with your actual domain name.      
      

      ```Plain Text
      ServerName  www.example.com
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_529bc71e337bf4fff7a3dd6b526fc8e4.png) </span>

   4. Press`Ctrl` +`S`to save the changes and exit the file.

   5. Restart the Apache server.

5. Modify the WordPress configuration.

   1. Go to the WordPress management page.

   2. In the directory tree on the left, select "Settings \> General," and change the values of `WordPress Address` and `Site Address(URL)` to your domain name. Click the "Save Changes" button at the bottom of the page to save the changes.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a447f52ceecc67ef4b40ec33f61d0264.png) </span>

6. After you complete the preceding steps, you can access WordPress in your browser by using the domain name.


<span id=".56ys5LqU5q2l77ya5Li6572R56uZ5ZCv55SoSFRUUFPvvIjlj6_pgInvvIk="></span>
### Step 5: Enable HTTPS for the website (optional)

When a user accesses your website over the HTTP protocol, the browser warns the user that the connection is not secure. We recommend that you enable HTTPS secure communication for your website. This ensures encrypted data transmission between users and your website, effectively defending against network hijacking, information leakage, and other threats.

To enable HTTPS, you need to deploy an SSL certificate on your website.
