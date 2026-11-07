---
title: "Building an HTTPS static page"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Creating-an-HTTPS-static-page"
---

This article explains how to set up an HTTPS static page to distribute web service traffic to two backend servers for load balancing.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The required Virtual Private Cloud vpc\-01 and subnet subnet\-01 have been created. For more information, see Setting up an IPv4 VPC.

* The security group for Elastic Compute Service (ECS) has opened the TCP protocol for 100.64.0.0/10 CIDR block and the service port (for example, TCP port 80). For more details, refer to Configuring the backend server security group.

* Certificate and private key files have been obtained.


<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedures

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following section only covers essential parameters and their recommended values when configuring each service resource. For all parameters not explicitly discussed, retain the default settings unless otherwise required by your specific use case.</div>


<span id=".5q2l6aqk5LiA77ya5Yib5bu65LqR5pyN5Yqh5Zmo"></span>
### Step 1: create an ECS instance


1. Log in to [the ECS console](https://console.byteplus.com/ecs/instance).

2. Click Create Instance and refer to the table below to complete the basic instance configuration of the ECS.

   
   |Parameter |Explanation |Value |
   |---|---|---|
   |Billing method |Select a billing method for the ECS instance. |Pay\-as\-you\-go |
   |Region and AZ |Select the region and availability zone for the ECS instance. |China (Beijing), Availability Zone A |
   |Flavor |Select the ECS instance type. |General\-purpose g2i |
   |Image |Select the image for the ECS. |Public image, CentOS 7.6 |
   |Storage |Select the storage for ECS. |System disk, ultra\-fast SSD, 40 GiB |
   

3. Click Next: Network and Security, and complete the network and security configuration according to the table below.

   
   |Parameter |Explanation |Value |
   |---|---|---|
   |VPC |Select the Virtual Private Cloud (VPC) where the ECS resides. |vpc\-01 |
   |Subnet |Select the subnet where the ECS resides. |subnet\-01 |
   |EIP |Select whether to associate Elastic IP (EIP). |Select Assign Elastic IP |
   |Security protection |Select the Security Type for the Elastic IP (EIP). |default |
   |ISP |Select the ISP for the EIP. |BGP (multi\-ISP) |
   |Metering method |Select the metering method for the EIP. |Pay\-by\-data\-transfer |
   |Bandwidth cap |Specify the bandwidth cap for the EIP. |5Mbps |
   |Security group |Select the security group associated with the ECS primary network interface. |Default |
   

4. Click Next: Advanced Configuration, and complete the advanced configuration according to the table below.

   
   |Parameter |Explanation |Value |
   |---|---|---|
   |Login credentials |Select login credentials. |Password |
   |Login name |Enter the login name. |root |
   |Login password |Enter the login password. |password@123 |
   |Confirm password |Confirm the login password. |password@123 |
   |Instance name |Enter instance name. |ecs\-[1,2] |
   |Hostname |Enter the hostname. |host\-[1,2] |
   |Instance count |Select the number of hosts. |2 units |
   

5. Click the **Next: confirm order** button to confirm the configuration information of the Elastic Compute Service (ECS) instance.

6. Follow the console guidance to review and accept Legal.

7. Click **Buy now** to redirect to the purchase submitted page.

8. Click the **Go to console** button to navigate to the Instances page and view the newly created ECS instances ecs\-01 and ecs\-02.


<span id=".5q2l6aqk5LqM77ya5pCt5bu65ZCO56uv5pyN5Yqh"></span>
### Step two: set up backend services

Deploy Nginx on the ECS instances and edit the HTML pages to achieve the following: when accessing ecs\-01, return a page titled Welcome to CLB Page One!, when accessing ecs\-01, return a page titled Welcome to CLB Page Two!. Procedures:


1. Log in to the ECS instance. For details, see [log in to Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Install Nginx on the ECS instance.

   1. Run the following command to install Nginx.

      `yum install -y nginx`

   2. Run the following command to check the installed version of Nginx.

      `nginx -v`

      The echo is shown in the figure below. The Nginx version installed in this example is 1.20.1.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ca7bd08210635778482a2a8e03f090b0.png) </span>

   3. Run the following command to start nginx.

      `systemctl start nginx.service`

   4. Run the following command to check the status of Nginx.

      `systemctl status nginx.service`

      The presence of Active (running) in the returned information indicates successful start up of Nginx.

   5. Access http://EIP address of ECS instance using a browser. If the following page displays, it confirms successful Nginx installation.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3415529370b264460d5422f0df48798c.png) </span>

3. Modify the ECS instance's html page.

   1. Run the following command to check the directory of the Nginx configuration file index.html:

      `find / -name index.html`

      The output is shown below. In this example, the Nginx configuration file index.html is located in the /usr/share/nginx/html directory.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a353d1c6c8e58512d1b84d1e4bcef96b.png) </span>

   2. Run the following command to open the index.html page:

      `vi /usr/share/nginx/html/index.html`

   3. Press i to enter the editing mode to modify the index.html page.

      * For the ecs\-01 instance, replace the content of the web page with the following:

         ```Plain Text
         <div id="content">
         
                 <h1>Welcome to CLB Page One!</h1>
         
                 <h2>This page is used for test.</h2>
         
         </div>
         ```
         

      * For the ecs\-02 instance, replace the content of the web page with the following:

         ```Plain Text
         <div id="content">
         
                 <h1>Welcome to CLB Page Two!</h1>
         
                 <h2>This page is used for test.</h2>
         
         </div>
         ```
         

   4. Press Esc key to exit the editing mode, then type :wq to save and exit.

4. Verify the Nginx service.

   Access http://EIP of ecs\-01 and http://EIP of ecs\-02 separately via a browser, respectively. If the updated HTML pages display, this verifies the successful modification of the Nginx configuration.

   * The HTML page for ecs\-01 is shown below.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bfd5dcad87bbdac278fb8cffc38f8620.png) </span>

   * The HTML page for ecs\-02 is shown below.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0bccbdb124db2e0ac5cfa00711d56060.png) </span>


<span id=".5q2l6aqk5LiJ77ya5Yib5bu66LSf6L295Z2H6KGh5a6e5L6L"></span>
### Step 3: Create a CLB instance


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. Click Create Load Balancer, and configure related parameters according to the table below.

   
   |Parameter |Explanation |Value |
   |---|---|---|
   |**Basic information** |||
   |Billing method |Select billing method. |Pay\-as\-you\-go |
   |Regions |Select the Region where the CLB resides. |China (Beijing) |
   |Name |Enter the region name. |clb\-01 |
   |**Network Configuration** |||
   |IP version |Select the IP version of CLB. |IPv4 |
   |Network type |Select the network type of the CLB. |Internet |
   |VPC |Select the private network of the CLB. |vpc\-01 |
   |Subnet |Select the subnet to which the CLB instance belongs. |subnet\-01 |
   |IPv4 address |Configure the IPv4 address occupied by the CLB. |Automatic IP assignment |
   |**Associate an EIP** |||
   |ISP |Select the ISP for the EIP. |BGP (multi\-ISP) |
   |Metering method |Select the metering method for the EIP. |Pay\-by\-bandwidth\-cap |
   |Bandwidth cap |Enter the bandwidth limit for the public network IP. |20Mbps |
   |**Instance type** |||
   |Specification |Select the specification of CLB instance. |Small I |
   

3. Follow the console guidance to review and accept Legal.

4. Click Submit Order to navigate to the application submission success page.

5. Click **Go to the console** to navigate to the Instances page and view the newly created instance.


<span id=".5q2l6aqk5Zub77ya5Yib5bu65ZCO56uv5pyN5Yqh5Zmo57uE"></span>
### Step 4: create backend server group


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. Click the instance name clb\-01.

3. On the **Server Group** tab, click **Add Server Group**.

4. Configure the name of the backend server group. In this example, set it to group\-01.

5. Click **Migrate** to complete the action.


<span id=".5q2l6aqk5LqU77ya5re75Yqg5ZCO56uv5pyN5Yqh5Zmo"></span>
### Step 5: Add backend server


1. Click the created Server Group name group\-01.

2. Click **Add server**.

3. Select Normal mode and check the created ECS instances **ecs\-01** and **ecs\-02**.

4. Click Next.

5. Configure the port and weight for the added ECS instances.

   In this example, set the port to 80 and the weight to 100.

6. Click **Migrate** to complete the action.


<span id=".5q2l6aqk5YWt77ya5LiK5Lyg6K-B5Lmm"></span>
### Step 6: Upload certificate


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the left\-side navigation pane, select **Certificate**.

3. Click Upload server certificate, and configure the following arguments.

   
   |Parameter |Explanation |Value |
   |---|---|---|
   |**Basic information** |||
   |Regions |Select the Region where the CLB resides. |China (Beijing) |
   |Name |Enter the name of CLB. |cert\-01 |
   |**Certificate information** |||
   |Certificate type |Select the certificate type. |Server certificate |
   |Public key certificate |Enter the PEM encoding of your public key certificate. |PEM encoding of your public key certificate |
   |Private key certificate |Enter the PEM code of your private key certificate. |PEM encoding of your private key certificate |
   

4. Click **OK** to complete the operation.


<span id=".5q2l6aqk5LiD77ya5re75Yqg55uR5ZCs5Zmo"></span>
### Step 7: Add listener


1. On the Classic Load Balancer (CLB) instance list page, click the instance clb\-01 and then click Configure Listener.

2. Click Add Listener, see the table below to configure protocol & listener arguments.

   
   |Parameter |Explanation |Value |
   |---|---|---|
   |Listener name |Enter the listener name. |listener\-01 |
   |CLB protocol |Select the load balancing protocol. |HTTPS |
   |Listening port |Enter the listening port. |443 |
   |Scheduling algorithm |Select a scheduling algorithm. |Weighted Round Robin (WRR) |
   |Access control |Enable access control. |Disable |
   

3. Keep the timeout at the default value.

4. After completing the configuration, click Next.

5. On the SSL Certificate configuration page, select the created server certificate cert\-01, and then click Next.

6. On the Default Server Group configuration page, select the created backend server group group\-01, and then click Next.

7. On the Health Check configuration page, retain default values of all parameters and click Next.

8. On the Configuration Review page, confirm all settings are correct, then click Confirm to complete the actions.


<span id=".57uT5p6c6aqM6K-B"></span>
## Result verification


1. If the domain name is not registered publicly, follow the steps below to add domain name mapping.

   1. Modify the hosts file on the local PC.

      On the CLB instance list page, locate the EIP of the clb\-01 instance. The CLB domain name must match with the domain name authenticated by the certificate. In this case, www.test.com is used as an example.

      * Windows OS

         1. Open the hosts file under the C:\Windows\System32\drivers\etc directory on the local PC.

         2. At the end, add the EIP address of the CLB instance clb\-01 for www.test.com to map the domain name to the CLB instance's EIP.

         3. Save the above configuration and exit the file.

      * Linux or MacOS operating system

         1. Use the `vi /etc/hosts` command to open the hosts file.

         2. Press `i` to enter edit mode. At the end, add the public IP address of the CLB instance clb\-01 for www.test.com to map the domain name to the created CLB instance clb\-01's public IP.

         3. Press the Esc key to exit edit mode.

         4. Input :wq and press Enter to save the configuration and exit.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0beb233e0ddbce69fe1d94a9bb795eca.png) </span>

   2. In the local PC command line window, run the following command to check if the domain name mapping is successful.

      `ping www.test.com`

      If the ping succeeds, the domain name mapping is successful.

2. Using the browser to access https://www.test.com, the displayed page (as shown in the image below) indicates that the request was forwarded by the CLB instance to the backend Elastic Compute Service (ECS) server ecs\-01, which successfully processed the request normally and returned the requested page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_588558e5e275ef468f431edf296c677e.png) </span>

3. Using the browser to access https://www.test.com again, the displayed page (as shown in the image below) indicates that the request was forwarded by the CLB instance to the backend Elastic Compute Service (ECS) server ecs\-02, which successfully processed the request normally and returned the requested page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_90cd610c2fb52b3481bf5d4fbf9ca656.png) </span>
