---
title: "Obtaining client source IP via backend server"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Configuring-back-end-servers-for-retrieving-client-IP-addresses"
---

This topic describes how a backend server obtains the source IP address of a client accessing an Application Load Balancer (ALB).

<span id=".5Z-65pys5Y6f55CG"></span>
## **Basic principles**


* ALB listeners (HTTP and HTTPS listeners) can obtain the client's real IP address by configuring the backend server to use X\-Forwarded\-For.

* The real IP address of the client will be inserted into the X\-Forwarded\-For field of the HTTP header by the ALB. The first IP address in this field is the real client source IP. The specific format is as follows: `X-Forwarded-For: client-real-IP, proxy-server-1-IP, proxy-server-2-IP, ...`


<span id=".6YWN572u5q2l6aqk"></span>
## **Configuration procedures**

<span id=".5pON5L2c57O757uf"></span>
### **Operating system**

This topic uses CentOS 7.6 as an example. You can replace it as needed with CentOS 7.9, veLinux 1.0 (CentOS compatible), or other CentOS 7 series images.​

<span id=".d2Vi5bqU55So5pyN5Yqh5Zmo57G75Z6L"></span>
### Web server types

Follow the appropriate configuration steps based on your Web server type configured on the backend server. This topic provides the following two types of web servers:


* Nginx: A high\-performance, lightweight web server for HTTP and reverse proxy. This topic uses Nginx 1.17.0 as an example.

* Apache: A stable and reliable web server, using Apache 2.4.6 as an example in this topic.


<span id=".6YWN572ubmdpbnjmnI3liqHlmag="></span>
### **Configure a Nginx server**


1. Access the target backend server based on [Logging on to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Run the following commands in order to install the http_realip_module.

   `yum -y install gcc pcre pcre-devel zlib zlib-devel openssl openssl-devel`

   `wget https://nginx.org/download/nginx-1.17.0.tar.gz`

   `tar zxvf nginx-1.17.0.tar.gz`

   `cd nginx-1.17.0`

   `./configure --prefix=/path/server/nginx --with-http_stub_status_module --without-http-cache --with-http_ssl_module --with-http_realip_module`

   `make`

   `make install`

3. Run the following command to open the nginx.conf file.

   `vi /path/server/nginx/conf/nginx.conf`

4. Press `i` to enter edit mode, then add the new configuration fields and information after the server configuration below.

   ```Plain
   server {
           listen 80;
           server_name localhost;
   ```
   

   Configuration fields and information to add:

   ```Plain
   set_real_ip_from  100.64.0.0/10;
   real_ip_header X-Forwarded-For;
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can add the proxy server’s network CIDR block into set_real_ip_from <IP_cidr\> to obtain the IP address of the proxy server. For example, add the IP address range used by the ALB (100.64.0.0/10). This range is reserved exclusively for the ALB and cannot be assigned to other users, eliminating any potential security risks.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Separate multiple IP address ranges with commas (,).   </div>
   

5. Press ESC to exit edit mode.

6. Type :wq to save and exit the file.

7. Run the following command to start Nginx.

   `/path/server/nginx/sbin/nginx`

8. Run the following command to view Nginx access logs and obtain the real client IP.

   `cat /path/server/nginx/logs/access.log`


<span id=".6YWN572uYXBhY2hl5pyN5Yqh5Zmo"></span>
### **Configure an Apache server**


1. Access the target backend server based on [Logging on to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Run the following command to check the Apache version.

   `httpd -v`

   The following output indicates that the Apache version is 2.4.6.​

   ```Plain
   Server version: Apache/2.4.6 (CentOS)
   Server built:   Mar 24 2022 14:57:57
   ```
   

3. Run the following command to open the httpd.conf file.

   `vi /etc/httpd/conf/httpd.conf`

4. Press `i` to enter edit mode, modify the log format, and add the related configuration information at the end of the file.

   * Modifications on the log format are as follows:

   ```Plain
   LogFormat "%{X-Forwarded-For}i %h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\"" combined    #在原内容中添加配置%{X-Forwarded-For}i
   CustomLog "logs/access_log" common  #去掉此行配置前的注释符#：
   ```
   

   * Configuration fields and information to append:

   ```Plain
   LoadModule remoteip_module modules/mod_remoteip.so
   RemoteIPHeader X-Forwarded-For
   RemoteIPInternalProxy 100.64.0.0/10
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can add the proxy server’s network CIDR block into RemoteIPInternalProxy <IP_cidr\> to obtain the IP address of the proxy server. For example, add the IP address range used by the ALB (100.64.0.0/10). This range is reserved exclusively for the ALB and cannot be assigned to other users, eliminating any potential security risks.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Separate multiple IP address ranges with commas (,).   </div>
   

5. Press ESC to exit edit mode.

6. Type :wq to save and exit the file.

7. Run the following command to restart Apache.

   `systemctl restart httpd`

8. Run the following command to view Apache access logs and obtain the real client IP.

   `cat /etc/httpd/logs/access_log`
