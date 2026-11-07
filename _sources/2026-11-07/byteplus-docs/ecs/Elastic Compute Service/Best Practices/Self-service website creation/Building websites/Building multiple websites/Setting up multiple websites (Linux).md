---
title: "Setting up multiple websites (Linux)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-multiple-websites"
---

You can host multiple websites on a single ECS instance, enabling unified management and resource sharing for small\-scale sites, such as multiple WordPress blogs and static web pages.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* **Web environment deployment**

   An instance is purchased and a web environment is set up. For more information, see [Setting up an LNMP environment (CentOS 7)](https://docs.byteplus.com/en/docs/ecs/Building-an-LNMP-environment-CentOS-7).

* **Software versions**

   * Operating system: In the example provided in this topic, CentOS 7.6 is used.

   * Nginx: A high\-performance, lightweight web server that supports HTTP and reverse proxy. In the example provided in this topic, Nginx 1.20.1 is used.

   * MySQL/MariaDB: A database management system. In the example provided in this topic, MySQL 14.14 is used.

   * PHP: A server\-side scripting language embedded in HTML documents. In the example provided in this topic, PHP 7.0.33 is used.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

This topic describes how to set up two static web pages on an ECS instance running the Linux operating system.

<span id=".5q2l6aqk5LiA77ya6YWN572uTmdpbng="></span>
### Step 1: Configure Nginx


1. Remotely connect to and log in to the ECS instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to view the path of the Nginx configuration file.

   ```Plain Text
   cat /etc/nginx/nginx.conf
   ```
   

   In the following output, the `include` configuration item indicates the path of the file.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/a57315c079204185b9c21db5b13c6fcd.png) </span>

3. Execute the following command to enter the configuration file directory.

   ```Plain Text
   cd /etc/nginx/conf.d
   ```
   

4. Execute the following command to create a new configuration file.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Perform the operation twice to create the configuration files for web page 1 (webtest1) and web page 2 (webtest2), respectively. The following sections use web page 1 (webtest1) as an example.   </div>
   

   1. Execute the following command to create a new configuration file.

      ```Plain Text
      vim webtest1.conf
      ```
      

   2. Press the `i` key to enter edit mode, and then add the following content.

      ```Plain Text
      server {
          listen       80;
          server_name  webtest1.com;    #Type the domain name of web page 1. Use the actual server domain name if you perform this step in a production environment.
      
          #charset koi8-r;
          access_log  /var/log/nginx/b.access.log  main;
      
          location / {
              root   /usr/share/nginx/html/webtest1;    #Type the website root directory of web page 1. Type the project code path if you perform this step in a production environment. The directory is used to store the website information.
              index  index.html index.htm;
          }
      
          #error_page  404              /404.html;
      
          error_page   500 502 503 504  /50x.html;
          location = /50x.html {
              root   /usr/share/nginx/html;
          }
      }
      ```
      

   3. Press `Esc`, enter `:wq`, and then press the `Enter` key to save the file and return to the CLI interface.

5. Execute the following command to start the Nginx service.

   ```Plain Text
   systemctl start nginx
   ```
   


<span id=".5q2l6aqk5LqM77ya5Yib5bu6V2Vi6aG16Z2i"></span>
### Step 2: Create web pages


1. Execute the following command to enter the website root directory of Nginx.

   ```Plain Text
   cd /usr/share/nginx/html
   ```
   

2. Create the website root directories for web pages and configure the website information. The name of the root directory must be the same as the name of the website root directory configured in the Nginx configuration file `***.conf` in Step 1.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Perform the operation twice to create web page 1 (webtest1) and web page 2 (webtest2), respectively. The following sections use web page 1 (webtest1) as an example.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you want to set up a WordPress blog or other websites, create multiple root directories for websites in the <code>/usr/share/nginx/html/</code> directory, and deploy each site in its corresponding root directory.   </div>
   

   1. Create the website root directory for web page 1 (webtest1).

      ```Plain Text
      mkdir webtest1
      ```
      

   2. Go to the website root directory for web page 1 (webtest1).

      ```Plain Text
      cd webtest1
      ```
      

   3. Create a test file.

      ```Plain Text
      vim index.html
      ```
      

   4. Press the `i` key to enter edit mode, and then enter the following content.

      ```Plain Text
      webtest1
      ```
      

   5. Press `Esc`, enter `:wq`, and then press the `Enter` key to save the file and return to the CLI interface.


<span id=".5q2l6aqk5LiJ77ya6K6_6ZeuV2Vi6aG16Z2i"></span>
### Step 3: Access the web page


1. Enter the following address in the local browser to visit web page 1.

   ```Plain Text
   http://<ECS instance's Elastic IP (EIP)>/webtest1/index.html
   ```
   

2. Enter the following address in the local browser to visit web page 2.

   ```Plain Text
   http://<ECS instance's Elastic IP (EIP)>/webtest2/index.html
   ```
   


<span id=".5q2l6aqk5Zub77ya5Li6572R56uZ5ZCv55SoSFRUUFPvvIjlj6_pgInvvIk="></span>
### Step 4: Enable HTTPS for the website (optional)

When a user accesses your website over the HTTP protocol, the browser warns the user that the connection is not secure. We recommend that you enable HTTPS secure communication for your website. This ensures encrypted data transmission between users and your website, effectively defending against network hijacking, information leakage, and other threats.

To enable HTTPS, you need to deploy an SSL certificate on your website.
