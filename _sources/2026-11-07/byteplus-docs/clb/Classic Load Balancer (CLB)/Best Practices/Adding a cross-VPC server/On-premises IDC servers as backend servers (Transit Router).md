---
title: "On-premises IDC servers as backend servers (Transit Router)"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Combining-with-the-TR-service-to-use-a-server-in-a-data-center-as-the-cross-VPC-server"
---

This topic introduces how Classic Load Balancer (CLB) integrates with Transit Router (TR) to enable server instances within a data center as the backend servers of the CLB.

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenarios

CLB forwards access requests to servers within the IDC for processing. The figure demonstrates:

> The diagram displays sample configurations for each service. Modify these values according to your actual network architecture during implementation.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_35a155c7025e0d965b1577c3cb372a48.png) </span>

&nbsp;

All resources in the diagram above are located in the China (Beijing) region. Other data annotations in the diagram are explained below:


* Virtual Private Cloud vpc\-01: the subnet segment is `172.16.1.0/24`; the private IP address of Elastic Compute Service ecs\-01 is `172.16.1.10`; an EIP of ecs\-01 is `10.XX.XX.10`.

* Classic Load Balancer clb\-01: The private IP address is 172.16.1.20, and the EIP address is 10.XX.XX.20.

* Direct Connect Gateway dcgw\-01: gateway IP is `10.0.0.1`; BGP ASN is 4600; BGP key is 123456.

* Local IDC: The subnet is `192.168.1.0/24`, the private IP address of server server\-01 is `192.168.1.10`, and the gateway IP is `10.0.0.2`.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The creation of vpc\-01 and its subnet is complete. For more information, see Setting up an IPv4 VPC.

* The creation of ecs\-01 is complete. For more information, see Purchasing an ECS instance.

* Confirm that routing from the data center to the cloud network is configured, and ensure no IP addresses within the 100.64.0.0/10 CIDR block exist in the data center.

* The private IP addresses of IDC servers have been obtained, and backend services are deployed on the on\-premises IDC servers.


<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedures

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following section only covers essential parameters and their recommended values when configuring each service resource. For all parameters not explicitly discussed, retain the default settings unless otherwise required by your specific use case.</div>


<span id=".5q2l6aqk5LiA77ya5Yib5bu66LSf6L295Z2H6KGh5a6e5L6L"></span>
### Step 1: Create CLB instance


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. Click Create CLB.

3. Configure relevant parameters based on the table below.

   
   |Parameter |Explanation |Value |
   |---|---|---|
   |**Basic information** |||
   |Billing method |Select a billing method for the CLB instance. |Pay\-as\-you\-go |
   |Regions |Select the Region where the CLB instance resides. |China (Beijing) |
   |Name |Enter the name of CLB instance. |clb\-01 |
   |**Network Configuration** |||
   |IP version |Select the IP version of CLB. |IPv4 |
   |Network type |Select the network type of the CLB instance. |Internet |
   |VPC |Select the VPC to which the CLB instance belongs. |vpc\-01 |
   |Subnet |Select the subnet to which the CLB instance belongs. |subnet\-01 |
   |IPv4 address |Select the allocation method of the private IPv4 address for the CLB network interface. |Automatic IP assignment |
   |**Associate an EIP** |||
   |ISP |Select the ISP for the EIP. |BGP (multi\-line) |
   |Metering method |Input the billing method of the EIP |Pay\-by\-bandwidth\-cap |
   |Bandwidth cap |Type a bandwidth cap for the Elastic IP (EIP). |20Mbps |
   

4. Follow the console guidance to review and accept Legal.

5. Click Submit Order to navigate to the application submission success page.


<span id=".5q2l6aqk5LqM77ya5Yib5bu65ZCO56uv5pyN5Yqh5Zmo57uE"></span>
### Step 2: Create server group


1. On the Instances page, click the name clb\-01 of the CLB instance.

2. On the **Server Group** tab, click **Add Server Group**.

3. Configure relevant parameters based on the table below.

   
   |Parameter |Explanation |Value |
   |---|---|---|
   |Name |Enter the name of the backend server group. |rsp\-01 |
   |Topic |Select the type of the backend server group. |IP type |
   

4. Click Confirm to complete the creation of the Server Group.

5. Click the name of the created Server Group rsp\-01.

6. Click **Add IP Address**.

7. Configure relevant parameters based on the table below.

   
   |Parameter |Explanation |Value |
   |---|---|---|
   |IP Address |Type the private IP address of the server within the data center. |192.168.1.10 |
   |Port |Type the port of the server in the data center. |80 |
   |Weight |Type the server's weight within a data center. |100 |
   

8. Click Confirm to complete the configuration of the Server Group.


<span id=".5q2l6aqk5LiJ77ya5re75Yqg55uR5ZCs5Zmo"></span>
### Step 3: Add listener


1. On the details page of CLB instance clb\-01, select the Listener tab.

2. Click Add Listener and configure the protocol and listener parameters according to the table below.

   
   |Parameter |Explanation |Value |
   |---|---|---|
   |Listener name |Enter the listener name. |listener\-01 |
   |CLB protocol |Select the protocol for the CLB instance listener. |TCP |
   |Listening port |Enter the listening port. |80 |
   |Scheduling algorithm |Select the rule the listener follows to forward requests. |Weighted Round Robin (WRR) |
   |Timeout period |Set the timeout period. |900 seconds |
   

3. After completing the configuration, click Next.

4. On the Server Group configuration page, select the created backend server group rsp\-01, then click Next.

5. On the Health Check configuration page, retain default values of all parameters and click Next.

6. On the Configuration Review page, click OK to complete the actions.


<span id=".5q2l6aqk5Zub77ya6YWN572u5LiT57q_6L-e5o6l5pyN5Yqh"></span>
### Step four: configure Direct Connect service


1. Refer to [Create DC Connection](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1) to open a Direct Connect Connection. The DC Connection used in this example is DAS237_port101_conn in China (Beijing).

2. Create Direct Connect gateway.

   1. In the left\-side navigation pane, select Direct Connect Gateway.

   2. Click **Create DC Gateway**.

   3. Configure relevant parameters based on the table below.

      
      |Parameter |Explanation |Value |
      |---|---|---|
      |Regions |Select the region of the Direct Connect. |China (Beijing) |
      |Name |Input the name of the Direct Connect |dcgw\-01 |
      |Agreement |Follow the console guidance to review and accept Legal. |\- |
      

   4. Click Buy now to complete the creation of the Direct Connect Gateway.

3. Create Virtual Interface.

   1. Click the name of the target Direct Connect Gateway.

   2. On the Virtual Interface tab, click Add Virtual Interface.

   3. Configure relevant parameters based on the table below.

      
      |Parameter |Explanation |Value |
      |---|---|---|
      |**Basic information** |||
      |Regions |Select the region of the virtual interface. |China (Beijing) |
      |Name |Enter a name of the DC Virtual Interface. |vif\-01 |
      |DC Connection |Select the DC Connection to be associated with the virtual interface. |DAS237_port101_conn |
      |Direct Connect Gateway |Select the DC Gateway to be associated with the DC Virtual Interface. |dcgw\-01 |
      |**Interconnection information** |||
      |IPv4 interconnect IP |Type the IPv4 interconnect IP. |* ​Local Gateway Interconnection IP: 10.0.0.1/30​​<br><br>* Your gateway peer IP: 10.0.0.2/30​​ |
      |VLAN ID |Set the VLAN ID for connecting to the data center. Range: 0–2999. |10 |
      |**Routing information** |||
      |Route Type |Select the route type. |BGP |
      |BGP ASN |Type the ASN of the BGP Peer. |4600 |
      |BGP key |Type the authentication key for the BGP Peer. |123456 |
      

   4. Click Create to complete the virtual interface creation.


<span id=".5q2l6aqk5LqU77ya6YWN572u5Lit6L2s6Lev55Sx5Zmo5pyN5Yqh"></span>
### Step 5: Configure Transit Router service


1. Refer to [Creating a Transit Router instance](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-01) to complete the creation of transit router instance tr\-01.

   After TR instance tr\-01 is created, the system automatically creates a route table for it, such as rtb\-01.

2. Create a network instance attachment.

   Follow the steps below to create 2 network instance attachments, associating them with vpc\-01 and dcgw\-01 respectively.

   1. Click the transit router instance name tr\-01.

   2. On the Intra\-Region Attachment tab, click Create intra\-region attachments.

   3. Configure relevant parameters based on the table below.

      * VPC attachment

         
         |Parameter |Explanation |Value |
         |---|---|---|
         |**Basic information** |||
         |Transit Router |Select the Transit Router. |tr\-01 |
         |Regions |Select the region where the network instance resides. |China (Beijing) |
         |Name |Type the name for the attachment. |attach\-01 |
         |**Network Instances** | | |
         |Network instance type |Select a type of network instance. |VPC |
         |VPC |Select a network instance. |vpc\-01 |
         |**Attachment point configuration** |||
         |AZs and Subnets |Select the Availability Zone for the attachment point and specify a subnet. The subnet assigns a private IP address to the attachment point (that is, the network interface). |Availability Zone A, subnet\-01 |
         |**Route configuration** |||
         |Association forwarding |Specify whether to enable association forwarding for this attachment. |Turn on, rtb\-01 |
         |Route Propagation |Specify whether to enable route learning for this attachment. |Turn on, rtb\-01 |
         

      * DC Gateway attachment

         
         |Parameter |Explanation |Value |
         |---|---|---|
         |**Basic information** |||
         |Transit Router |Select the Transit Router. |tr\-01 |
         |Regions |Select the region where the network instance resides. |China (Beijing) |
         |Name |Type the name for the attachment. |attach\-02 |
         |**Network Instances** |||
         |Network instance type |Select a type of network instance. |Direct Connect Gateway |
         |Direct Connect Gateway |Select a network instance. |dcgw\-01 |
         |**Route configuration** |||
         |Association forwarding |Specify whether to enable association forwarding for this attachment. |Enabled, rtb\-01 |
         |Route Propagation |Specify whether to enable route learning for this attachment. |Turn on, rtb\-01 |
         

   4. Click **Create** to complete the action.

3. Configure routing information.

   1. In the Route Table tab, and click the target routing table rtb\-01.

   2. Click Create Static Route on the right pane.

   3. Configure relevant parameters based on the table below.

      
      |Parameter |Explanation |Value |
      |---|---|---|
      |Route name |Input the route name. |rte\-01 |
      |Destination CIDR |Input the back\-to\-origin IP addresses for the CLB Layer\-4 listener in the Cloud Service region. For details, see CLB Back\-to\-origin IP Address.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the Cloud Service region has multiple back\-to\-origin addresses, you must refer to this step and configure them all.</div><br> |100.127.216.0/22<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This example is for China (Beijing). Besides configuring 100.127.216.0/22, you also need to configure 100.127.64.0/19 based on this procedure.</div><br> |
      |Black hole routing |Is it a blackhole route |No |
      |Next Hop |Select the next hop of the route. |vpc\-01 |
      


<span id=".5q2l6aqk5YWt77ya6YWN572uVlBD6Lev55Sx"></span>
### Step 6: Configure VPC routes

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The target route table of vpc\-01 must be a system route table because the load balancer forwards traffic according to the VPC’s system route table.</div>



1. Log in to the [Route table console](https://console.byteplus.com/vpc/routeTable).

2. In the top menu bar, select the region for the target VPC: China (Beijing).

3. Click the target route table name.

4. On the Route Entry tab, select Custom Route.

5. Click Add Route Entry, and configure the custom route entry following the prompts.

   
   |Parameter |Explanation |Value |
   |---|---|---|
   |Destination CIDR |Input the target CIDR block. |192.168.1.10/32<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This CIDR block is the IP address of the server in the local data center.</div><br> |
   |Next Hop type |Select the Next Hop type. |Transit Router |
   |Next Hop |Select the next hop. |tr\-01 |
   

6. Click Confirm to complete the VPC route configuration.


<span id=".5q2l6aqk5LiD77ya6aqM6K-B6LSf6L295Z2H6KGh5pyN5Yqh"></span>
### Step 7: Verify CLB service


1. Log in to the Elastic Compute Service (ECS) instance ecs\-01; see [Logging into the Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Logging in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance) for details.

2. Run the `ping` command to connect to the private IP address of backend server server\-01 and test network connectivity.

3. Open the browser on the local computer, input http://12.XX.XX.89, and the interface of backend service configured on Elastic Compute Service (ECS) server\-01 is displayed. This indicates that the current access request has been forwarded by the CLB instance to the backend ECS server\-01, and server\-01 is able to process the request normally and return the requested page.
