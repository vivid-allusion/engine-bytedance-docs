---
title: "Getting the client source IP for layer-7 listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Configuring-a-Layer-7-listener-to-obtain-the-client-source-IP-address"
---

This topic introduces how the Layer 7 listener obtains the client source IP address accessing the Classic Load Balancer (CLB) service.

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenarios

The Layer 7 listener of CLB (HTTP/HTTPS protocol) obtains the visitor's real IP address by configuring the backend server using the X\-Forwarded\-For method.

The real IP address of the visitor will be placed by CLB in the X\-Forwarded\-For field of the HTTP header, and the first address in this field is the real IP address of the visitor.

<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedures


<Tabs>
<Tab zoneid="eSLvedOJ0i" title="Configure a Nginx server">
<TabTitle>Configure a Nginx server</TabTitle>

1. Access the target backend server based on Logging on to a Linux instance.

2. Run the following command to install Nginx.

   ```JSON
   yum install -y https://mirrors.ivolces.com/nginx_all/centos/7/x86_64/RPMS/nginx-1.22.0-1.el7.ngx.x86_64.rpm
   ```
   

3. Run the following command to check the Nginx version.

   ```JSON
   nginx -v
   ```
   

   The output below indicates successful installation.

   ```JSON
   nginx version: nginx/1.22.0
   ```
   

4. Run the following command to check the path of the Nginx configuration file, nginx.conf:

   ```JSON
   find / -name nginx.conf
   ```
   

   The output is shown below, indicating that the path of the Nginx configuration file is /etc/nginx/nginx.conf.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7679b6c9e6de071070adf76485020657.png) </span>

5. Run the following commands in sequence to back up the Nginx configuration file in its directory, then open the original Nginx configuration file.

   ```Plain Text
   cd /etc/nginx
   cp nginx.conf nginx.conf.bak
   vi nginx.conf
   ```
   

6. Press it to enter edit mode, then add new configuration fields and details after the following server configuration information.

   ```Plain Text
   server {
       listen 80;
       server_name localhost;
   ```
   

   Configuration fields and information to add:

   ```Plain Text
   set_real_ip_from  100.64.0.0/10;
   real_ip_header X-Forwarded-For;
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can add the proxy server's network CIDR block into set_real_ip_from <IP_cidr\> to obtain the IP address of the proxy server. For example, add the IP address range of the Cloud Load Balancer (100.64.0.0/10 is a reserved address range for the CLB, which cannot be allocated to other users, eliminating any security risks). Separate multiple IP address ranges with commas (,).   </div>
   

7. Press ESC to exit the editing mode, input :wq to save and exit the file.input

8. Run the following command to restart Nginx.

   ```Plain Text
   systemctl restart nginx.service
   ```
   

9. Run the following command to check the path of the Nginx access log file, access.log:

   ```Plain Text
   find / -name access.log
   ```
   

   The output is shown below, indicating that the path of the Nginx access log file is /var/log/nginx/access.log.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1ec4895e181bf3dbc3c27a8e44e29457.png) </span>

10. Run the following command to view the Nginx access log and obtain the real visitor IP.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">cat /var/log/nginx/access.log   </div>
   


</Tab>
<Tab zoneid="DSSCTPVXGB" title="Configure an Apache server">
<TabTitle>Configure an Apache server</TabTitle>

1. Access the target backend server based on Logging on to a Linux instance.

2. Run the following command to install Apache, using Apache 2.4.6 as an example.

   ```JSON
   yum install httpd -y
   ```
   

3. Run the following command to check the Apache version.

   ```JSON
   httpd -v
   ```
   

   The output shown below indicates a successful installation.

   ```Plain Text
   Server version: Apache/2.4.6 (CentOS)
   Server built:   Mar 24 2022 14:57:57
   ```
   

4. Run the following command to start the Apache service.

   ```JSON
   systemctl start httpd
   ```
   

5. Run the following command to set Apache service to start on boot.

   ```JSON
   systemctl enable httpd
   ```
   

6. Run the following command to view the Apache configuration file path.

   ```JSON
   httpd -V
   ```
   

   The output shown below indicates the Apache configuration file path is “/etc/httpd/conf/httpd.conf”.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0a59d9c9378bf228ba7d2166de746acf.png) </span>

7. Run the following command to open the httpd.conf file:

   ```JSON
   vi /etc/httpd/conf/httpd.conf
   ```
   

8. Press i to enter edit mode, modify the log format, and add the related configuration information at the end of the file.

   * Modifications on the log format are as follows:

      ```Plain Text
      LogFormat "%{X-Forwarded-For}i %h %l %u %t "%r" %>s %b "%{Referer}i" "%{User-Agent}i"" combined    //在原内容中添加配置%{X-Forwarded-For}i
      CustomLog "logs/access_log" common  //去掉此行配置前的注释符#
      ```
      

   * Configuration fields and information to append:

      ```Plain Text
      LoadModule remoteip_module modules/mod_remoteip.so
      RemoteIPHeader X-Forwarded-For
      RemoteIPInternalProxy 100.64.0.0/10
      ```
      

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">You can add the proxy server’s network CIDR block into RemoteIPInternalProxy <IP_cidr\> to obtain the IP address of the proxy server. For example, add the IP address range of the Cloud Load Balancer (100.64.0.0/10 is a reserved address range for the Cloud Load Balancer and cannot be assigned to other users, ensuring no security risk). Separate multiple IP address ranges with commas (,).   </div>
   

9. Press ESC to exit the editing mode, input :wq to save and exit the file.input

10. Run the following command to restart Apache.

   ```JSON
   systemctl restart httpd
   ```
   

11. Run the following command to view Apache access logs and obtain the real visitor IP.

   ```JSON
   cat /etc/httpd/logs/access_log
   ```
   





</Tab>
</Tabs>
