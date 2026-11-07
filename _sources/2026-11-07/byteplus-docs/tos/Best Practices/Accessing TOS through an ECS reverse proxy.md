---
title: "Accessing TOS through an ECS reverse proxy"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Use-ecs-instance-to-reverse-proxy-tos"
---

Object Storage TOS is usually accessed through domain names, with dynamically changing service addresses and no fixed IP provided. Certain industries may have security compliance requirements that necessitate accessing Object Storage TOS through a fixed IP. To meet these requirements, you can configure an Nginx reverse proxy server on an ECS instance. By accessing port 80 of the ECS instance's public IP, you can access files in TOS buckets, enabling access to Object Storage TOS resources via a fixed IP. This article introduces the advantages and operation steps of using an ECS instance to reverse proxy TOS.

<span id="202ae894"></span>
## Advantages of the solution

When using an ECS instance to reverse proxy TOS, ECS not only provides a fixed IP access point for Object Storage but also enhances TOS security through its powerful security capabilities, as explained below:


* Fixed IP access: Access resources in Object Storage TOS via a fixed IP to meet security compliance requirements of industries such as finance and healthcare.

* Security enhancement: ECS instances can enable features like WAF and firewall to strengthen access security for Object Storage.

* Log tracking: ECS serves as a unified access point, recording all access logs for TOS, facilitating tracking and auditing.


<span id="5723a11d"></span>
## Prerequisites

ECS instances have been created. For detailed steps, refer to [Purchase instances through the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This article uses an ECS instance with CentOS Stream release 9 64\-bit system as an example to explain how to use an ECS instance to reverse proxy TOS.</div>


<span id="eedf2ef7"></span>
## Step 1: Open port 80

Nginx uses port 80 by default for communication. You need to open port 80 in the security group of the ECS instance to allow users to access TCP port 80.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation bar, select **Instances & Images \> Instances**.

3. On the **Instances** page, click the name of the target instance.

4. On the instance details page, click the **Security Group** tab.

5. Click **Edit Rules** under the **Security Groups** section.

6. On the **Inbound rules** tab, click **Add rule**

7. In the **Add Inbound rule** dialog, configure the following parameters

   
   |**Parameter** |**Description** |
   |---|---|
   |Priority |Priority of the security group rule. |
   |Strategy |Set to **Allow**. |
   |Protocol type |Set to **TCP**. |
   |Port range |Set to port 80.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you need to access the ECS instance using HTTPS protocol, set the port range to 443.</div><br> |
   |Source |Configure the allowed network address range to control which IP addresses can access the ECS instance through port 80. |
   

8. After completing the configuration, click **Add**.


<span id="6ccc1bb6"></span>
## Step 2: Obtain Public IP Address


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance)

2. In the left navigation pane, select **Instances & Images \> Instances**

3. On the **Instances** page, click the name of the target instance

4. On the right side of the **Overview** tab under the **Network information** section, obtain the public IP address


<span id="16908229"></span>
## Step 3: Configure Nginx


1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Run the following command to install Nginx.

   ```Plain
   sudo yum install -y nginx
   ```
   

3. Run the following command to open the Nginx configuration file nginx.conf.

   ```Plain
   sudo vi /etc/nginx/nginx.conf
   ```
   

4. Modify the HTTP module in the nginx.conf configuration file. After completing the changes, save and exit.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you access the ECS instance via HTTPS, configure the HTTPS module in the nginx.conf file. For details, see <a href="https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-install-certificate-on-nginx">Installing an SSL certificate on Nginx</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When configuring Nginx, the system disk generates access and error logs. It is recommended to clean up disk space regularly to prevent excessive log files from degrading cloud server performance.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This configuration method only supports proxying access to one storage bucket.   </div>
   

   ```Plain
   error_log /var/log/nginx/error.log;
   
   events {
       worker_connections 1024;  # The current setting of 1024 is relatively conservative; adjust this parameter flexibly according to business needs in a production environment. 
   }
   
   http {
       log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                         '$status $body_bytes_sent "$http_referer" '
                         '"$http_user_agent" "$http_x_forwarded_for"';
      
   
       access_log  /var/log/nginx/access.log  main;
   
   
       server {
           listen       80;
           listen       [::]:80;
            
           location / {
           proxy_pass http://bucketname.tos-cn-guangzhou.bytepluses.com.cn;
           proxy_set_header Host $http_host;
           proxy_http_version 1.1;
           
           proxy_set_header Connection "";
           proxy_buffering off;
           proxy_request_buffering off;
           }
       }
   }
   ```
   

   Modify the following parameters in the nginx.conf file according to your actual business needs:

   
   |**Parameter** |**Description** |
   |---|---|
   |worker_connections |Maximum concurrent connections. Adjust this value according to your actual business needs. |
   |proxy_pass |The address of the proxy server, which needs to be set as the access domain of the TOS bucket here. Note:<br><br><br>* When the ECS instance and the bucket are in the same region, enter the internal access domain name of the target bucket here, for example, `http://bucketname.tos-cn-guangzhou.ibytepluses.com.cn`<br><br>* When the ECS instance and the bucket are in different regions, enter the external access domain name of the target bucket here, for example, `http://bucketname.tos-cn-guangzhou.bytepluses.com.cn`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can find the bucket domain name on the <strong>Bucket Overview</strong> page. For details, see <a href="https://docs.byteplus.com/docs/tos/docs-bucket-overview">Bucket Overview</a>.</div><br> |
   

5. Run the following command to check the status of the Nginx configuration file nginx.conf.

   ```Plain
   nginx -t
   ```
   

   The following output indicates that the nginx.conf file is in good status.

   ```Plain
   nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
   nginx: configuration file /etc/nginx/nginx.conf test is successful
   ```
   

6. Run the following command to restart the Nginx server and apply the configurations.

   ```Plain
   systemctl restart nginx
   ```
   


<span id="1f2945dd"></span>
## Step four: configure DNS resolution

This article uses the Linux system as an example to explain how to configure DNS resolution on the client side.

Run the following command to open the hosts file.

```Plain
sudo vi /etc/hosts
```


Add the following content at the end of the file to resolve the TOS domain name to the ECS instance’s public IP address.

```Plain
<public IP address> <bucket access domain>
```


The example is as follows:

```Plain
118.125.1**.**  bucketname.tos-ap-southeast-1.bytepluses.com
```


<span id="8f754cc3"></span>
## Result verification


1. Install tosutil. For detailed instructions, refer to [Download and installation](https://docs.byteplus.com/docs/tos/Download-and-install).

2. Run the following command to grant full execution permissions to tosutil.

   ```Plain
   chmod +x tosutil
   ```
   

3. Run the following command to initialize the configuration of tosutil using the `config` command.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you access the ECS instance via HTTPS, set the <code>-e</code> parameter to <code>https://<endpoint></code> when initializing tosutil.   </div>
   

   ```Plain
   # -i specifies the account/subaccount access key
   # -k specifies the account/subaccount secret key
   # -e specifies the endpoint to access
   # -re specifies the region to access
   ./tosutil config -i <access key> -k <secret key> -e http://<endpoint> -re <region>
   ```
   

   Example as follows:

   ```Plain
   ./tosutil config -i AKLTN2FmOGM4Z********* -k WXpkbVlXTm1OVGs1T0RabE********  -e http://tos-cn-guangzhou.bytepluses.com.cn -re cn-guangzhou
   ```
   

4. Execute the following command to upload files to the bucket.

   ```Plain
    ./tosutil cp  span.log tos://bucketname/span.log
   ```
   

5. On the ECS instance, run the following command to view Nginx access logs.

   ```Plain
   tail -f /var/log/nginx/access.log
   ```
   

   The access logs show that file upload requests are forwarded to Nginx, indicating that using the ECS instance to reverse proxy TOS is successful.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97129f434ffe44f19bd907005dd1548e~tplv-goo7wpa0wc-image.image" width="2986px" />   </div>
