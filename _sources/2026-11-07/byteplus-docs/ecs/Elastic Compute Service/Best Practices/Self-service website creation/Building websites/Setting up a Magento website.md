---
title: "Setting up a Magento website"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-a-Magento-website"
---

Magento is a professional e\-commerce platform developed with PHP and built on the Zend Framework. It offers a flexible design, modular architecture, and comprehensive feature set, while enabling seamless integration with third\-party applications. It is well\-suited for building online storefronts, including electronic payment platforms.

<span id=".6L2v5Lu254mI5pys"></span>
## Software versions


* Operating system: In the example provided in this topic, CentOS 7.6 is used.

* Composer: A dependency management tool for PHP 5.3 and later. In the example provided in this topic, Composer 1.10.19 is used.

* Magento: In the example provided in this topic, Magento 2.1 is used.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A Linux instance is purchased and a LAMP environment is set up. For more information, see [Setting up a LAMP environment (CentOS 7)](https://docs.byteplus.com/en/docs/ecs/Building-an-LAMP-environment-CentOS-7).

<span id=".56ys5LiA5q2l77ya6YWN572uQXBhY2hl"></span>
## Step 1: Configure Apache


1. Execute the following command, and then press the `i` key to enter the edit mode.

   ```Plain Text
   vim /etc/httpd/conf/httpd.conf
   ```
   

2. Change the parameter setting highlighted in the following figure from `AllowOverride None` to `AllowOverride All`.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_b803c49be97a160e4c40ad66414d5027) </span>

3. Add the following line at the end of the configuration file: `LoadModule rewrite_module modules/ mod_rewrite.so`, as shown in the following figure. Then, press `Esc`, enter `:wq`, and press Enter to exit edit mode.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_8fef628538ad83119aedec71a59331cc) </span>


<span id=".56ys5LqM5q2l77ya6YWN572uUEhQ"></span>
## Step 2: Configure PHP


1. Execute the following command to open the PHP configuration file.

   ```Plain Text
   vim /etc/php.ini
   ```
   

2. Add the configuration for memory limit and time zone at the end of the file:

   ```Plain Text
   The maximum amount of memory that can be allocated to the PHP script. You can adjust the memory limit on demand.
   memory_limit = 1024M
   ; Set the time zone to Shanghai
   date.timezone = Asia/Shanghai                                                        
   ```
   

3. The following figure shows the content of the configuration file after you add the preceding configuration. Press Esc, enter `:wq`, and press Enter to save and close the file.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_312ceec0b133edfe269c0628b9a21328) </span>

4. Execute the following command to install the PHP 7.0 modules required by Magento.

   ```Plain Text
   yum -y install php-pdo php-mysqlnd php-opcache php-xml php-gd php-mcrypt php-devel php-intl php70-mbstring php-bcmath php-json php-iconv php-mbstring php-zip
   ```
   

5. Execute the following command to restart the Apache service.

   ```Plain Text
   systemctl restart httpd
   ```
   


<span id=".56ys5LiJ5q2l77ya6YWN572uTWVnb250b-aVsOaNruW6kw=="></span>
## Step 3: Configure a database for Megonto


1. Remotely connect to and log in to the ECS instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to access the MySQL database as the root user. The password of the root user is the one you specified during MySQL configuration.

   ```Plain Text
   mysql -u root -p
   ```
   

3. Execute the following command to create a database for Megonto.

   ```SQL
   create database database_name;
   ```
   

4. Create a user for the database created for Megonto.

   ```SQL
   create user 'username'@'localhost' identified by 'Password';
   ```
   

5. Grant all permissions to the user.

   ```SQL
   grant all privileges on database name.* to 'username'@'localhost';
   ```
   

6. Execute the following command to make the preceding commands take effect.

   ```SQL
   flush privileges;
   ```
   

7. Execute the following command to exit the MySQL database.

   ```SQL
   exit
   ```
   


<span id=".56ys5Zub5q2l77ya5a6J6KOF5bm26YWN572uQ29tcG9zZXI="></span>
## Step 4: Install and configure Composer

Composer is a dependency management tool for PHP. Composer allows you to declare the code libraries your project depends on and helps you install them into your project.


1. Execute the following command to install the latest version of Composer.

   ```Plain Text
   curl -sS https://getcomposer.org/installer | php
   ```
   

   If the following output is displayed, the installation is successful.

   ```Plain Text
   All settings correct for using Composer
   Downloading...
   
   Composer (version 2.2.18) successfully installed to: /root/composer.phar
   Use it: php composer.phar
   ```
   

2. Execute the following command to configure Composer for global use.

   ```Plain Text
   mv composer.phar /usr/bin/composer
   ```
   

3. Execute the `composer -v` command to check whether Composer is installed successfully.

   If the following output is displayed, the installation is successful.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_83b1c513e54129ec7da755497336acaf.png) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Magento2 depends on Composer 1.x. Make sure that the installed Composer version is 1.x. You can execute the <code>composer self-update 1.10.19</code> command to switch the Composer version. In the example provided in this topic, Composer 1.10.19 is used.   </div>
   

<span id=".56ys5LqU5q2l77ya5a6J6KOF5bm26YWN572uTWFnZW50bw=="></span>
## Step 5: Install and configure Magento

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can install Magento by using different methods and specify whether to install example data.</div>



* <div data-tips="true" data-tips-type="default">If you install Magento only for testing, you can install example data.</div>


* <div data-tips="true" data-tips-type="default">If you install Magento for a production environment, we recommend that you perform a fresh installation of Magento and start the configuration from scratch.</div>


1. Execute the following command to install Git.

   ```Plain Text
   yum -y install git
   ```
   

2. Execute the following commands in sequence to download Magento by using Git.

   ```Plain Text
   cd /var/www/html/
   git clone https://github.com/magento/magento2.git    
   ```
   

3. Execute the following command to switch Magento to the stable version.

   > By default, the command from the previous step installs the latest development version of Magento. We recommend that you switch to the stable version in the production environment. Otherwise, future upgrades cannot be performed.   
   

   ```Plain Text
   cd magento2 && git checkout tags/2.1.0 -b 2.1.0
   ```
   

   If the following output is displayed, the installation is successful.

   ```Plain Text
   Switched to a new branch '2.1.0'
   ```
   

4. Execute the following command to move the installation files to the root directory of the web server.

   ```Plain Text
   shopt -s dotglob nullglob && mv /var/www/html/magento2/* /var/www/html/ && cd ..
   ```
   

5. Execute the following commands in sequence to specify the permissions for Magento files.

   ```Plain Text
   chown -R :apache /var/www/html
   find /var/www/html -type f -print0 | xargs -r0 chmod 640
   find /var/www/html -type d -print0 | xargs -r0 chmod 750
   chmod -R g+w /var/www/html/{pub,var}
   chmod -R g+w /var/www/html/{app/etc,vendor}
   chmod 750 /var/www/html/bin/magento    
   ```
   

6. Execute the following commands separately to install Magento.

   ```Plain Text
   cd /var/www/html/
   composer install --ignore-platform-reqs     
   ```
   

7. Use a browser to access `http://ECS instance EIP/setup`, such as http://180.XX.XX.62/setup. If the following page is displayed, Magento is installed successfully.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_24505d67cc97dfcbf27e9be2aabf0683.png) </span>

8. Configure Magento.

   1. Click the "Agree and Setup Magento" button to start the Magento configuration.

   2. Click the "Start Readiness Check" button to start the environment check. After the check passes, click "Next".

      <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_fa4a0f4c4e73f01dc78f7c3b44b7609c) </span>

9. Specify the MySQL database name, enter the password for the "root" account, and then click "Next".

   > The database name is the one created in the previous [Configure a database for Megonto](https://docs.byteplus.com/en/docs/ecs/Building-a-Magento-website#.56ys5LiJ5q2l77ya6YWN572uTWVnb250b-aVsOaNruW6kw==) section. The password is the password for logging in to the MySQL database as the root account.   
   

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_2ba503e5cfcd6264885f8704dbb226b1) </span>

10. Specify the website access address and the backend management address, such as http://180.XX.XX.62/admin_1h5z9s, and then click "Next".

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_d0b7585d2d4f4d23a69775e7e7026a65) </span>

11. Specify the language, time zone, and currency type, and then click "Next".

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_c365989ccbcc5c488cf6228af80619a4) </span>

12. Create an administrator account, and then click "Next".

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_e711fad3b75f173b47b9591feac07a2a) </span>

13. Click "Install Now" to immediately install the system.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_6080293bf7b46f06308fc3c1fb0a6869) </span>

14. If the following page is displayed, the system is installed successfully.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_60a616283e6cd429124a2d18652ed224) </span>

15. Configure the cron utility to execute scheduled jobs.

   1. Run the `crontab -u apache -e` command to configure a cron job.

   2. Press the `i` key to enter edit mode, add the following content, press Esc, enter `:wq`, and then press Enter to exit edit mode.

      ```Plain Text
      */10 * * * * php -c /etc /var/www/html/bin/magento cron:run
      */10 * * * * php -c /etc /var/www/html/update/cron.php
      */10 * * * * php -c /etc /var/www/html/bin/magento setup:cron:run
      ```
      

16. Use your browser to access `http://ECS instance EIP`, such as http://180.XX.XX.62. The following page is displayed.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_6cb0b1f785fd3f656ac7f7f15b58f1ce) </span>

17. Use a browser to access the Magento backend management address specified in Step 8, such as http://180.XX.XX.62/admin_1h5z9s, and then log in with the admin account and password you configured. If the login is successful, the following page is displayed.

   > If "One or more indexers are invalid. Make sure your Magento cron job is running." is displayed after your login, you can execute the `php bin/magento indexer:reindex` command in the /var/www/html directory.   
   

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_967335bd30862d553c674c7aeac24f64) </span>


<span id=".56ys5YWt5q2l77yI5Y-v6YCJ77yJ77ya6Kej5p6QTWFnZW50b-Wfn-WQjQ=="></span>
## Step 6 (optional): Resolve the Magento domain name

You can configure a domain name for your website, eliminating the need to use a complex, less secure EIP to access it. You can perform the following steps to specify a domain name for the website.


1. Purchase a domain name.

2. Apply for an ICP filing for your domain name.

   If your domain name points to a server located in the Chinese mainland, you need to apply for an ICP filing for your domain name. Otherwise, the website is not accessible.

3. Configure domain name resolution.

   You need to resolve your domain name to the EIP to access your website.

4. After you complete the preceding steps, you can enter `http://<domain name>` in your local browser to access the WordPress website.


<span id=".56ys5LiD5q2l77yI5Y-v6YCJ77yJ77ya5Li6572R56uZ5ZCv55SoIEhUVFBT"></span>
## Step 7 (Optional): Enable HTTPS for the website

When a user accesses your website over the HTTP protocol, the browser warns the user that the connection is not secure. We recommend that you enable HTTPS secure communication for your website. This ensures encrypted data transmission between users and your website, effectively defending against network hijacking, information leakage, and other threats.

To enable HTTPS, you need to deploy an SSL certificate on your website.
