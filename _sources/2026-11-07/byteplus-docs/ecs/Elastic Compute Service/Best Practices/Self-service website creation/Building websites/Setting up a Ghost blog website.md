---
title: "Setting up a Ghost blog website"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-a-Ghost-blog"
---

Ghost is an outstanding open\-source blog website developed with Node.js. It uses MySQL, SQLite, or PostgreSQL to store data. This topic describes how to set up a Ghost blog website for a production environment on the Linux operating system.

<span id="ctDb2hB7"></span>
## Feature comparison

Compared to Wordpress, Ghost offers advantages such as instant preview, simplicity, and ease of use:


* Architecturally, Ghost is developed by using Node.js, enabling higher concurrency.

* In terms of design, Ghost features a more streamlined interface, native Markdown support, and a writing\-focused environment that minimizes distractions.

* Ghost supports multiple capabilities such as online preview and online writing, facilitating seamless content creation anytime, anywhere.


<span id=".6L2v5Lu254mI5pys"></span>
## Software versions


* Operating system: In the example provided in this topic, Ubuntu 18.04 is used.

* Nginx: A high\-performance, lightweight web server that supports HTTP and reverse proxy. In the example provided in this topic, Nginx 1.14.0 is used.

* MySQL: A database management system. In the example provided in this topic, MySQL 14.14 is used.

* Node.js: A server\-side scripting language embedded in HTML documents. In the example provided in this topic, Node.js 14.18.1 is used.

* Ghost: In the example provided in this topic, Ghost 4.24.0 is used.


<span id=".56ys5LiA5q2l77ya5Yib5bu65paw55So5oi3"></span>
## Step 1: Create a user

The official Ghost website recommends that you do not perform operations directly as the `root` user. Before you set up a Ghost blog website, create a user.


1. Remotely connect to and log in to the ECS instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to create a user.

   Do not use `ghost` as a username. Otherwise, conflicts with Ghost\-CLI may arise. In the example provided in this topic, `ghostuser` is used as the username.

   ```Plain Text
   adduser ghostuser
   ```
   

   The following output is displayed. You need to specify the password and other information for `ghostuser`. If you do not want to specify other information, you can press the Enter key to skip the configuration.

   ```Plain Text
   Enter new UNIX password: 
   Retype new UNIX password: 
   passwd: password updated successfully
   Changing the user information for sxm
   Enter the new value, or press ENTER for the default
   Full Name []: 
   Room Number []: 
   Work Phone []: 
   Home Phone []: 
   Other []: 
   Is the information correct? [Y/n]
   ```
   

3. Execute the following command to add user permissions.

   ```Plain Text
   usermod -aG sudo ghostuser
   ```
   

4. Execute the following command to switch to the `ghostuser` user.

   ```Plain Text
   su - ghostuser
   ```
   

   If the following output is displayed, you are switched to the `ghostuser` user.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_d887b5e606058a2980b6f8a6020087e1.png) </span>


<span id=".56ys5LqM5q2l77ya5a6J6KOFTmdpbng="></span>
## Step 2: Install Nginx


1. Execute the following command to update the software package.

   ```Plain Text
   sudo apt-get update
   sudo apt-get upgrade -y
   ```
   

2. Execute the following command to install Nginx.

   ```Plain Text
   sudo apt-get install -y nginx
   ```
   

3. Execute the following command to view the Nginx version.

   ```Plain Text
   nginx -v
   ```
   

   If the following output is displayed, the installation is successful.

   ```Plain Text
   nginx version: nginx/1.14.0 (Ubuntu)
   ```
   

4. In the local browser, enter `http://<ECS instance EIP>/` to access Nginx.

   If the following output is displayed, Nginx is set up successfully.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/a4fccfd077864ba1a3d19e6782329ee4.png) </span>


<span id=".56ys5LiJ5q2l77ya5a6J6KOFTm9kZS5qcw=="></span>
## Step 3: Install Node.js


1. Execute the following commands in sequence to install Node.js.

   ```Plain Text
   apt install curl
   curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash 
   sudo apt-get install -y nodejs
   ```
   

2. Execute the following command to view the Node.js version.

   ```Plain Text
   node -v
   ```
   

   If the following output is displayed, Node.js is set up successfully.

   ```Plain Text
   v14.18.1
   ```
   


<span id=".56ys5Zub5q2l77ya5a6J6KOFTXlTUUw="></span>
## Step 4: Install MySQL


1. Execute the following command to install MySQL.

   ```Plain Text
   sudo apt-get install -y mysql-server
   ```
   

2. Execute the following command to connect to MySQL.

   ```Plain Text
   sudo mysql
   ```
   

3. Execute the following command to create the database used by Ghost. In the example provided in this topic, `ghostdata` is created.

   ```SQL
   CREATE DATABASE ghostdata;
   ```
   

4. Execute the following command to specify the password for the root account.

   ```SQL
   ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Input the root account Password';
   ```
   

5. Execute the following command to exit MySQL.

   ```SQL
   \q
   ```
   

6. Execute the following command to view the MySQL version.

   ```Plain Text
   mysql -V
   ```
   

   If the following output is displayed, MySQL is set up successfully.

   ```Plain Text
   mysql Ver 14.14 Distrib 5.7.36, for Linux (x86_64) using EditLine wrapper
   ```
   


<span id=".56ys5LqU5q2l77ya5a6J6KOF5bm26YWN572uR2hvc3Q="></span>
## Step 5: Install and configure Ghost


1. Execute the following command to install the Ghost\-CLI tool.

   ```Plain Text
   sudo npm install ghost-cli@latest -g
   ```
   

2. Execute the following command to create a folder for installing Ghost.

   ```Plain Text
   sudo mkdir -p /var/www/ghost
   ```
   

3. Execute the following command to configure permissions for the `ghostuser` user.

   ```Plain Text
   sudo chown ghostuser:ghostuser /var/www/ghost
   ```
   

4. Execute the following command to enter the Ghost folder.

   ```Plain Text
   cd /var/www/ghost
   ```
   

5. Execute the following command to install Ghost by using Ghost\-CLI.

   ```Plain Text
   ghost install
   ```
   

   The following output is displayed. Complete the configuration in sequence.

   * You can perform simple configurations based on your business requirements. If you want to make changes later, execute the `vi config.production.json` command to open the configuration file and make the necessary changes.

      ```Plain Text
      ? Enter your blog URL: http://www.****.com #The domain name of the Ghost blog.
      ? Enter your MySQL hostname: localhost  #The endpoint of the database. In this example, the database resides on the instance. Therefore, type `localhost`.
      ? Enter your MySQL username: root  #The username of the database. Input root.
      ? Enter your MySQL password: [hidden]  #The password of the database. Type the password of the root user.
      ? Enter your Ghost database name: ghostdata  #The database used by Ghost. Type the name of the database created in step 4.
      ```
      

   * Follow the onscreen instructions to perform operations.


<span id=".56ys5YWt5q2l77ya6K6_6ZeuR2hvc3TljZrlrqI="></span>
## Step 6: Visit the Ghost blog website

Enter the Ghost domain name in your local browser to access the Ghost blog website.

<span id=".56ys5LiD5q2l77yI5Y-v6YCJ77yJ77ya5Li6572R56uZ5ZCv55SoIEhUVFBT"></span>
## Step 7 (Optional): Enable HTTPS for the website

When a user accesses your website over the HTTP protocol, the browser warns the user that the connection is not secure. We recommend that you enable HTTPS secure communication for your website. This ensures encrypted data transmission between users and your website, effectively defending against network hijacking, information leakage, and other threats.

To enable HTTPS, you need to deploy an SSL certificate on your website.
