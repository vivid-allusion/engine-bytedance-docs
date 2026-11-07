---
title: "ECS instances across VPCs serve as backend servers (Transit Router)"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Cross-VPC-ECS-instances-as-backend-servers-TR"
---

This topic explains how to integrate Network Load Balancer (NLB) with Transit Routers (TR) to enable Elastic Compute Service (ECS) instances across VPCs as NLB backend servers.

<span id="MSJvdnJT"></span>
## Scenarios

The NLB distributes access requests to these cross\-VPC cloud servers for processing. The figure demonstrates:

> The diagram displays sample configurations for each service. Modify these values according to your actual network architecture during implementation.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_680e3e0a624590449a772f32b582ad48.png) </span>

All resources in the diagram above are located in the China (Beijing) region. Other data annotations in the diagram are explained below:


* Virtual Private Cloud VPC\-A: CIDR block `172.16.0.0/16`.

   * The CIDR block of Subnet\-A1 is `172.16.1.0/24`.

   * The CIDR block of Subnet\-A2 is `172.16.2.0/24`.

   * The private IP address of ECS\-A is `172.16.1.10`.

* Virtual Private Cloud VPC\-B: CIDR block `192.168.0.0/16`.

   * The CIDR block of Subnet\-B is `192.168.1.0/24`.

   * The private IP address of ECS\-B is `192.168.1.10`.

* Virtual Private Cloud VPC\-C: CIDR block `10.0.0.0/16`.

   * The CIDR block of Subnet\-C is `10.0.1.0/24`.

   * The private IP address of ECS\-C is `10.0.1.10`.


<span id="lGtLdGyk"></span>
## Preparations


1. Using your BytePlus account, create three VPCs in the China (Beijing) region, with configurations matching the parameters described in the [background section above](https://docs.byteplus.com/en/docs/natgateway/Configuring-multiple-Internet-NAT-Gateways-in-a-VPC#.6IOM5pmv5LuL57uN). For specific actions, see [Creating a Virtual Private Cloud](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

2. Create Elastic Compute Service (ECS) instances in each VPC subnet as follows, all without EIP addresses:​​​​ VPC\-A:​​ In Subnet\-A1, create ​​ECS\-A​​ with private IP 172.16.1.10​​; VPC\-B:​​ In Subnet\-B, create ​​ECS\-B​​ with private IP 192.168.1.10​​; VPC\-C:​​ In Subnet\-C, create ​​ECS\-C​​ with private IP 10.0.1.10. For more information, see [Buying ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

3. Deploy backend services on ECS\-B and ECS\-C. For operations, see [Configuring backend services](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTP-static-page#.5q2l6aqk5LqM77ya5pCt5bu65ZCO56uv5pyN5Yqh).


<span id="4NQw5gXI"></span>
## Configuration procedures

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following section only covers essential parameters and their recommended values when configuring each service resource. For all parameters not explicitly discussed, retain the default settings unless otherwise required by your specific use case.</div>


<span id="HHmgOWqs"></span>
### Step 1: Configure the Transit Router (TR)

Create a Transit Router instance and configure relevant routing to achieve bi\-directional communication between VPC\-A and VPC\-B/VPC\-C, while maintaining isolation between VPC\-B and VPC\-C.​​

This guide uses multiple VPCs under the same account and region as an example. For cross\-account or cross\-region configurations, refer to the following documentation as needed:


* [Implement private connectivity and segmentation between VPCs (same account, cross-region)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-03)

* [Implement private connectivity and segmentation between VPCs (cross-account, same region)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-04)

* [Implement connectivity and segmentation between VPCs (cross-account, cross-region)](https://docs.byteplus.com/en/docs/transitrouter/Connecting-and-isolating-different-VPCs-across-accounts-and-Regions)


<span id="X2hYaFa6"></span>
#### (1) Create TR instance and its route table


   1. Log in to the [Transit Router console](https://console.byteplus.com/tr/transitRouter).

   2. Click **Create TR**.

   3. Configure relevant parameters based on the table below.

      
      |Parameter |Explanation |Example |
      |---|---|---|
      |Regions |Select the region for the Transit Router (TR) instance.​​ |China (Beijing) |
      |Name |Enter the name of the Transit Router instance. |TR\-X |
      |ASN |Specify a BGP ASN for the TR instance. Valid range: 64512\-65534 or 4200000000\-4294967294.<br><br>The ASN assigned here will be automatically prepended to the AS_Path attribute of routes propagated to other network instances.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For cross\-region networking scenarios, it is strongly recommended to use ​​different ASNs for Transit Routers in different regions​​; otherwise, cross\-region route propagation may break.</div><br> |64512 |
      |Project |Select the project for the Transit Router. |default |
      |Tags |Add one or more custom tags to the transit router as needed. |No custom tags added |
      

   4. Click **Create** to complete the creation of the TR instance.

      Upon successful creation, the system automatically generates a default TR route table. Record its name. Take **RouteTable\-default** as an example.

   6. On the Transit Router instances page, click the name of your target TR instance.

   7. On the **Route Table** tab, click **Create Route Table** next to the TR route table list.

   8. Type the custom route table name: R\-Table\-X.

   9. Click **Create** to complete the custom TR route table creation.


<span id="iVehr1aM"></span>
#### ​(2) Create Network Instance Connection


Follow the steps below to create ​​3 network instance connections​​ sequentially. Configure these connections using the parameters shown in ​​Configuration Example 1​​, ​​Configuration Example 2​​, and ​​Configuration Example 3​​ from the parameter table, respectively.

   1. On the Transit Router instances page, click the name of your target TR instance.

   2. On the **Intra\-region attachments** tab, click **Create attachment**.

   3. Configure relevant parameters based on the table below.

      
      |Parameter |Explanation |Example value 1 |Example value 2 |Example value 3 |
      |---|---|---|---|---|
      |Transit Router |Default: The Transit Router instance you selected.​​ |TR\-X |TR\-X |TR\-X |
      |Regions |Default: Same as the region where the TR instance resides. |China (Beijing) |China (Beijing) |China (Beijing) |
      |Name |The name of the network instance attachment to be created. |Attach\-VPC\-A |Attach\-VPC\-B |Attach\-VPC\-C |
      |Network instance type |Select the type for the network instance attachment to be created. |VPC |VPC |VPC |
      |VPC |Select the VPC instance to be attached. |VPC\-A |VPC\-B |VPC\-C |
      |AZs and Subnets |Select the subnet in the Availability Zone where the attachment point resides. The subnet assigns a private IP address to the network interface of the attachment.​​ |Availability Zone A, Subnet\-A |Availability Zone A, Subnet\-B |Availability Zone A, Subnet\-C |
      |Association forwarding |Enable association forwarding and select the destination Transit Router (TR) route table. When enabled, traffic originating from this network attachment will be forwarded based on the routing entries in its associated Transit Router (TR) route table.​​ |Enable; R\-Table\-X |Enable; RouteTable\-default |Enable; RouteTable\-default |
      |Route Propagation |Enable route propagation and select the destination Transit Router (TR) route table. When enabled, the specified Transit Router (TR) route table automatically creates routing entries with destination CIDRs set to the subnets of the attached VPC, using the network attachment itself as the next hop.​​ |Enable; RouteTable\-default |Enable; R\-Table\-X |Enable; R\-Table\-X |
      |Auto Publish Route |Specify whether to enable route publishing for this attachment. When activated **, ** the system automatically propagates routes from the associated Transit Router (TR) route table to all selected VPC route tables as system routes.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If association forwarding is not enabled, enabling route publishing will not add any routes to the VPC route table. Route publishing is only triggered when you enable association forwarding.</div><br> |Check |Check |Check |
      

   4. Click **Buy now** to complete the action.

   5. To verify whether the TR is configured correctly at this stage, perform the following operations:

      1. Check the TR configuration and VPC route tables.

         * The routing entries and association status for the two TR route tables are as follows:

            
            |TR route table name |Destination CIDR |Next Hop |Association forwarding |Explanation |
            |---|---|---|---|---|
            |RouteTable\-default |172.16.0.0/24,<br><br>172.16.1.0/24 |Attach\-VPC\-A |Attach\-VPC\-B, Attach\-VPC\-C |Traffic destined for 172.16.0.0/24 and 172.16.1.0/24, learned by the Transit Router through its attachments to ​​Attach\-VPC\-B​​ and ​​Attach\-VPC\-C​​, will be forwarded to ​​Attach\-VPC\-A​​. |
            |R\-Table\-X |10.0.1.0/24 |Attach\-VPC\-C |Attach\-VPC\-A |Traffic destined for 10.0.1.0/24 received through attachment Attach\-VPC\-A will be forwarded to Attach\-VPC\-C via the Transit Router. |
            ||192.168.1.0/24 |Attach\-VPC\-B ||The Transit Router will forward traffic destined for 192.168.1.0/24 received through Attach\-VPC\-A to Attach\-VPC\-B. |
            

         * The routing table details of the VPC are as follows:

            * Route Table for VPC\-A

               
               |Destination CIDR |Next Hop type |Next hop instance |
               |---|---|---|
               |10.0.1.0/24 |Transit Router |TR\-X |
               |192.168.1.0/24 |Transit Router |TR\-X |
               

            * Route Table for VPC\-B

               
               |Destination CIDR |Next Hop type |Next hop instance |
               |---|---|---|
               |172.16.1.0/24 |Transit Router |TR\-X |
               |172.16.2.0/24 |Transit Router |TR\-X |
               

            * Route Table for VPC\-C

               
               |Destination CIDR |Next Hop type |Next hop instance |
               |---|---|---|
               |172.16.1.0/24 |Transit Router |TR\-X |
               |172.16.2.0/24 |Transit Router |TR\-X |
               

      2. Connectivity and Isolation Verification (Example using Linux ECS instances):​​

         1. Log in to ECS\-A (172.16.1.10) in VPC\-A, and execute `ping 192.168.1.10` and `ping 10.0.1.10` in the command line. Verify connectivity between VPC\-A and VPC\-B/VPC\-C.

         2. Log in to ECS\-B (192.168.1.10) in VPC\-B, and execute `ping 172.16.1.10` and `ping 10.0.1.10` in the command line. Verify connectivity between VPC\-B and VPC\-A/VPC\-C.

         3. Log in to the ECS\-C on VPC\-C (10.0.1.10), then execute ping`172.16.1.10` and `ping 192.168.1.10` in the command line. Verify connectivity between VPC\-C and VPC\-A/VPC\-B.

         4. Expected results:

            * VPC\-A establishes bidirectional connectivity with both VPC\-B and VPC\-C.

            * Network isolation between VPC\-B and VPC\-C.


<span id="JVNisx2b"></span>
### Step 2: Configure the NLB instance

<span id="P1VYqJAK"></span>
#### (1) Create the NLB instance


   1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

   2. In the top menu bar, select the target project and region.

   3. Click **Create NLB**, and configure related parameters according to the table below.

      
      |Parameter |Explanation |Example |
      |---|---|---|
      |**Basic information** |||
      |Regions |Select the Region where the NLB instance resides. After you select a region, the created NLB instance can only be used by resources in the selected region and cannot be migrated. You must confirm that the region of the instance is the same as that of the backend server instance. |China (Beijing) |
      |Name |Type the name of NLB instance. |nlb\-01 |
      |**Network Configuration** |||
      |IP version |Select the private IP address type of the NLB instance. |IPv4 |
      |Network Type (IPv4) |Select the network type for the NLB instance's IPv4 address. |Internet |
      |VPC |Select the Virtual Private Cloud (VPC) to which the NLB instance belongs. You can select all VPCs under the specified Region of the current account, excluding Shared VPCs. |VPC\-A |
      |AZs and Subnets |Select the supported Availability Zone for the NLB instance, and specify the subnet, IP address, and Elastic IP (EIP) for each availability zone.<br><br>NLB supports multi\-AZ active\-active disaster recovery by default, and please select at least 2 availability zones. If higher business reliability is required, you may optionally choose 2 or more availability zones.<br><br><br>* **Subnet**: Provides a private network deployment environment for the NLB instance. The system automatically creates a network interface within the subnet and attaches it to the NLB.<br><br>* **IPv4 address**: Select the allocation method for the IPv4 address of the NLB instance. After the instance is created, all assigned IPv4 addresses cannot be modified.<br><br>   * **Auto IP Assignment**: The system automatically allocates 3 private IPv4 addresses for the network interface associated with the NLB, including 1 VIP and 2 LIPs.<br><br>   * **Custom\-assign IP**: Please manually input an IPv4 address within the subnet range. When typing an IPv4 address as the VIP for the network interface attached to the NLB. The system will automatically assign 2 LIPs.<br><br>* **EIP**: Provides internet capabilities for the NLB instance. Configure this parameter only when the network type (IPv4) is **Internet**.<br><br>   * **Newly purchased EIP**: The ElP is created along with the NLB instance, defaults to pay\-by\-data\-transfer billing method, adopts BGP (Multi\-ISP) as the ISP, and has a bandwidth cap of 200 Mbps. |* Availability zone A<br><br>   * Subnet\-A1 \| 172.16.1.0/24<br><br>   * Automatic IP assignment<br><br>   * New Elastic IP (EIP)<br><br>* Availability Zone B<br><br>   * Subnet\-A2 \| 172.16.2.0/24<br><br>   * Automatic IP assignment<br><br>   * New Elastic IP (EIP) |
      |Security group |Select at least one security group for the NLB instance. |Default |
      

   4. Follow the console guidance to review and accept the Legal.

   5. Click **Buy now** to complete instance creation.

   6. Click **Go to console** to view the newly created instance.


<span id="EInRuRBP"></span>
#### (2) Create server group


   1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

   2. In the left navigation pane, select **Server group**.

   3. In the top menu bar, select the target project and region.

   4. In the left navigation pane, select **Server Group**.

   5. Click **Create server group**, and see the table below to configure the basic information of the server group.

      
      |Parameter |Explanation |Example |
      |---|---|---|
      |Name |Enter server group name |rsp01 |
      |Server Group Type |Select the type of the server group. **For backend servers across VPCs, you must choose the IP type.**  |**IP type** |
      |IP version |Protocol type for the backend server's private IP address. |IPv4 |
      |VPC |Select a server group in the same Virtual Private Cloud (VPC) as the NLB instance. |VPC\-A |
      |Backend protocol |The protocol used by the NLB instance to forward traffic to the backend server. |TCP |
      |Scheduling algorithm |Select the algorithm for forwarding requests to the backend server. |Weighted Round Robin (WRR) |
      |Session Persistence |Enable session persistence<br><br><br>* After the sticky session feature is enabled, the NLB forwards access requests from the same Source IP address to the same backend server for processing.<br><br>* **Session persistence timeout period** ranges from 1 to 3600 seconds. |Disable |
      |Connection Draining |Enable Connection Draining<br><br><br>* After enabling, when a backend server is deleted or a health check exception occurs, existing connections will transmit normally within the connection draining timeout period.<br><br>* **Timeout period of connection draining** ranges from 0 to 900 seconds. |Disable |
      |Client IP Preservation |Whether to enable client IP address preservation. Cannot be enabled when the server group type is set to IP type. |Do not enable |
      |Proxy\-Protocol |Enable the Proxy\-Protocol<br><br>After enabling, NLB instance forwards the Source IP address of the client to the server group through the Proxy\-Protocol protocol. The Proxy\-Protocol needs to be configured on the server. For detailed information on this feature, see [Obtaining client source IP through Proxy Protocol](https://docs.byteplus.com/en/docs/clb/Configuring-a-Layer-4-listener-to-obtain-the-client-source-IP-address). |Disable |
      |All\-port forwarding |When the service ports of all backend servers in the server group are the same as the listening port, you can enable all\-port forwarding.<br><br>When enabled, this server group only supports attaching listeners with all\-port forwarding enabled, and backend servers in the group do not need to specify ports. NLB forwards traffic to backend servers based on the front\-end request port (i.e., listening port) by default. |Disable |
      

   6. Configure health check information according to the table below.

      
      |Parameter |Explanation |Example |
      |---|---|---|
      |Health check |Select whether to enable the health check feature. After enabling health checks, NLB can check whether the backend server status is normal, stop forwarding requests to abnormal backend servers, and ensure overall service availability.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Disabling health checks may result in requests being forwarded to abnormal backend servers. To ensure continuous availability of the service, it is discouraged to disable health checks.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Health checks consume a certain amount of network resources. To minimize their impact on your business operations, it is advised to reduce the health check frequency and increase the interval between checks based on your specific workload.</div><br> |Check |
      |Health check protocol |The protocol type of the health check request. |TCP |
      |Health check port |Configure the port used for the health check. |Use backend server port |
      |Response timeout |Configure the waiting time for the health check response.<br><br><br>* If no valid response is received from the backend server within the response timeout period, the health check is considered abnormal.<br><br>* Value range: 1 to 60 seconds. Default timeout period: 3 seconds. |3 seconds |
      |Detect interval |Enter the interval for performing health checks.<br><br><br>* The detect interval must be greater than or equal to the response timeout period.<br><br>* Value range: 3 to 300 seconds. The default interval is 10 seconds, meaning a health check is performed on the backend server every 10 seconds. |10 seconds |
      |Healthy threshold |After enabling health checks, specify the number of consecutive successful health checks required to consider a backend server normal.<br><br><br>* When the same backend server undergoes consecutive health checks for a specified number of times and all results are **Normal**, its status changes from **Abnormal** to **Normal**.<br><br>* Value range: 2 to 10 times. Default: 3 times. |3 times |
      |Unhealthy threshold |After enabling health checks, enter the number of consecutive health check failures required to determine backend server failure.<br><br><br>* When the same backend server undergoes consecutive health checks for a specified number of times and all results are **Abnormal**, its status changes from **Normal** to **Abnormal**.<br><br>* Value range: 2 to 10 times. Default: 3 times. |3 times |
      

   7. Click **OK** to complete the action.


<span id="umbbNv0Y"></span>
#### (3) Add backend server


   1. Click the name of server group rsp\-01.

   2. Click **Add server**.

   3. Configure relevant parameters based on the table below.

      
      |Parameter |Explanation |ECS\-B serves as the backend server |ECS\-C serves as the backend server |
      |---|---|---|---|
      |IP Address |Input the private IP address of the cross\-VPC Elastic Compute Service (ECS). |192.168.1.10 |10.0.1.10 |
      |Port |Type the port of cross\-VPC Elastic Compute Service (ECS). |80 |80 |
      |Weight |Type the weight of the cross\-VPC Elastic Compute Service (ECS) instance. |100 |100 |
      

   4. Click **Confirm** to complete the action.


<span id="VlPphETd"></span>
#### (4) Add Listener


   1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

   2. In the top menu bar, select the target project and region.

   3. Click **Edit listener** on the right side of the target NLB instance.

   4. Click **Add listener** and see the table below to configure the listener.

      
      |Parameter |Explanation |Example |
      |---|---|---|
      |Listener name |Enter the listener name. If left blank, it defaults to **Protocol\-port**, such as **TCP\-80**. |listener01 |
      |Listening protocol |Select the protocol type for NLB instance listener. This article uses TCP. [Prerequisite](https://docs.byteplus.com/en/docs/clb/NLB-Listener-overview#.55uR5ZCs5Y2P6K6u57G75Z6L) |TCP |
      |Listening port |Enter the listening port. The range is 1 to 65535. |80 |
      |Timeout period |Set the timeout period. If no data is transferred over the connection within the timeout period, it will be automatically disabled.<br><br>For TCP listeners, the timeout period ranges from 10 to 900 seconds, with a default value of 900 seconds. |900 seconds |
      |Tags |A tag consists of a key\-value pair and is used for categorizing and searching resources [Prerequisite](https://docs.byteplus.com/en/docs/clb/NLB-Tag-Management) |* Tag key: listener\-key<br><br>* Tag value: listener\-test |
      

   5. Click **Next** and select a **Server group with TCP protocol**.

   6. Click **Next** to confirm the configuration information.

   7. Click **Confirm** to complete the action.


<span id="b6Uj9b45"></span>
#### (5) Configure Network ACL and Security Group


   * **Security Groups and Network ACLs associated with the NLB instance**

      * Security Group configuration example:

         
         |Rule direction |Priority |Strategy |Protocol type |Port range |Source/destination address |Description |
         |---|---|---|---|---|---|---|
         |Inbound |1 |Allow |Listening protocol: TCP |Listening port: 80 |Client address: 0.0.0.0/0 |Allow inbound client traffic to the NLB |
         ||1 |Allow |ICMP |ALL |100.64.0.0/10 |Allow traffic to detect the availability of the NLB instance private IPv4 address |
         ||1 |Deny |TCP |80 |Access to the NLB's IP address is not allowed |Deny specified IP addresses from accessing the NLB |
         |Outbound |100 |Allow |ALL |ALL |0.0.0.0/0 |Allow\-all fallback policy |
         

      * Network ACL Configuration Example (NOTE: If no network ACLs are associated with the NLB's subnets, this configuration is unnecessary and may be ignored):

         
         |Rule direction |Priority |Policy |Agreement |Source/destination address |Destination port |Description |
         |---|---|---|---|---|---|---|
         |Inbound |1 |Allow |Listening protocol (TCP) |0.0.0.0/0 |Listening port<br><br>(80) |Allow inbound client traffic to the NLB |
         ||2<br><br> |<div style="text-align: center"><br>Allow</div><br><br><br><div style="text-align: center"><br></div><br> |Listening protocol and health check protocol<br><br>(both are TCP) |Backend server private IP address (192.168.1.10) |Backend server port and health check port (both port 80) |Allow health check response traffic from backend servers to the NLB, allow client\-originated response traffic from backend servers to the NLB |
         ||3 |Allow |ICMP |100.64.0.0/10 |ALL |Allow traffic for system probes to detect the availability of the NLB private IPv4 address |
         |Outbound |1 |Allow |ALL |0.0.0.0/0 |ALL |Allow all IPv4 traffic |
         

   * **Security Groups and Network ACLs associated with the backend servers**

      * Security Group configuration example:

         
         |Rule direction |Priority |Policy |Protocol type |Port range |Source |Description |
         |---|---|---|---|---|---|---|
         |Inbound |1 |Allow |Listening protocol and health check protocol<br><br>(both TCP) |Backend server port and health check port (both port 80) |CIDR block of the subnet where the NLB instance resides. (172.16.1.0/24, 172.16.2.0/24) |Allow both request forwarding traffic and health check traffic from NLB to backend servers |
         

      * Network ACL Configuration Example (NOTE: If no network ACLs are associated with the backend servers, this configuration is unnecessary and may be ignored)

         
         |Rule direction |Priority |Policy |Agreement |Source/destination address |Destination port |Description |
         |---|---|---|---|---|---|---|
         |Inbound<br><br> |1 |Allow<br><br> |Listening protocol and health check protocol<br><br>(both TCP) |Source address: CIDR blocks of the subnet where the NLB instance resides (172.16.1.0/24, 172.16.2.0/24) |Backend server port and health check port (both port 80) |Allow both request forwarding traffic and health check traffic from NLB to backend servers |
         |Outbound |1 |Allow |ALL |Destination: 0.0.0.0/0 |ALL |Allow all traffic |
         

      For more details, see [Configuring NLB security groups and Network ACLs](https://docs.byteplus.com/en/docs/clb/Configuring-security-group-and-Network-ACL-for-NLB) and [Configuring backend server security groups and Network ACLs](https://docs.byteplus.com/en/docs/clb/NLB-Configuring-backend-server-security-group-and-Network-ACL).


<span id="VWEMsALX"></span>
### Step 3: Resolve your custom domain name to the NLB domain name

BytePlus does not allow users to **Directly** use the default domain name provided by the NLB service for **Internet** access. If you need to provide services to the internet through an NLB instance, please use your own domain name and resolve it via CNAME to the NLB domain name. If you do not have your own domain name, see [BytePlus Domain Names](https://docs.byteplus.com/en/docs/domain-names/introduction_en).

<div data-tips="true" data-tips-type="tip">Explanation</div>


<div data-tips="true" data-tips-type="tip">This example uses configuring resolution records in BytePlus's DNS service. If you manage your business domain name on another platform, please configure resolution records on the corresponding platform.</div>



1. Log in to the.

2. See [Map Your Domain Name to a CDN CNAME](https://docs.byteplus.com/en/docs/byteplus-dns-suite/Map_Your_Domain_Name_to_a_CDN_CNAME) to resolve your domain name to the NLB instance domain name and verify that the configuration is effective. The parameter description is shown in the table below.

   
   |Parameter |Description |
   |---|---|
   |Domain name |Set it to the host record (domain prefix) of your own domain name. For example: `www`. |
   |Record type |Set to **CNAME**. |
   |Record value |Set to the domain name of your NLB instance. In this example: `nlb-2fe5ahfkoi9s059gp683y****.cn-beijing.nlb.volces.com`. |
   |<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For parameters not mentioned above, please keep the default values.</div><br> ||
   


<span id="HA0n1Xfd"></span>
## Verification


1. Open the browser on your local computer.

2. Input `http://your custom domain name`, if the application page deployed by the backend server is displayed, it indicates that your business has successfully configured the NLB.
