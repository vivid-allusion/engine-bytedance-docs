---
title: "Configuring the active and standby availability zones in the same region for CLB disaster recovery"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Best-practices-12"
---

This section describes how to implement disaster recovery of Classic Load Balancer (CLB) between the active and standby availability zones (AZs).

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenarios

CLB supports disaster recovery between the active and standby AZs. Deploying CLB in different AZs within the same region can help you implement disaster recovery for services. When the active AZ fails because the network is abnormal or the CLB service is unavailable, inbound traffic can be distributed through CLB deployed in the standby AZ.

This section takes the China (Shanghai) region as an example to describe how to deploy CLB in the active and standby AZs to achieve disaster recovery. The specific scenario is shown in the figure below.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d3a7031b26e7c16e53bc7765ec11b8b7.png) </span>

&nbsp;

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The required Virtual Private Cloud VPC\-1 and subnets Subnet\-1 and Subnet\-2 have been created. For more information, refer to [Setting up an IPv4 VPC](https://docs.byteplus.com/en/docs/vpc/Building-an-IPv4-VPC).

* The required Elastic Compute Service (ECS) instances ECS\-1, ECS\-2, ECS\-3, and ECS\-4, have been created. For more information, refer to [Purchasing ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* The required ECS instances have completed backend service deployment. For more information, refer to [Setting up a backend service](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTP-static-page#.5q2l6aqk5LqM77ya5pCt5bu65ZCO56uv5pyN5Yqh).

* The security groups for the required Elastic Compute Service (ECS) server instances have allowed access from the CIDR block `100.64.0.0/10 `over TCP, along with the required service ports (For example, TCP port 80). For details, refer to [Configuring the backend server security group](https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group).


<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following describes only the required parameters and their values. For other parameters, retain the default values. For more information about other parameters, refer to <a href="https://docs.byteplus.com/en/docs/clb/CLB-instances-01">CLB User Guide</a>.</div>


<span id=".5q2l6aqk5LiA77ya5Yib5bu66LSf6L295Z2H6KGh5a6e5L6L"></span>
### Step 1: Create a CLB instance


1. Log in to [the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. Click **Create Classic Load Balancer**.

3. Configure the basic information of the CLB instance as prompted.

   
   |Name |Valid Value |
   |---|---|
   |**Basic information** ||
   |Billing methods |Pay\-as\-you\-go |
   |Region |China (Shanghai) |
   |AZ |* Active availability zone: Availability Zone A<br><br>* Standby availability zone: Availability Zone B |
   |Term |clb\-1 |
   |**Network Configuration** ||
   |IP Address Version |IPv4 |
   |Network Type |Internet |
   |Virtual Private Cloud |vpc\-1 |
   |Subnet |subnet\-1 |
   |IPv4 address |Automatic assignment IP |
   |**Associating EIP** ||
   |ISP |BGP(multi\-line) |
   |Billing rule |Pay\-by\-bandwidth |
   |Bandwidth cap |20Mbps |
   |**Instance specification** ||
   |Type |small_1 |
   

4. follow the console instructions to review and confirm the legal agreements.

5. Click **Submit Order**. You will be redirected to the Application Submitted Successfully page.

6. Click **Go to console** to view the newly created Classic Load Balancer instance on the Instances page.


<span id=".5q2l6aqk5LqM77ya6YWN572u5ZCO56uv5pyN5Yqh5Zmo57uE"></span>
### Step 2: Configure a Server Group


1. On the instance list page, click the name of the CLB instance clb\-1.

2. On the **Server Group** tab, click **Create a Server Group**.

3. Input the name group\-1, and click **Confirm**.

4. Click the name of the created backend server group group\-1.

5. Click the **Add Server** button and select the created Elastic Compute Service (ECS) instances ECS\-1, ECS\-2, ECS\-3, and ECS\-4.

6. Click **Next** to configure the port and weight for the ECS instances ECS\-1, ECS\-2, ECS\-3, and ECS\-4.

   In this example, the port is set to 80 and the weight is set to 100 for all backend servers.

7. Click **Confirm** to complete the configuration.


<span id=".5q2l6aqk5LiJ77ya5re75Yqg55uR5ZCs5Zmo"></span>
### Step 3: Add Listener


1. On the details page of the CLB instance clb\-1, select the **Listener** tab.

2. Click **Add Listener**, refer to the table below to configure the protocol and listening parameters.

   
   |Name |Valid Value |
   |---|---|
   |Listener name |listener\-1 |
   |CLB protocol |HTTP |
   |Listening port |80 |
   |Scheduling algorithm |Weighted Round Robin (WRR) |
   |IAM |Disable |
   

3. The timeout period remains unchanged.

4. After the configuration is complete, click **Next**.

5. On the **Default Server Group** configuration page, select the created backend server group group\-1, then click **Next**.

6. On the **Health Check** configuration page, retain default values of all parameters, then click **Next**.

7. On the **Configuration Review** page, click **Confirm** to complete the operation.


<span id=".57uT5p6c6aqM6K-B"></span>
## Result verification


* When the active AZ is normal, the CLB instance deployed in the active AZ will forward access requests to all backend servers in the backend server group associated with the listener according to the scheduler configured for the listener.

* When the active AZ is abnormal, the CLB instance deployed in the standby AZ will forward access requests to all backend servers that are located in the standby AZ and belong to the backend server group associated with the listener according to the scheduler configured for the listener.

* When the CLB instance in the active AZ is faulty, the CLB instance deployed in the standby AZ will forward access requests to all backend servers in the backend server group associated with the listener according to the scheduler configured for the listener.
