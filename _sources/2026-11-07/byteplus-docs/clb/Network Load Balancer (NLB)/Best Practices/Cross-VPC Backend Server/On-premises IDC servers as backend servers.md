---
title: "On-premises IDC servers as backend servers"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-On-premises-IDC-servers-as-backend-servers"
---

This topic provides a step\-by\-step guide to configuring on\-premises IDC server instances as backend servers for your Network Load Balancer (NLB).

<span id="HoP0chjl"></span>
## Scenarios

The NLB forwards access requests to servers within your on\-premises IDC for processing. The figure demonstrates:

> The diagram displays sample configurations for each service. Modify these values according to your actual network architecture during implementation.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ea900fd380c444e5fadd58d2fa505c19.png) </span>

The following diagram illustrates a sample configuration:


* Virtual Private Cloud VPC\-A: CIDR block `172.16.0.0/16`.

   * The CIDR block of Subnet\-A1 is `172.16.1.0/24`.

   * The CIDR block of Subnet\-A2 is `172.16.2.0/24`.

   * The private IP address of ECS\-A is `172.16.1.10`.

* Data Center (IDC):

   * The local gateway IP address is `10.0.0.2`.

   * CIDR block: `192.168.1.0/24`

   * The server IP address is `192.168.1.10`.


<span id="SWxC3ztL"></span>
## Preparations


1. Using your BytePlus account, create one VPC in the China (Beijing) region, with configurations matching the parameters described in the [Background section above](https://docs.byteplus.com/en/docs/natgateway/Configuring-multiple-Internet-NAT-Gateways-in-a-VPC#.6IOM5pmv5LuL57uN). For specific actions, see [Creating a Virtual Private Cloud](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

2. Create ECS\-A (172.16.1.10) in Subnet\-A1 of VPC\-A. For more information, see [Purchasing an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

3. To establish connectivity between your on\-premises IDC and cloud\-based VPCs, see [Using Cloud Enterprise Network (CEN) for cloud-to-on-premises IDC connectivity](https://docs.byteplus.com/en/docs/directconnect/Quick-start) and [Implementing Transit Routers for VPC-to-IDC interconnection](https://docs.byteplus.com/en/docs/transitrouter/Best-Practices-02).


<span id="Vj0efRLM"></span>
## Configuration procedures

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following section only covers essential parameters and their recommended values when configuring each service resource. For all parameters not explicitly discussed, retain the default settings unless otherwise required by your specific use case.</div>


<span id="88rKfGEw"></span>
### Step 1: Verify connectivity between on\-premises data center and VPCs


1. Log in to server A whose IP address is 172.16.1.10.

2. Execute the `ping 192.168.1.10` command in the command line.

3. A successful `ping` response confirms connectivity between your on\-premises data center and VPCs.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If <code>ping</code> fails, see <a href="https://docs.byteplus.com/en/docs/directconnect/Direct-Connect-gateway#.5bey5a6M5oiQ5LqR5LiK5LqR5LiL6YWN572u77yM5L2G572R57uc5LuN54S25LiN6YCa77yM5aaC5L2V5o6S5p-l77yf">Troubleshooting Network Connectivity Issues After Cloud\-to\-On\-Premises Configuration</a>.</div>


<span id="LeZ5C1UM"></span>
### Step 2: Configure NLB instance

<span id="nerbbmvV"></span>
#### (1) Create NLB instance


   1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

   2. In the top menu bar, select the target project and region.

   3. Click **Create NLB**, and configure related parameters according to the table below.

      
      |Parameter |Explanation |Example |
      |---|---|---|
      |**Basic information** |||
      |Region |Select the Region where the NLB instance resides. After you select a region, the created NLB instance can only be used by resources in the selected region and cannot be migrated. You must confirm that the region of the instance is the same as that of the backend server instance. |China (Beijing) |
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


<span id="h5Gvb947"></span>
#### (2) Create server group


   1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

   2. In the top menu bar, select the target project and region.

   3. In the left navigation pane, select **Server group**.

   4. Click **Create server group**, and refer to the table below to configure the basic information of the server group.

      
      |Parameter |Explanation |Example |
      |---|---|---|
      |Name |Enter server group name |rsp01 |
      |Server Group Type |Select the type of the server group. **When using on\-premises IDC servers as backend servers, you must configure them as IP targets.**  |**IP type** |
      |IP version |Protocol type for the backend server's private IP address. |IPv4 |
      |VPC |Select a server group in the same Virtual Private Cloud (VPC) as the NLB instance. |VPC\-A |
      |Backend protocol |The protocol used by the NLB instance to forward traffic to the backend server. |TCP |
      |Scheduling algorithm |Select the algorithm for forwarding requests to the backend server. |Weighted Round Robin (WRR) |
      |Session Persistence |Enable session persistence<br><br><br>* After the sticky session feature is enabled, the NLB forwards access requests from the same Source IP address to the same backend server for processing.<br><br>* **Session persistence timeout period** ranges from 1 to 3600 seconds. |Disable |
      |Connection Draining |Enable Connection Draining<br><br><br>* After enabling, when a backend server is deleted or a health check exception occurs, existing connections will transmit normally within the connection draining timeout period.<br><br>* **Timeout period of connection draining** ranges from 0 to 900 seconds. |Disable |
      |Client IP Preservation |Whether to enable client IP address preservation. Cannot be enabled when the server group type is set to IP type. |Do not enable |
      |Proxy\-Protocol |Enable the Proxy\-Protocol<br><br>After enabling, NLB instance forwards the Source IP address of the client to the server group through the Proxy\-Protocol protocol. The Proxy\-Protocol needs to be configured on the server. For detailed information on this feature, see [Obtaining client source IP through Proxy Protocol](https://docs.byteplus.com/en/docs/clb/Configuring-a-Layer-4-listener-to-obtain-the-client-source-IP-address). |Disable |
      |All\-port forwarding |When the service ports of all backend servers in the server group are the same as the listening port, you can enable all\-port forwarding.<br><br>When enabled, this server group only supports attaching listeners with all\-port forwarding enabled, and backend servers in the group do not need to specify ports. NLB forwards traffic to backend servers based on the front\-end request port (i.e., listening port) by default. |Disable |
      

   5. Configure health check information according to the table below.

      
      |Parameter |Explanation |Example |
      |---|---|---|
      |Health check |Select whether to enable the health check feature. After enabling health checks, NLB can check whether the backend server status is normal, stop forwarding requests to abnormal backend servers, and ensure overall service availability.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Disabling health checks may result in requests being forwarded to abnormal backend servers. To ensure continuous availability of the service, it is discouraged to disable health checks.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Health checks consume a certain amount of network resources. To minimize their impact on your business operations, it is advised to reduce the health check frequency and increase the interval between checks based on your specific workload.</div><br> |Check |
      |Health check protocol |The protocol type of the health check request. |TCP |
      |Health check port |Configure the port used for the health check. |Use backend server port |
      |Response timeout |Configure the waiting time for the health check response.<br><br><br>* If no valid response is received from the backend server within the response timeout period, the health check is considered abnormal.<br><br>* Value range: 1 to 60 seconds. Default timeout period: 3 seconds. |3 seconds |
      |Detect interval |Enter the interval for performing health checks.<br><br><br>* The detect interval must be greater than or equal to the response timeout period.<br><br>* Value range: 3 to 300 seconds. The default interval is 10 seconds, meaning a health check is performed on the backend server every 10 seconds. |10 seconds |
      |Healthy threshold |After enabling health checks, specify the number of consecutive successful health checks required to consider a backend server normal.<br><br><br>* When the same backend server undergoes consecutive health checks for a specified number of times and all results are **Normal**, its status changes from **Abnormal** to **Normal**.<br><br>* Value range: 2 to 10 times. Default: 3 times. |3 times |
      |Unhealthy threshold |After enabling health checks, enter the number of consecutive health check failures required to determine backend server failure.<br><br><br>* When the same backend server undergoes consecutive health checks for a specified number of times and all results are **Abnormal**, its status changes from **Normal** to **Abnormal**.<br><br>* Value range: 2 to 10 times. Default: 3 times. |3 times |
      

   6. Click **OK** to complete the action.


<span id="SbCx7PBp"></span>
#### (3) Add backend server


   1. Click the name of server group rsp\-01.

   2. Click **Add server**.

   3. Configure relevant parameters based on the table below.

      
      |Parameter |Explanation |Value |
      |---|---|---|
      |IP Address |Enter the private IP address of the on\-premises IDC server. |192.168.1.10 |
      |Port |Enter the port of the data center server. |80 |
      |Weight |Enter the weight of the data center server. |100 |
      

   4. Click **Confirm** to complete the action.


<span id="2nsoxRTD"></span>
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


<span id="TGJKmAJH"></span>
#### (5) Configure Network ACL and Security Group


   * **Security Groups and Network ACLs associated with the NLB instance**

      * Security Group configuration example:

         
         |Direction |Priority |Policy |Protocol type |Port range |Source/destination address |Description |
         |---|---|---|---|---|---|---|
         |<div style="text-align: center"><br>Inbound</div><br> |1 |Allow |Listening protocol: TCP |Listening port: 80 |Client address: 0.0.0.0/0 |Allow inbound client traffic to the NLB |
         ||1 |Allow |ICMP |ALL |100.64.0.0/10 |Allow traffic to detect the availability of the NLB instance private IPv4 address |
         ||1 |Deny |TCP |80 |Access to the NLB's IP address is not allowed |Deny specified IP addresses from accessing the NLB |
         |Outbound |100 |Allow |ALL |ALL |0.0.0.0/0 |Allow\-all fallback policy |
         

      * Network ACL Configuration Example (NOTE: If no network ACLs are associated with the NLB's subnets, this configuration is unnecessary and may be ignored):

         
         |Rule direction |Priority |Policy |Agreement |Source/destination address |Destination port |Description |
         |---|---|---|---|---|---|---|
         |Inbound |1 |Allow |Listening protocol (TCP) |0.0.0.0/0 |Listening port<br><br>(80) |Allow inbound client traffic to the NLB |
         ||2<br><br> |<div style="text-align: center"><br>Allow</div><br><br><br><div style="text-align: center"><br></div><br> |Listening protocol and health check protocol<br><br>(both TCP) |Backend server private IP address (192.168.1.10) |Backend server port and health check port (both port 80) |Allow health check response traffic from backend servers to the NLB, allow client\-originated response traffic from backend servers to the NLB |
         ||3 |Allow |ICMP |100.64.0.0/10 |ALL |Allow traffic for system probes to detect the availability of the NLB private IPv4 address |
         |Outbound |1 |Allow |ALL |0.0.0.0/0 |ALL |Allow all IPv4 traffic |
         

   * **Backend server**

      On\-premises IDC backend servers must allow both request forwarding traffic and health check traffic from NLB to backend servers

   For more details, see [Configuring the NLB security groups and Network ACLs](https://docs.byteplus.com/en/docs/clb/Configuring-security-group-and-Network-ACL-for-NLB) and [Configuring the backend server security groups and Network ACLs](https://docs.byteplus.com/en/docs/clb/NLB-Configuring-backend-server-security-group-and-Network-ACL).


<span id="0Fkbb57Y"></span>
### Step 3: Resolve your custom domain name to the NLB domain name

BytePlus does not allow users to **Directly** use the default domain name provided by the NLB service for **Internet** access. If you need to provide services to the internet through an NLB instance, please use your own domain name and resolve it via CNAME to the NLB domain name. If you do not have your own domain name, see  [BytePlus Domain Names](https://docs.byteplus.com/en/docs/domain-names/introduction_en).

<div data-tips="true" data-tips-type="tip">Explanation</div>


<div data-tips="true" data-tips-type="tip">This example uses configuring resolution records in BytePlus's DNS service. If you manage your business domain name on another platform, please configure resolution records on the corresponding platform.</div>



1. Log in to the [DNS console](https://console.byteplus.com/dns-suite/dns/publiczone/zones?).

2. See [Map Your Domain Name to a CDN CNAME](https://docs.byteplus.com/en/docs/byteplus-dns-suite/Map_Your_Domain_Name_to_a_CDN_CNAME) to resolve your custom domain name to the NLB instance's domain name and verify whether the configuration takes effect. The parameter description is shown in the table below.

   
   |Parameter |Description |
   |---|---|
   |Domain name |Set it to the host record (domain prefix) of your own domain name. For example: `www`. |
   |Record type |Set to **CNAME**. |
   |Record value |Set to the domain name of your NLB instance. In this example: `nlb-2fe5ahfkoi9s059gp683y****.cn-beijing.nlb.volces.com`. |
   |<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For parameters not mentioned above, please keep the default values.</div><br> ||
   


<span id="05tEUcNx"></span>
## Verification


1. Open the browser on your local computer.

2. Input `https://your custom domain name`, if the application page deployed by the backend server is displayed, it indicates that your business has successfully configured the NLB.
