---
title: "Configuring proxy servers"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Configuring-a-Proxy-Server"
---

Migration commands of the migration tool Agent must be transmitted over the public network. If your source server cannot connect to the BytePlus platform over the public network, you can create a proxy server that can connect to the public network before migration. This allows the source server to connect to the BytePlus platform via the proxy server.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The proxy server must be able to access the public network and have private network connectivity to the migration source server.

* Additionally, the security group for the migration target must be configured to allow inbound traffic on the ports used by the proxy server. For detailed operations, see [Modifying security group rules](https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

This section uses squid\-cache (Squid) to describe how to configure a proxy server on servers running Linux or Windows.


<Tabs>
<Tab zoneid="cZa6xqPOWR" title="Linux operating system">
<TabTitle>Linux operating system</TabTitle>

In the example provided in this topic, the proxy server running CentOS 7.9 is used.


1. Execute the following command on the proxy server to install Squid.

   ```Plain Text
   yum install -y squid
   ```
   

2. Generate Squid login username and password.

   1. Execute the following command to install the password generation tools.

      ```Plain Text
      yum install -y httpd-tools
      ```
      

   2. Execute the following command to create a directory for storing the password.

      ```Plain Text
      mkdir /etc/squidpwd
      ```
      

   3. Execute the following command to create a Squid user and configure the login password as instructed.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">In the following command, <code>squiduser</code> is the username. Change it to the name you require.      </div>
      

      ```Plain Text
      htpasswd -cd /etc/squidpwd/passwords squiduser
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2fb241f80e15395d71ef7f941352773a.png) </span>

3. Modify the Squid configuration file.

   1. Execute the following command to edit the configuration file.

      ```Plain Text
      vim /etc/squid/squid.conf
      ```
      

   2. Press `i` to enter edit mode and modify the following content.

      * `http_port`: The port on which Squid listens for requests. The default is `3128`.

      * `acl localnet src`: Modify this to the private network IP of the server that needs to access the internet through the proxy server. It is typically set to the private network CIDR block of the migration source server (The specific configuration in the picture below is for reference only).

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_834c574bc9a7380b491c83ea25fb0316.png) </span>

      * Uncomment the `cache_dir` configuration line.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_df04c6c4a8af32a1428aa92edf395d50.png) </span>

      * Add username and password configurations.

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">The path in the red box in the picture below is the path of your generated password file.         </div>
         

         ```Plain Text
         auth_param basic program /usr/lib64/squid/basic_ncsa_auth /etc/squidpwd/passwords
         acl ncsa_users proxy_auth REQUIRED
         http_access allow ncsa_users
         ```
         

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_693174966d98dac04499c97c4508e640.png) </span>

4. Press `Esc` to exit edit mode, enter `:wq`, and press Enter to save the changes and exit.

5. Execute the following command to initialize Squid.

   ```Plain Text
   squid -z
   ```
   

   An output sample is shown in the picture below. Press Enter to continue.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_51b9740cafdecbc9f2ce2bdc939bb760.png) </span>

6. Execute the following commands to start Squid and configure it to start on boot.

   ```Plain Text
   systemctl start squid.service
   systemctl enable squid.service
   ```
   

7. You can execute the following command to view the running status of the Squid service.

   ```Plain Text
   systemctl status squid.service
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5e9ae1cf693ee2d22d5334d368adc453.png) </span>


</Tab>
<Tab zoneid="l5jF8fIZPA" title="Windows operating system">
<TabTitle>Windows operating system</TabTitle>

In the example provided in this topic, the proxy server running Windows Server 2022 is used.


1. On the proxy server, download and install Apache httpd.

   1. To download it, visit the [official Apache website](https://httpd.apache.org/docs/current/platform/windows.html#down).

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_227224c094e17f47ba0cc2a454cc6844.png) </span>

   2. In this practice, a 64\-bit operating system is used as an example. Therefore, download the Win64 version of httpd.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e2a40614bc6aee1652045aead1e575a9.png) </span>

   3. After the download is complete, decompress the package.

2. On the proxy server, download and install Squid.

   1. To download the Squid Windows installation tool, visit the [official Squid website](https://squid.diladele.com/).

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a77abe09cce9b3da84aae04e51d24002.png) </span>

   2. Double\-click `squid.msi` to open the installation program.

   3. Click the "Next" button to start the Squid installation process.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bb3481ea21f2b0b8928c7e8e0b12a0bb.png) </span>

   4. Select "I accept the terms in the License Agreement" and click the "Next" button.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_13d6b0bea3f439b0188da71043a9e9bf.png) </span>

   5. Select the Squid installation path and click the "Next" button.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f7bd9e053f3c269ea7457b985f9d4462.png) </span>

   6. Click the "Finish" button to complete the installation.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5982b386fdb5640b5de98936f226338e.png) </span>

   7. After installation is complete, you can view the Squid tool icon in the lower right corner of the desktop.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_325ffe59aceb1287d136948601c312ef.png) </span>

3. Configure Squid.

   1. Click the Squid tool icon in the lower right corner and select "Stop Squid Service" to stop the Squid service.

   2. Click the Squid tool icon in the lower right corner and select "Open Squid Configuration" to open the Squid configuration file.

   3. In the squid.conf file, modify the following settings:

      * http_port: The port on which Squid listens for requests. The default is `3128`.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_145b10b857823faf0ea832b544ae1136.png) </span>

      * acl: Add the private network IP address of server that needs to access the public network through the proxy server. Where:

         * Replace `Source` with the alias you choose for the source server IP address.

         * Replace `192.168.10.3` with the actual private network IP of the source server, which is typically set to the private network CIDR block of the migration source server.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3c584835f22809f28c879aa8b0c80afd.png) </span>

      * http_access: Before `http_access deny all`, insert a line `http_access allow Source` (Replace `Source` with the alias configured for the source server's private network IP in the `acl` field above).

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f40d80ba97ead4a0c6158d7a96e81a48.png) </span>

      * Add username and password configurations.

         1. Create Squid user and password file.

            1. Execute the following command in Command Prompt.

               <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="5">tip               </div>
               

               * <div data-tips="true" data-tips-type="default" data-wrapper-indent="5">Replace <code>C:\Users\Administrator\Downloads\httpd-2.4.59-240605-win64-VS17\Apache24\bin\httpd</code> with the path to which httpd.exe is downloaded.               </div>
               

               * <div data-tips="true" data-tips-type="default" data-wrapper-indent="5">Replace <code>C:\Squid\passwdfile</code> with the actual path where the password file is stored.               </div>
               

               * <div data-tips="true" data-tips-type="default" data-wrapper-indent="5">Replace <code>squid</code> with the actual username.               </div>
               

               ```Plain Text
               C:\Users\Administrator\Downloads\httpd-2.4.59-240605-win64-VS17\Apache24\bin\htpasswd -c C:\Squid\passwdfile squiduser
               ```
               

            2. Enter the Squid access password as instructed and press Enter to confirm.

               <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_626d6477e3f94e754a919099529a2c14.png) </span>

         2. Add the following content to squid.conf file.

            <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="4">tip            </div>
            

            * <div data-tips="true" data-tips-type="default" data-wrapper-indent="4">Replace <code>C:\Squid\lib\squid\basic_ncsa_auth</code> with the actual path of the Squid built\-in program for Basic Authentication.            </div>
            

            * <div data-tips="true" data-tips-type="default" data-wrapper-indent="4">Replace <code>C:\squid\passwdfile</code> with the actual password file path.            </div>
            

            ```Plain Text
            # Enable Basic Authentication
            auth_param basic program C:\Squid\lib\squid\basic_ncsa_auth C:\squid\passwdfile
            auth_param basic children 5
            auth_param basic realm Squid proxy-caching web server
            auth_param basic credentialsttl 2 hours
            auth_param basic casesensitive off
            
            # Allow Access Control List (ACL)
            acl auth_users proxy_auth REQUIRED
            http_access allow auth_users
            ```
            

4. Press `Ctrl` + `s` to save the changes and close the file.

5. Click the Squid tool icon in the lower right corner and select "Start Squid Service" to start the Squid service.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_12edeeb1a11fc1bc84d588de28de15f3.png) </span>


</Tab>
</Tabs>


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

Configure the proxy server information in the migration tool Agent of the migration source server. For operation details, see [Configuring proxy server information](https://docs.byteplus.com/en/docs/smc/Management-Migration-Tool-Agent#.6YWN572u5Luj55CG5pyN5Yqh5Zmo5L-h5oGv).
