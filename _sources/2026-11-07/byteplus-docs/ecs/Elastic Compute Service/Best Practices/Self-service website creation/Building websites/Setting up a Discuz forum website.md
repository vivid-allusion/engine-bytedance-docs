---
title: "Setting up a Discuz forum website"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-a-Discuz-forum"
---

Discuz is one of the most mature and widely adopted forum software systems in the world. It can be deployed on an ECS instance that supports Apache and MySQL databases to create your own website. This topic describes how to set up a Discuz forum website on a Linux instance.

<span id=".6L2v5Lu254mI5pys"></span>
### Software versions


* Operating system: In the example provided in this topic, CentOS 7.6 is used.

* Apache: A web server with stable performance. In the example provided in this topic, Apache 2.4.6 is used.

* MySQL/MariaDB: A database management system. In the example provided in this topic, MySQL 14.14 is used.

* PHP: A server\-side scripting language embedded in HTML documents. In the example provided in this topic, PHP 7.0.33 is used.

* Discuz: In the example provided in this topic, Discuz! 3.4 is used.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A Linux instance is purchased and a LAMP environment is set up. For more information, see [Setting up a LAMP environment](https://docs.byteplus.com/en/docs/ecs/Building-an-LAMP-environment-CentOS-7).

<span id=".56ys5LiA5q2l77ya5pCt5bu6RGlzY3V6572R56uZ"></span>
## Step 1: Set up a Discuz website


1. Execute the following command to download the Discuz installation package. Log in to the [Gitee official website](https://gitee.com/Discuz/DiscuzX/attach_files) to obtain the Discuz download address, and replace the link in the following `wget` command.

   ```Plain Text
   yum install git
   wget https://gitee.com/Discuz/DiscuzX/attach_files/XXX/download
   ```
   

2. Execute the following command to decompress the Discuz installation package. Replace `download` with the file name from the Discuz download address.

   ```Plain Text
   unzip download
   ```
   

3. Execute the following command to copy the contents of the "upload" folder to the `/var/www/html` directory.

   ```Plain Text
   cp -r upload/* /var/www/html
   ```
   

4. Execute the following command to grant write permission to other users.

   ```Plain Text
   chmod -R 777 /var/www/html
   ```
   

5. Execute the following command to download PHP\-related modules.

   ```Plain Text
   yum -y install php-xml
   ```
   

6. Execute the following command to start the PHP\-FPM service.

   ```Plain Text
   systemctl start php-fpm
   ```
   

7. Execute the following command to restart the Apache service.

   ```Plain Text
   systemctl restart httpd
   ```
   


<span id=".56ys5LqM5q2l77ya55m75b2VRGlzY3V6572R56uZ"></span>
## Step 2: Log in to the Discuz website


1. In the local browser, enter `http://<ECS instance EIP>/` to access the Discuz website.

   If the following output is displayed, Discuz is set up successfully.

2. Click the "I agree" button to enter the installation wizard. Follow the onscreen instructions and click the "Next" button in sequence to go to the "Create database" page, where you can create a database for Discuz.

   Fill in the basic information for the database as shown in the following table. For any information not described in the following table, fill it in based on your business requirements.

   
   |Information |Description |
   |---|---|
   |**Database information** |\-\- |
   |Database server address |In the example provided in this topic, the database and the website are deployed on the same server. Under such circumstances, enter 127.0.0.1 or localhost. |
   |Database name |Specify the name of the database used by Discuz. |
   |Database username/password |Enter root and the password of the root account. |
   |Administrator account/password |Specify the administrator username and password for the Discuz website. |
   

3. Click the "Next" button to complete the installation.

4. Click the "Your forum has been installed. Click here to access the forum" button to enter the forum.

   The following page is displayed. You can use the administrator account and password you specified to log in to the forum.


<span id=".56ys5LiJ5q2l77ya6Kej5p6QRGlzY3V65Z-f5ZCN"></span>
## Step 3: Resolve the Discuz domain name

You can configure a domain name for your website, eliminating the need to use a complex, less secure EIP to access it. You can perform the following steps to specify a domain name for the website.


1. Purchase a domain name.

2. Apply for an ICP filing for your domain name.

   If your domain name points to a server located in the Chinese mainland, you need to apply for an ICP filing for your domain name. Otherwise, the website is not accessible.

3. Configure domain name resolution.

   You need to resolve your domain name to the EIP to access your website.

4. After you complete the preceding steps, you can enter `http://<domain name>` in your local browser to access the Discuz website.


<span id=".56ys5Zub5q2l77yI5Y-v6YCJ77yJ77ya5Li6572R56uZ5ZCv55SoIEhUVFBT"></span>
## Step 4 (Optional): Enable HTTPS for the website.

When a user accesses your website over the HTTP protocol, the browser warns the user that the connection is not secure. We recommend that you enable HTTPS secure communication for your website. This ensures encrypted data transmission between users and your website, effectively defending against network hijacking, information leakage, and other threats.

To enable HTTPS, you need to deploy an SSL certificate on your website.
