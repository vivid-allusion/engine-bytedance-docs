---
title: "Creating an HTTP static page"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Creating-an-HTTP-static-page"
---

This section describes how to create an HTTP static page to distribute the traffic of web services to two backend servers for load balancing.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The required Virtual Private Cloud vpc\-01 and subnet subnet\-01 have been created. For more information, refer to [Setting up an IPv4 VPC](https://docs.byteplus.com/en/docs/vpc/Building-an-IPv4-VPC).

* The security group for Elastic Compute Service (ECS) has opened the TCP protocol for `100.64.0.0/10` CIDR block and the service port (for example, TCP port 80). For more details, refer to [Configuring the backend server security group](https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group).


<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following only describes the parameters required for service resource configuration and their values. For other parameters, retain the default values.</div>


<span id=".5q2l6aqk5LiA77ya5Yib5bu65LqR5pyN5Yqh5Zmo"></span>
### Step one: create an Elastic Compute Service (ECS)


1. Log in to[ the ECS console](https://console.byteplus.com/ecs/instance). 

2. Click **Create Instance**, and complete the basic configuration of the ECS instances by referring to the table below.

   
   |Name |Valid Value |
   |---|---|
   |Billing methods |Pay\-as\-you\-go |
   |Region and AZ |North China (Beijing), Availability Zone A |
   |Instance Type |General\-purpose g2i |
   |Image |Public Image CentOS 7.6 |
   |Storage |Root Volume, ESSD, 40 GiB |
   

3. Click **Next: Network and Security**, and complete the network and security configuration by referring to the table below.

   
   |Name |Valid Value |
   |---|---|
   |Virtual Private Cloud |vpc\-01 |
   |Subnet |subnet\-01 |
   |Elastic IP |Select **Assign Elastic IP** |
   |Security |Default |
   |ISP |BGP (multi\-line) |
   |Billing rule |Pay\-by\-data\-transfer |
   |Bandwidth cap |5 Mbps |
   |Security group |Default |
   

4. Click **Next: Advanced Configuration**, and complete the advanced configuration by referring to the table below.

   
   |Name |Valid Value |
   |---|---|
   |Login credentials |Password |
   |Login name |root |
   |Login password |password@123 |
   |Confirm Password |password@123 |
   |Instance name |ecs\-[1,2] |
   |Hostname |host\-[1,2] |
   |Quantity |2 |
   

5. Click **Next: Confirm Order**, and confirm the configuration information of the ECS instance.

6. Please refer to the console guidance to review and Confirm the related Legal.

7. Click **Buy now** to be redirected to a page indicating that your application has been successfully submitted.

8. Click **Go to Console** to navigate to the instance list page to view the newly created ECS instances ecs\-01 and ecs\-02.


<span id=".5q2l6aqk5LqM77ya5pCt5bu65ZCO56uv5pyN5Yqh"></span>
### Step Two: Set up backend services

Deploy Nginx on the ECS instances and edit the HTML pages to achieve the following: when accessing ecs\-01, return a page titled **Welcome to CLB Page One!** , when accessing ecs\-01, return a page titled **Welcome to CLB Page Two!** . The procedure is as follows:


1. Log in to an ECS instance by referring to [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Logging in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Install Nginx on the ECS.

   1. Run the following command to update the PHP source in Yum:

      `rpm -ivh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm`

   2. Run the following command to install Nginx:

      `yum install -y nginx`

   3. Run the following command to check the version of the installed Nginx:

      `nginx -v`

      The output is shown below. In this example, the Nginx version installed is 1.20.1.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1a4eba31ff6ed560d3f3880008d77780.png) </span>

   4. Run the following command to start Nginx:

      `systemctl start nginx.service`

   5. Run the following command to check the Nginx status:

      `systemctl status nginx.service`

      The presence of **Active (running)**  in the returned information indicates successful start up of Nginx.

   6. Access `http://EIP address of ECS instance` using a browser. If the following page displays, it confirms successful Nginx installation.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fd594d54a78c6a738370c0a0c14def5.png) </span>

3. Modify the HTML page of the ECS instance.

   1. Run the following command to check the directory of the Nginx configuration file index.html:

      `find / -name index.html`

      The output is shown below. In this example, the Nginx configuration file index.html is located in the `/usr/share/nginx/html` directory.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_65416472a0ec9048665b7137de80d4d6.png) </span>

   2. Run the following command to open the index.html page:

      `vi /usr/share/nginx/html/index.html`

   3. press`i`Enter the editing mode to modify the index.html page.

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
         

   4. Press `Esc` key to exit the editing mode, then input `:wq` to save and exit.

4. Verify the Nginx service.

   Access` http://EIP of ecs-01` and` http://EIP of ecs-02` separately via a browser, respectively. If the updated HTML pages display, this verifies the successful modification of the Nginx configuration.

   * The HTML page for ecs\-01 is shown below.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5094af2034fa800bfe4f95580fdab222.png) </span>

   * The HTML page for ecs\-02 is shown below.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_112bebb41596f5d7e29096265e59d943.png) </span>


<span id=".5q2l6aqk5LiJ77ya5Yib5bu66LSf6L295Z2H6KGh5a6e5L6L"></span>
### Step 3: Create a CLB instance


1. Log in to[ the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. Click **Create Classic Load Balancer**.

3. Refer to the table below for configuration related arguments.

   
   |Name |Valid Value |
   |---|---|
   |**Basic information** |\-\- |
   |Billing methods |Pay\-as\-you\-go |
   |Region |China (Beijing) Zone 2 |
   |Term |clb\-01 |
   |**Network Configuration** |\-\- |
   |IP Address Version |IPv4 |
   |Network Type |Internet |
   |Virtual Private Cloud |vpc\-01 |
   |Subnet |subnet\-01 |
   |IPv4 address |Automatic IP assignment |
   |**Associating EIP** |\-\- |
   |ISP |BGP (multi\-line) |
   |Billing rule |Pay\-by\-data\-transfer |
   |Bandwidth cap |20Mbps |
   |**Instance specification** |\-\- |
   |Type |small_1 |
   

3. Please refer to the console guidance to review and Confirm the related Legal.

4. Click **Submit Order** to be redirected to the application submission success page.

5. Click **Go to Console** to navigate to the instances page and view the newly created instance.


<span id=".5q2l6aqk5Zub77ya5Yib5bu65ZCO56uv5pyN5Yqh5Zmo57uE"></span>
### Step 4: Create a backend server group


1. Log in to[ the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. Click the CLB instance name clb\-01.

3. On the **Server Group** tab, click **Create Server Group**.

4. Configure the name of the backend server group. In this example, set it to group\-01.

5. Click **OK** to complete the action.


<span id=".5q2l6aqk5LqU77ya5re75Yqg5ZCO56uv5pyN5Yqh5Zmo"></span>
### Add a backend server


1. Click the name of the created backend server group group\-01.

2. Click **Add Server**.

3. Select the normal mode and select the created ECS instances ecs\-01 and ecs\-02.

4. Click **Next**.

5. Configure the port and weight for the added ECS instance.

   In this example, the port is set to 80 and the weight is set to 100.

6. Click **Confirm** to complete the action.


<span id=".5q2l6aqk5YWt77ya5re75Yqg55uR5ZCs5Zmo"></span>
### Add a listener


1. On the CLB instance list page, click **Configure Listener** to the right of the CLB instance clb\-01.

2. Click **Add Listener**. Refer to the table below to configure the protocol and listening parameters.

   
   |Name |Valid Value |
   |---|---|
   |Listener name |listener\-01 |
   |CLB protocol |HTTP |
   |Listening port |80 |
   |Scheduling algorithm |Weighted Round Robin (WRR) |
   |IAM |Disable |
   

3. The timeout period remains unchanged.

4. After completing the configuration, click **Next**.

5. On the **Default Server Group** configuration page, select the created backend server group group\-01, then click **Next**.

6. On the **Health Check** page, retain default values of all arguments, and click **Next**.

7. On the **Configuration Review** page, confirm all settings are correct, and click **Confirm** to complete the action.


<span id=".57uT5p6c6aqM6K-B"></span>
## Result verification

Before verification, view and record the EIP of instance clb\-01 on the CLB instance list page.


1. When accessing `http://EIP of clb-01` through a browser, the page shown in the following figure appears. This indicates that this access request has been forwarded by the CLB instance to the backend Elastic Compute Service (ECS) ecs\-01, which successfully processed the request and returned the page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2a17612ae948cce261e55b04cf813c2e.png) </span>

2. When accessing `http://EIP of clb-01` through a browser again, the page shown in the following figure appears. This indicates that this access request has been forwarded by the CLB instance to the backend Elastic Compute Service (ECS) ecs\-02, which successfully processed the request and returned the page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_32c433384cff5f5aea6b67486c72778f.png) </span>
