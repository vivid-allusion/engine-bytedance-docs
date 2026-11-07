---
title: "Cross-VPC ECS instance as a backend server (Transit Router)"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Combining-with-the-TR-service-to-use-an-ECS-instance-in-a-VPC-as-the-cross-VPC-server"
---

This section describes how to integrate the Classic Load Balancer (CLB) service with the TransitRouter (TR) service to implement the load balancing capability of an Elastic Compute Service (ECS) instance that is located in one Virtual Private Cloud (VPC) but acts as the backend server of a CLB instance in another VPC.

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenarios

CLB can integrate with CEN to forward access requests to the Elastic Compute Service (ECS) instances across VPCs for further processing. Example as shown below:

> The information marked in the figure is for reference only. Please modify the relevant information according to the actual network planning.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_717ff6265e47d9c36dbe22aadf4928b9.png) </span>

All resources in the above diagram belong to the China (Beijing) Region, and other data in the diagram are explained as follows:


* Private Virtual Private Cloud vpc\-01: The subnet CIDR block is `172.16.1.0/24`; The private IP address of the Elastic Compute Service (ECS) ecs\-01 is `172.16.1.10`.

* Classic Load Balancer clb\-01: The private IP address is `172.16.1.20`, and the Elastic IP (EIP) address is `12.XX.XX.89`.

* Virtual Private Cloud (VPC) vpc\-02: The CIDR block of the subnet is `192.168.1.0/24`. The private IP address of the Elastic Compute Service (ECS) instance ecs\-02 is `192.168.1.10`.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The creation of vpc\-01, vpc\-02, and their subnets is complete. For more information, refer to [Setting up an IPv4 VPC](https://docs.byteplus.com/en/docs/vpc/Building-an-IPv4-VPC).

* The creation of ecs\-01 and ecs\-02 is complete, and the configuration of backend service of ecs\-02 is complete. For more information, refer to [Purchasing ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) and [Creating the backend service](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTP-static-page#.5q2l6aqk5LqM77ya5pCt5bu65ZCO56uv5pyN5Yqh).


<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following only describes the parameters required for service resource configuration and their values. For other parameters, retain the default values.</div>


<span id=".5q2l6aqk5LiA77ya5Yib5bu66LSf6L295Z2H6KGh5a6e5L6L"></span>
### Step 1: Create CLB instance


1. Log in to[ the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. Click **Create Classic Load Balancer**.

3. Refer to the table below for configuration related arguments.

   
   |Name |Explaination |Valid Value |
   |---|---|---|
   |**Basic information **  |||
   |Billing methods |Select a billing method for the CLB instance. |Pay\-as\-you\-go |
   |Region  |Select a region to deploy the CLB instance. |China (Beijing) |
   |Term |Type the name of the CLB instance. |clb\-01 |
   |**Network Configuration** |||
   |IP Address Version |Select the IP version of the CLB instance. |IPv4 |
   |Network Type |Select the network type of the CLB instance. |Internet  |
   |Virtual Private Cloud |Select the VPC where the CLB instance resides. |vpc\-01 |
   |subnet |Select the subnet where the CLB instance resides. |subnet\-01 |
   |IPv4 address |Select the allocation method for the private IPv4 address of the CLB network interface. |Automatic assignment IP |
   |**Associating EIP** |||
   |ISP |Select the ISP of the EIP. |BGP (multi\-line) |
   |Billing rule |Input the billing method of the EIP |Pay\-by\-bandwidth  |
   |Bandwidth cap |Input the bandwidth cap of the Elastic IP (EIP). |20Mbps |
   

4. Follow the console instructions to review and confirm the legal agreements.

5. Click **Submit Order** to navigate to the application submission success page.

6. Click **Go to Console** to navigate to the instances page to view the newly created instance.


<span id=".5q2l6aqk5LqM77ya6YWN572u5ZCO56uv5pyN5Yqh5Zmo57uE"></span>
### Step 2: Configure a Server Group


1. On the instance list page, click the CLB instance name clb\-01.

2. On the **Server Group** tab, click **Create Server Group**.

3. Refer to the table below for configuration related arguments.

   
   |Name |Explaination |Valid Value |
   |---|---|---|
   |Term |Enter the name of the backend server group. |rsp\-01 |
   |Type  |Select the Type of the Server Group. |IP type |
   

4. Click **Confirm** to complete the creation of the Server Group.

5. Click the name of the created Server Group rsp\-01.

6. Click **Add IP Address**.

7. Refer to the table below for configuration related arguments.

   
   |Name |Explaination |Valid Value |
   |---|---|---|
   |IP address |Input the private IP address of the cross\-VPC Elastic Compute Service (ECS). |192.168.1.10 |
   |Port |Input the port of cross\-VPC Elastic Compute Service (ECS). |80 |
   |Weight |Enter the weight of the cross\-VPC Elastic Compute Service (ECS) instance. |100 |
   

8. Click **Confirm** to complete the configuration of the Server Group.


<span id=".5q2l6aqk5LiJ77ya5re75Yqg55uR5ZCs5Zmo"></span>
### Step 3: Add Listener


1. On the details page of CLB instance clb\-01, select the **Listener** tab.

2. Click **Add Listener**, refer to the table below to configure the protocol and listening parameters.

   
   |Name |Explaination |Valid Value |
   |---|---|---|
   |CLB protocol |Select the protocol for the CLB instance listener. |TCP |
   |Listening port |Input the listening port. |80 |
   |Scheduling algorithm |Select the rules that the listener follows to forward requests. |Weighted Round Robin (WRR) |
   |Timeout Period |Set the timeout period. |900 seconds |
   

3. After completing the configuration, click **Next**.

4. On the **Server Group** configuration page, select the created backend server group rsp\-01, then click **Next**.

5. On the **Health Check** configuration page, retain default values of all parameters and click **Next**.

6. On the **Configuration Review** page, click **OK** to complete the actions.


<span id=".5q2l6aqk5Zub77ya6YWN572u5Lit6L2s6Lev55Sx5Zmo"></span>
### Step 4: Configure a TR instance


1. **Create a TR instance tr\-01 by referring to**[ Creating a TR instance](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-01).

   After tr\-01 is created, the system automatically creates a routing table for it, such as tr\-systemrtb.

2. **Refer to the following steps to create two attachments for the instance tr\-01, attaching vpc\-01 and vpc\-02 respectively**.

   1. Click the TR instance name tr\-01.

   2. Under the **Basic Information** section, on the **Intra\-Region Attachment** tab, click **Create Intra\-Region Attachment**. Refer to the table below to configure the relevant information for 2 intra\-region attachments.

      
      |Name |Explaination |Value (Network Instance Connection 1) |Value (Network Instance Connection 2) |
      |---|---|---|---|
      |**Basic information **  ||||
      |Transit Router  |Select the Transit Router. |tr\-01 |tr\-01 |
      |Region  |Select the region where the network instance resides. |China (Beijing) |China (Beijing) Zone 2 |
      |Term |Input the name of the attachment. |netlink\-01 |netlink\-02 |
      |**Network Instance** ||||
      |Network instance type |Select a type of network instance. |Virtual Private Cloud |Virtual Private Cloud |
      |Virtual Private Cloud |Select network instance. |vpc\-01 |vpc\-02 |
      |**Attachment point configuration** ||||
      |Availability Zone and Subnet |Select the Availability Zone for the attachment point and specify a subnet. The subnet assigns a private IP address to the attachment point (that is, the network interface). |Availability Zone A, subnet\-01 |Availability Zone A, subnet\-02 |
      |**Route configuration** ||||
      |Associated forwarding |Specify whether to enable associated forwarding for the attachment. |Enable, tr\-systemrtb |Enable, tr\-systemrtb |
      |Route learning |Specify whether to enable route learning for the attachment. |Enable, tr\-systemrtb |Enable, tr\-systemrtb |
      

   3. Click **Create** to complete the actions.

3. **Configure the route information for tr\-01 as follows**:

   1. In the **Route Table** tab, click the target routing table tr\-systemrtb.

   2. On the right\-hand page, click **Create Static Route** and refer to the table below to configure routing information.

      
      |Name |explain |Valid Value |
      |---|---|---|
      |Route name |Input the name of the route. |trentry\-01 |
      |Destination CIDR block |Input the back\-to\-origin IP addresses for the CLB Layer\-4 listener in the Cloud Service region. Refer to [CLB Back-to-origin IP Address](https://docs.byteplus.com/en/docs/clb/Cross-VPC-server-overview).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the Cloud Service region has multiple back\-to\-origin addresses, you must refer to this step and configure them all.</div><br> |100.127.216.0/22<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This example is for China (Beijing). Besides configuring 100.127.216.0/22, you must also perform this step to configure 100.127.64.0/19.</div><br> |
      |Blackhole route |Whether it is a blackhole route. |No  |
      |Next Hop  |Select the next hop of the route. |vpc\-01 |
      

   3. Click **Confirm** to complete the configuration.


<span id=".5q2l6aqk5LqU77ya6YWN572uVlBD6Lev55Sx5L-h5oGv"></span>
### Step 5: Configure VPC route entries

Follow these steps to configure routing information for the target routing tables of vpc\-01 and vpc\-02 separately:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The target route table of vpc\-01 must be a system route table, because the CLB instance forwards traffic based on the system route table of the VPC.</div>


* <div data-tips="true" data-tips-type="tip">The target routing table for vpc\-02 refers to the route table associated with the subnet where the backend server ecs\-02 resides.</div>


1. Log in to[ the Route Table console](https://console.byteplus.com/vpc/routeTable). 

2. In the top menu bar, select the region for the target VPC: China (Beijing).

3. In the route table list, click the name of the target route table.

4. On the **Route Entry** tab, select **Custom Route**.

5. Click **Add Route Entry**, and configure the custom route entry following the prompts.

   
   |Name |Explaination |Value (vpc\-01) |Value (vpc\-02) |
   |---|---|---|---|
   |Destination CIDR block |Input the target CIDR block. |192.168.1.10/32<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This CIDR block is the private IP address of the backend server ecs\-02. You can also configure it as the subnet range to which ecs\-02 belongs, according to your actual requirements.</div><br> |100.127.216.0/22<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Input the back\-to\-origin IP addresses for the CLB Layer\-4 listener in the Cloud Service region. Refer to <a href="https://docs.byteplus.com/en/docs/clb/Cross-VPC-server-overview">CLB Back\-to\-origin IP Address</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the Cloud Service region has multiple back\-to\-origin addresses, you must refer to this step and configure them all. For example, if the region is China (Beijing), besides configuring 100.127.216.0/22, you also need to refer to this action to configure 100.127.64.0/19.</div><br> |
   |Next Hop type |Select next hop type. |Transit Router  |Transit Router  |
   |Next Hop  |Select the next hop. |tr\-01 |tr\-01 |
   

6. Click **Confirm** to complete the VPC route configuration.


<span id=".5q2l6aqk5YWt77ya6YWN572u5ZCO56uv5pyN5Yqh5Zmo5a6J5YWo57uE"></span>
### Step 6: Configure backend server security group

Authorize CLB traffic in the security group where the Elastic Compute Service (ECS) ecs\-02 is located.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This document uses the example of attaching an IPv4 server group (IP type) to a TCP listener. For configuring security group rules in other scenarios, please refer to <a href="https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group">Configuring a backend server security group</a>.</div>



1. Log in to[ the ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance). 

2. In the top menu bar, select the Target Region.

3. In the left\-side navigation pane, click **Instance**.

4. Click the name of target ECS instance ecs\-02.

5. In the **Security Group** tab, click **Configure Rule** to the right of the security group.

6. On the **Inbound Rule** tab, click **Add Rule**.

7. Refer to the table below for configuration related arguments.

   
   |No<br><br> |Policy  |Protocol Type |Port range |Source IP |Description |
   |---|---|---|---|---|---|
   |1 |Allow  |TCP |The port on which ECS provides services (this example uses 80) |100.64.0.0/10 |Receive health check requests and IPv4 client requests forwarded by CLB |
   

8. Click **Confirm** to complete the actions.


<span id=".5q2l6aqk5LiD77ya6aqM6K-B"></span>
## Verification Key


1. Log in to the ECS instance ecs\-01 by referring to [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Logging in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Run the `ping` command to connect to the private IP address of the backend server ecs\-02 and test the network connectivity.

3. Open the browser on the local computer, input `http://12.XX.XX.89`, if the backend service interface configured by the backend server ecs\-02 is displayed, it indicates that the access request has been forwarded by the CLB instance to the backend Elastic Compute Service (ECS) ecs\-02, and ecs\-02 can process the request properly and return the requested page.
