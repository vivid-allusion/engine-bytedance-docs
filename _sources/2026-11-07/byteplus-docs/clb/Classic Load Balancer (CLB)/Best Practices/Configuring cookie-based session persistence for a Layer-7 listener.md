---
title: "Configuring cookie-based session persistence for a Layer-7 listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Configuring-cookie-based-sticky-session-for-a-Layer-7-listener"
---

This section describes how to configure the sticky session feature for a Layer 7 listener to ensure that access requests from the same client are forwarded by Cloud Load Balancer (CLB) to the same backend server for processing.

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenarios

The Layer 7 listener of CLB supports the cookie\-based sticky session feature either by **inserting a cookie** or **rewriting a cookie**.


* **Inserting a cookie**: If this method is used, the configuration is simple. You only need to enable the sticky session feature on the CLB console and specify the sticky session timeout.

* **Rewriting a cookie**: If this method is used, you must first configure a cookie on the web server of the backend server, and then enable the sticky session feature and specify the cookie name on the CLB console.


The following takes **rewriting a cookie** as an example to describe how to configure the sticky session feature for a Layer 7 listener.

<span id=".6YWN572u6K-05piO"></span>
## Precautions


* Ensure that the web server, such as Nginx or Apache, has been installed on the backend server.

   * Nginx: A high\-performance lightweight web server for HTTP and reverse proxying, with Nginx 1.20.1 as an example in this section.

   * Apache: a high\-performance web server. In this topic, Apache 2.4.6 is used.

* Ensure that the scheduler **Weighted Round Robin (WRR)**  is used for the Layer 7 listener with sticky session enabled.


<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedure

<span id=".5q2l6aqk5LiA77ya5Li65ZCO56uv5pyN5Yqh5Zmo6YWN572uQ29va2ll"></span>
### Step 1: Configure the Cookie for the backend server

The cookie configuration method varies according to the web server. The following takes Nginx and Apache as examples to describe the cookie configuration procedure.

<span id="Nginx"></span>
#### Nginx


1. Log in to a backend server of the CLB instance by referring to [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Logging in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Run the following command to check the path of the Nginx configuration file:

   ```Plain Text
   find / -name nginx.conf
   ```
   

   The output is the path of the Nginx configuration file, as shown below.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4a039244f8ba785d00e0e7569388ada3.png) </span>

3. Run the following command to back up the configuration file in the configuration file directory.

   ```Plain Text
   cd /etc/nginx
   cp nginx.conf nginx.conf.bak
   ```
   

4. Run the following command to modify the Nginx configuration file:

   ```Plain Text
   vi nginx.conf
   ```
   

5. press`i`Enter edit mode, add the configuration `location` field in the server configuration information, and configure the cookie information.

   ```Plain Text
   ···
   server {
      listen       80;
      listen       [::]:80;
      server_name  localhost;
      location / {
   add_header Set-Cookie backend_server="ecs01";   # Settings cookie, backend_server indicates the cookie name, ecs01 indicates the cookie value
   expires 3600;   # Settings cookie expiration time
          root   html;
   return 200 '$request;$http_host;$server_port;$server_addr';  # Settings response format
          index  index.html index.htm;
      }
   ···
   ```
   

6. Press `ESC` to exit the editing mode, input `:wq` to save and exit the file.input

7. Run the following command to restart Nginx so that the configuration takes effect:

   ```Plain Text
   systemctl restart nginx.service
   ```
   

8. Refer to the above steps to complete the cookie configuration for all backend servers in the backend server group of the CLB instance.


<span id="Apache"></span>
#### Apache


1. Log in to a backend server of the CLB instance by referring to [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Logging in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Run the following command to check the path of the Apache configuration file:

   ```Plain Text
   httpd -V
   ```
   

   The following echo indicates that the path of the Apache configuration file is `/etc/httpd/conf/httpd.conf`.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e23d698a3a0de923893ab7067810a721.png) </span>

3. Run the following command to back up the configuration file in the Apache configuration file directory.

   ```Plain Text
   cd /etc/httpd/conf
   cp httpd.conf httpd.conf.bak
   ```
   

4. Run the following command to modify the Apache configuration file:

   ```Plain Text
   vi httpd.conf
   ```
   

5. press`i`Press  the I key to enter the editing mode, and configure the cookie by adding the following information at the end of the Apache configuration file:

   ```Plain Text
   Header add Set-Cookie "backend_server=ecs01; expires=3600"
   ```
   

6. Press `ESC` to exit the editing mode, input `:wq` to save and exit the file.input

7. Run the following command to restart Apache so that the configuration takes effect:

   `systemctl restart httpd.service`

8. Refer to the above steps to complete the cookie configuration for all backend servers in the backend server group of the CLB instance.


<span id=".5q2l6aqk5LqM77ya5Li65LiD5bGC55uR5ZCs5Zmo5ZCv55So5Lya6K-d5L-d5oyB5Yqf6IO9"></span>
### Step 2: Enable session persistence feature for the Layer 7 listener


1. Log in to[ the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. From the top menu bar, select the project and the region of the target CLB instance.

3. Click Configure Listener to the right of target CLB instance.

4. Click **Edit Listener** to the right of the target listener, configure the sticky session feature .

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Cookie name</strong> here must be consistent with the cookie configuration of the backend server.   </div>
   

5. Click **Confirm** to complete the procedure.


<span id=".5q2l6aqk5LiJ77ya6aqM6K-B5Lya6K-d5L-d5oyB55qE5pyJ5pWI5oCn"></span>
### Step 3: Verifying the sticky session feature


1. Log in to the client.

2. In the command line window, run the following command multiple times and check the returned backend server information:

   ```Plain Text
   curl -v http://EIP of the CLB instance:Listening port
   ```
   

   The backend server information returned multiple times is shown in the figure below. If it contains the `Set-Cookie` field and the returned values are the same, the session remains valid, and access requests from the same client are forwarded to the same backend server.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_164fbb54abb1539963192425a15a34d2.png) </span>
