---
title: "ECS instances across VPCs as backend servers (Cloud Enterprise Network)"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Combining-with-the-CEN-service-to-use-an-ECS-instance-in-a-VPC-as-the-cross-VPC-server"
---

This section describes how to integrate the Classic Load Balancer (CLB) service with the Cloud Enterprise Network (CEN) to implement ECS instances across VPCs as backend servers.

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenarios

CLB can integrate with CEN to forward access requests to the Elastic Compute Service (ECS) instances across VPCs for further processing.

This section uses the scenario of the same region as an example, as shown in the following figure:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For cross\-region scenarios, in addition to completing the configurations in this document, you must also configure the inter region bandwidth information for the CEN instance by referring to <a href="https://docs.byteplus.com/en/docs/cen/CEN-bandwidth-packages-01">Creating a CEN bandwidth package</a> and <a href="https://docs.byteplus.com/en/docs/cen/Inter-region-bandwidth-01">Allocating the inter region bandwidth</a>.</div>


> The information marked in the figure is for reference only. Please modify the relevant information according to the actual network planning.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ee8c71d36c0d22cc830ebffa30433827.png) </span>

&nbsp;

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


<span id=".5q2l6aqk5LiA77ya5Yib5bu6Q0xC5a6e5L6L"></span>
### Step 1: Create a CLB instance


1. Log in to [the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. Click **Create Classic Load Balancer**.

3. Refer to the table below for configuration related arguments.

   
   |Name |Explaination |Valid Value |
   |---|---|---|
   |**Basic information** |||
   |Billing methods |Input the billing method of the CLB instance. |Pay\-as\-you\-go |
   |Region |Select the Region where the CLB resides. |China (Beijing) |
   |Term |Type the name of the CLB instance. |clb\-01 |
   |**Network Configuration** |||
   |IP Address Version |Select the IP version of the CLB instance. |IPv4 |
   |Network Type |Select the network type of the CLB instance. |Internet |
   |Virtual Private Cloud |Select the VPC where the CLB resides. |vpc\-01 |
   |Subnet |Select the subnet where the CLB resides. |subnet\-01 |
   |IPv4 address |Select the allocation method for the private IPv4 address of the CLB network interface. |Automatic assignment IP |
   |**Associating EIP** |||
   |ISP |Select the ISP of the EIP. |BGP (multi\-line) |
   |Billing rule |Select the billing method for the EIP. |Pay\-by\-bandwidth |
   |Bandwidth cap |Input the bandwidth cap for the Elastic IP (EIP). |20Mbps |
   

4. Please refer to the console guidance to review and Confirm the related Legal.

5. Click **Submit Order** to redirect to application submission success page.

6. Click **Go to Console** to navigate to the instances page and view the newly created instance.


<span id=".5q2l6aqk5LqM77ya6YWN572u5ZCO56uv5pyN5Yqh5Zmo57uE"></span>
### Step 2: Configure a Server Group


1. On the instance list page, click the CLB instance name clb\-01.

2. On the **Server Group** tab, click **Create Server Group**.

3. Refer to the table below for configuration related arguments.

   
   |Name |Explaination |Valid Value |
   |---|---|---|
   |Term |Enter the name of the backend server group. |rsp\-01 |
   |Type |Select the Type of the Server Group. |IP type |
   

4. Click **OK** to complete the creation of the backend server group.

5. Click the name of the created backend server group rsp\-01.

6. Click **Add IP Address**.

7. Refer to the table below for configuration related arguments.

   
   |Name |Explaination |Valid Value |
   |---|---|---|
   |IP address |Input the private IP address of the cross\-VPC Elastic Compute Service (ECS). |192.168.1.10 |
   |Port |Input the port of the cross\-VPC Elastic Compute Service (ECS). |80 |
   |Weight |Input the weight of the cross\-VPC Elastic Compute Service (ECS). |100 |
   

8. Click **Confirm** to complete the actions.


<span id=".5q2l6aqk5LiJ77ya5re75Yqg55uR5ZCs5Zmo"></span>
### Step 3: Add Listener


1. On the details page of CLB instance clb\-01, select the **Listener** tab.

2. Click **Add Listener**, refer to the table below to configure protocol & listener arguments.

   
   |Name |Explaination |Valid Value |
   |---|---|---|
   |CLB protocol |Select the protocol for the CLB instance listener. |TCP |
   |Listening port |Input the listening port. |80 |
   |Scheduling algorithm |Select the rules that the listener follows to forward requests. |Weighted Round Robin (WRR) |
   |Timeout Period |Set the timeout period. |900 seconds |
   

3. After completing the configuration, click **Next**.

4. On the **Server Group** configuration page, select the created server group rsp\-01, then click **Next**.

5. On the **Health Check** configuration page, retain default values of all parameters, then click **Next**.

6. On the **Configuration Review** page, click **Confirm** to complete the operation.


<span id=".5q2l6aqk5Zub77ya6YWN572u5LqR5LyB5Lia572R"></span>
### Step 4: Configure the Cloud Enterprise Network (CEN)


1. **Create a CEN instance**.

   1. Log in to[ the CEN console](https://console.byteplus.com/cen/EnterpriseNetwork). 

   2. Click **Create Cloud Enterprise Network**.

   3. Refer to the table below for configuration related arguments.

      
      |Name |Explaination |Valid Value |
      |---|---|---|
      |Term |Type the name of the Cloud Enterprise Network (CEN) instance. |cen\-01 |
      |Load Network Instances |Load a VPC instance. |On |
      |Region |Select the region to which the network instance belongs. |China (Beijing) Zone 2 |
      |Instance Type |Select the type of network instance to be attached. |Virtual Private Cloud |
      |Network Instance |Select the network instance to be attached. |vpc\-01 |
      

   4. Click **Confirm** to complete the creation.

2. **Load a Virtual Private Cloud instance**.

   1. Click the name of the CEN instance to go to the details page.

   2. On the **Network Instance** tab, click **Load Network Instance**.

   3. Refer to the table below for configuration related arguments.

      
      |Name |Explaination |Valid Value |
      |---|---|---|
      |Account |Select the account to which the network instance belongs. |this account |
      |Region |Select the Region where the network instance resides. |China (Beijing) |
      |Instance Type |Select the type of network instance to be attached. |Virtual Private Cloud |
      |Network Instance |Select the network instance to be attached. |vpc\-02 |
      

   4. Click **OK** to complete the loading.

3. **Configure the CLB back\-to\-source routing**.

   1. On the network instance list page, select **Cloud Service** tab.

   2. Click **Configure Cloud Service**.

   3. Refer to the table below for configuration related arguments.

      
      |Name |Explaination |Valid Value |
      |---|---|---|
      |**Cloud as a service info** |||
      |Cloud as a service region |Select the Region of the cloud service. |China (Beijing) |
      |Cloud as a service VPC |Select the VPC where the Cloud Service resides. |vpc\-01 |
      |Cloud as a service address |Input the back\-to\-origin IP addresses for the CLB Layer\-4 listener in the Cloud Service region. Details refer to [CLB Back-to-origin IP Address](https://docs.byteplus.com/en/docs/clb/Cross-VPC-server-overview).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the Cloud Service region has multiple back\-to\-origin addresses, you must refer to this step and configure them all.</div><br> |100.127.216.0/22<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This example is for China (Beijing). Besides configuring 100.127.216.0/22, you must also perform this step to configure 100.127.64.0/19.</div><br> |
      |**Release information** |||
      |Release scope |Select the advertisement scope of the route. |Custom release scope |
      |Posting instances |Select the target network instance that receives source\-routed traffic. |vpc\-02 |
      

   4. Click **Confirm** to complete the configuration.


<span id=".5q2l6aqk5LqU77ya6YWN572u5ZCO56uv5pyN5Yqh5Zmo5a6J5YWo57uE"></span>
### Step 5: Configure the backend server security group

Allow CLB traffic in the security group where the ECS ecs\-02 is located.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This document uses the example of attaching an IPv4 server group (IP type) to a TCP listener. For configuring security group rules in other scenarios, please refer to <a href="https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group">Configuring a backend server security group</a>.</div>



1. Log in to[ the ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance). 

2. In the top menu bar, select the Target Region.

3. In the left\-side navigation pane, click **Instance**.

4. Click the name of target ECS instance ecs\-02.

5. In the **Security Group** tab, click **Configure Rule** to the right of the security group.

6. On the **Inbound Rule** tab, click **Add Rule**.

7. Refer to the table below for configuration related arguments.

   
   |No |Policy |Protocol Type |Port range |Source IP |Description |
   |---|---|---|---|---|---|
   |1 |Allow |TCP |The port on which ECS provides services (this example uses 80) |100.64.0.0/10 |Receive health check requests and IPv4 client requests forwarded by CLB |
   

8. Click **Confirm** to complete the action.


<span id=".5q2l6aqk5YWt77ya6aqM6K-B"></span>
### Step 6: Verify the connectivity


1. Log in to the ECS instance ecs\-01 by referring to [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Logging in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Execute the `ping` command to connect to the private IP address of the backend server ecs\-02 and test network connectivity.

3. Open the browser on the local computer, input `http://12.XX.XX.89`, if the backend service interface configured by the backend server ecs\-02 is displayed, it indicates that the access request has been forwarded by the CLB instance to the backend Elastic Compute Service (ECS) ecs\-02, and ecs\-02 can process the request properly and return the requested page.
