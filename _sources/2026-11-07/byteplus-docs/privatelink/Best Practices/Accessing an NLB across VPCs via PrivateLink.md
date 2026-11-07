---
title: "Accessing an NLB across VPCs via PrivateLink"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Accessing_an_NLB_across_VPCs_via_PrivateLink"
---

Use PrivateLink to access Network Load Balancer (NLB) across VPCs, achieving secure, private, and controllable Layer 4 load balancing service sharing.

<span id="sIJCIBr7"></span>
## Background introduction

A company has multiple businesses. It deploys core services (such as identity authentication services) in one VPC and shares these services with other VPCs through PrivateLink, avoiding duplicate deployment and reducing operational costs.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f3bfe5f42aefa6a31b2f185a7ddd1f43.png) </span>

<span id="9X62i9wt"></span>
## Data planning


|Account |Resource type |Resource name |CIDR block/IP address |Comment |
|---|---|---|---|---|
|Service provider |Virtual Private Cloud (VPC) |VPC\-Provider |192.168.0.0/16 |Located in China (Beijing) |
||Subnet |Subnet\-A |192.168.1.0/24 |Located in Availability Zone A |
|||Subnet\-B |192.168.2.0/24 |Located in Availability Zone B |
||ECS |ECS\-Provider\-A |192.168.1.11 |Not bound to EIP |
|||ECS\-Provider\-B |192.168.2.22 |Not bound to EIP |
||NLB |NLB\-X |\-\- |Private network type |
||Endpoint service |\-\- |\-\- |Automatically accept endpoint connections |
|Service consumer |Virtual Private Cloud (VPC) |VPC\-User |172.16.0.0/16 |Located in China (Beijing) |
||Subnet |Subnet\-C |172.16.1.0/24 |Located in Availability Zone A |
||ECS |ECS\-User |172.16.1.11 |Not bound to EIP |
||End point node |endpoint01 |\-\- |\-\- |


<span id="TYMplQky"></span>
## Preparations


1. Create two BytePlus accounts and complete real\-name authentication for both.

2. In the service provider account and the service consumer account, configure VPCs, subnets, and ECSs according to the data planning described above.

3. Deploy services within the ECS instances (ECS\-Provider\-A, ECS\-Provider\-B) of the service provider. For operations, see [Building the backend services](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTP-static-page#.5q2l6aqk5LqM77ya5pCt5bu65ZCO56uv5pyN5Yqh).


<span id="OwZ1zBXa"></span>
## Procedures

<span id="bs36TAI3"></span>
### Step 1: Configure NLB

<span id="VEfBmEAa"></span>
#### (1) Create the NLB instance


   1. Use the service provider account to log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">During initial login, follow the on\-screen instruction to complete cross\-service role authorization.      </div>
      

   2. Click **Create NLB** and configure the related parameters according to the table below.

      
      |Parameters |Notes |Example |
      |---|---|---|
      |**Basic information** |||
      |Region |Select the region where the NLB instance resides. After selection, the created NLB instance can only serve resources within its selected region and cannot be migrated. |China (Beijing) |
      |Name |Type the name of the NLB instance. |NLB\-X |
      |**Network configuration** |||
      |IP Version |Select the private IP address type of the NLB instance.<br><br><br>* IPv4: Only IPv4 is supported.<br><br>* Dual\-stack: Both IPv4 and IPv6 are supported.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">NLB IPv6 feature is currently in Beta stage. For trial requests, please contact your account manager.</div><br> |IPv4 |
      |Network Type (IPv4) |Select the network type for the IPv4 address of the NLB instance. The two network types can be interchanged. For detailed information, see [Changing IPv4 network type](https://docs.byteplus.com/en/docs/clb/Changing-Network-Load-Balancer-instance-network-type).<br><br><br>* **Public**: The NLB instance can be accessed by both the IPv4 private network and the IPv4 internet.<br><br>* **Private**: This NLB instance can only be accessed by the IPv4 private network. |VPC |
      |VPC |Select the VPC to which the NLB instance belongs. |VPC\-Provider |
      |Availability Zone and Subnet |Select the supported Availability Zone for the NLB instance, and specify the subnet, IP address, and Elastic IP (EIP) for each availability zone.<br><br>NLB supports multi\-AZ active\-active disaster recovery by default, and please select at least 2 availability zones. If higher business reliability is required, you may optionally choose 2 or more availability zones.<br><br><br>* Subnet: Provides a VPC deployment environment for the NLB instance. The system automatically creates a network interface within the subnet and attaches it to the NLB.<br><br>* IPv4 address: Select the allocation method for the IPv4 address of NLB instance. After the instance is created, all assigned IPv4 addresses cannot be modified.<br><br>* EIP: Provides internet capabilities for the NLB instance. Configure this parameter only when the network type (IPv4) is **Internet**. |* AZ\-A<br><br>   * Subnet\-A \| 192.168.1.0/24<br><br>   * Auto\-assign IP<br><br>   * Newly purchased EIP<br><br>* Availability Zone B<br><br>   * Subnet\-B \| 192.168.2.0/24<br><br>   * Auto\-assign IP<br><br>   * Newly purchased EIP |
      |Security Group |Select at least one security group for the NLB instance. |default |
      

   3. In the **Configuration Details** window on the right side of the page, check and confirm the Legal as guided by the console.

   4. Click **Submit order** to complete the instance creation.

   5. Click **Go to console** to view and record the domain name of the newly created NLB instance.


<span id="gn7yVdve"></span>
#### (2) Create server group and add backend server


   1. In the left navigation pane, select **Server Group**.

   2. Click **Create server group**, and configure parameters according to the table below.

      
      |Parameters |Notes |Example |
      |---|---|---|
      |Name |Enter server group name |rsp01 |
      |Server group type |Select the type of the server group.<br><br><br>* Server type: Only the Elastic Compute Service (ECS) instances or secondary network interfaces within the same VPC as the server group can be added as backend servers.<br><br>* IP type: You can only add IP addresses as backend servers. You can add IP addresses from other VPCs or on\-premises IDCs as backend servers, as long as they are network\-reachable. |Server type |
      |IP Version |Protocol type for the backend server's private IP address.<br><br><br>* IPv4: Only IPv4 backend servers can be added.<br><br>* IPv6: Only IPv6 backend servers can be added. IPv6 is only supported when the NLB instance is dual\-stack and the backend server group uses **Server type** targets.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When IPv6 access requests are forwarded to IPv4 backend servers, the IPv6 will first be converted to IPv4, and then forwarded to the IPv4 backend servers.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When forwarding IPv4 access requests to an IPv6 backend server, IPv4 is first converted to IPv6 and then forwarded to the IPv6 backend server.</div><br> |IPv4 |
      |VPC |Select a server group in the same VPC as the NLB instance. |VPC\-Provider |
      |Protocol |The protocol used by the NLB instance to forward requests to the backend server. |TCP |
      |Load balancing algorithm |Select the rules that the server group follows to forward requests.<br><br><br>* Weighted Round Robin (WRR): Higher weights values receive more frequent polling attempts (higher probability).<br><br>* Weighted Least Connections (WLC): First calculate the current connections/weight value of the backend server, then dispatch the request to the backend server with the smallest value.<br><br>* Source Address Hash (SH): A consistency hash based on the Source IP address, allowing the same source to be scheduled to the same backend server. |Weighted Round Robin (WRR) |
      

   3. Enable **Health check**, keep the remaining parameters at their default values.

   4. Click **Create** to complete the creation of the server group.

   5. Click  **··· \> Add server** to the right of the target server group.

   6. Click **Add server** and select the target ECS instance.

   7. Click **Next** to configure ports and weight for the added backend servers.

      
      |Parameters |Notes |Example |
      |---|---|---|
      |Port |The port on which the backend server provides services. |80 |
      |Weight |The probability of the backend server receiving a request (probability = the server weight / the sum of all servers' weights in the group).<br><br><br>* The larger the weight, the more requests are forwarded, and the default is 100.<br><br>* A weight of 0 indicates that the server will no longer accept new requests.<br><br>* If the scheduling algorithm is Source IP Hash (SH), weights only distinguish between 0 and non\-zero values. |100 |
      

   8. Click **Confirm** to complete the action.


<span id="0ZNOflAx"></span>
#### (3) Add listener


   1. In the left\-side navigation pane, select **Instances**.

   2. Click **Edit listener** on the right of the target NLB instance.

   3. Click **Add listener** and see table below to configure relevant parameters.

      
      |Parameters |Notes |Example |
      |---|---|---|
      |Listener name |Enter the listener name. If left empty, it defaults to **protocol\-port**, such as TCP\-80. |listener01 |
      |Listener protocol |Select the protocol type for NLB instance listener. [Learn more](https://docs.byteplus.com/en/docs/clb/NLB-Listener-overview#.55uR5ZCs5Y2P6K6u57G75Z6L) |TCP |
      |Listener port |Select the port type and enter the port. The port value ranges from 1 to 65535. [Learn more](https://docs.byteplus.com/en/docs/clb/NLB-Listener-overview) |80 |
      |Timeout |Set the timeout period. If no data is transferred over the connection within the timeout period, it will be automatically disabled. The value ranges from 10 to 900 seconds, with a default of 900 seconds. |900 seconds |
      

   4. Click **Next** and select the Server Group created above.

   5. Click **Next** to confirm the configuration information.

   6. Click **Confirm** to complete the action.


<span id="7SfvetKY"></span>
#### (4) Configure security group and network ACL


   * **Configure security group**

      For actions, see [Adding a security group rule](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules). Example configuration in this topic:

      * Security group associated with the NLB instance

         
         |Rule direction |Priority |Policy |Agreement |Port range |Source/destination address |Description |
         |---|---|---|---|---|---|---|
         |Inbound |1 |Allow |TCP |80 |Source address: 0.0.0.0/0 |Allow client access traffic to the NLB (in this case, TCP traffic on port 80) |
         ||1 |Allow |ICMP |ALL |100.64.0.0/10 |Allow traffic to detect the availability of the NLB instance private IPv4 address |
         ||1 |Deny |TCP |80 |Access to the NLB's IP address is not allowed |Deny specified IP addresses from accessing the NLB |
         |Outbound |100 |Allow |ALL |ALL |Destination: 0.0.0.0/0 |Allow\-all fallback policy |
         

      * Security group associated with the backend servers.

         
         |Rule direction |Priority |Policy |Agreement |Port range |Source |Description |
         |---|---|---|---|---|---|---|
         |Inbound |1 |Allow |TCP |80 |192.168.1.0/24, 192.168.2.0/24 |Allow both request forwarding traffic and health check traffic from NLB to backend servers |
         

   * **Configure Network ACL**

      For actions, see [Adding a Network ACL rule](https://docs.byteplus.com/en/docs/vpc/Managing-network-ACL-rules). If no subnet associated with the NLB has a Network ACL attached, the NLB example can be ignored. If no subnet associated with the backend servers has a Network ACL attached, the backend server example can be ignored.

      * NLB instance

         
         |Rule direction |Priority |Policy |Agreement |Source/destination address |Destination port |Description |
         |---|---|---|---|---|---|---|
         |Inbound |1 |Allow |TCP |0.0.0.0/0 |80 |Allow inbound client traffic to the NLB |
         ||2<br><br> |Allow<br><br> |TCP |192.168.1.11, <br><br>192.168.2.22 |80 |Allow health check response traffic from backend servers to the NLB, allow client\-originated response traffic from backend servers to the NLB |
         ||3 |Allow |ICMP |100.64.0.0/10 |ALL |Allow traffic for system probes to detect the availability of the NLB private IPv4 address |
         |Outbound |1 |Allow |ALL |0.0.0.0/0 |ALL |Allow all IPv4 traffic |
         

      * Backend server

         
         |Rule direction |Priority |Policy |Agreement |Source/destination address |Destination port |Description |
         |---|---|---|---|---|---|---|
         |Inbound<br><br> |1 |Allow<br><br> |TCP |192.168.1.0/24, 192.168.2.0/24 |80 |Allow both request forwarding traffic and health check traffic from NLB to backend servers |
         |Outbound |1 |Allow |ALL |0.0.0.0/0 |ALL |Release all traffic |
         

      For more details, see [Configuring NLB security groups and Network ACLs](https://docs.byteplus.com/en/docs/clb/Configuring-security-group-and-Network-ACL-for-NLB) and [Configuring backend server security groups and Network ACLs](https://docs.byteplus.com/en/docs/clb/NLB-Configuring-backend-server-security-group-and-Network-ACL).


<span id="g9c4n4Ow"></span>
### Step 2: Configure PrivateLink

<span id="VnW5FwQ0"></span>
#### (1) Create endpoint service


   1. Log in to the [Endpoint Service console](https://console.byteplus.com/pl/endpointServices) using the service provider account.

   2. Only accounts that have not completed cross\-service role authorization need to perform this. If already authorized, ignore this step.

      1. On the **Cross\-service access request** page, click **Authorize**.

         * The authorized role will be displayed in the role list of the Identity and Access Management (IAM) platform. Deleting the authorized role may cause cross\-service access failures. Proceed with caution.

         * If the authorization role is deleted and you need to continue using the PrivateLink service, you must re\-authorize the role.

      2. In the left navigation tree, click **Endpoint Service** again.

   3. In the top menu bar, select the target project and region.

   4. Click **Create Endpoint Service** and configure the parameters according to the table below.

      
      |Parameters |Notes |Example |
      |---|---|---|
      |**Basic information** |||
      |Region |Select the region to which the endpoint service belongs. |China (Beijing) |
      |Name |The name of the endpoint service does not need to be filled in manually. Once the endpoint service is created successfully, the system automatically generates it in the format of `com.volces.privatelink.<regionID>.<endpointserviceID>`. |\-\- |
      |**Service Resource** |||
      |Type |Select the service resource type provided by the endpoint service. |Network Load Balancer (NLB) |
      |Service Resource |Select the **NLB instance** to be used as the service resource. |NLB\-X |
      |**Advanced options** |||
      |Auto accept connection |Auto\-accept endpoint connection<br><br><br>* **Yes:**  Automatically accept connection requests from endpoints.<br><br>* **No**: If No is selected, after the endpoint is created, you must manually accept the connection request from the endpoint. For the procedure, see [Accepting an endpoint connection](https://docs.byteplus.com/en/docs/privatelink/Accepting-Rejecting-endpoint-connection). |Yes |
      

   5. Click **Create** to complete the action.


<span id="QLvSGxCD"></span>
####  **(2) Configure allowlist**


If the service consumer and service provider are the same account, ignore this operation.

   1. Log in to the [Endpoint Service console](https://console.byteplus.com/pl/endpointServices) using the service provider account.

   2. In the top menu bar, select the target project and region.

   3. Click the service ID of the target endpoint service and select the **Allowlist** tab.

   4. Click **Add allowlist**, and configure the allowlist according to the table below.

      
      |Parameters |Notes |Example |
      |---|---|---|
      |Allowlist range |Select the allowlist range of endpoint service.<br><br><br>* Specified account: Only allows endpoints under the specified accounts to establish connections with this endpoint service and access its service resources.<br><br>* All accounts: Allows endpoints under any account to establish connections with this endpoint service and access its service resources. |Specified Account |
      |Account ID |Enter the ID(s) of the target account(s). Separate multiple IDs with line breaks. Each operation supports entering multiple account IDs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When <strong>Allowlist range</strong> is set to <strong>All accounts</strong>, this parameter does not need to be configured.</div><br> |2100000001 |
      

   5. Click **Add** to complete the action.


<span id="thAh0Tlz"></span>
#### (3) Create endpoint


   1. Log in to the [Endpoint console](https://console.byteplus.com/pl/endpoints) using the Service consumer's account.

   2. Refer to the steps below to complete the cross\-service role authorization.

      Only accounts that have not completed cross\-service role authorization need to perform this. If already authorized, ignore this step.

      1. On the **Cross\-service access request** page, click **Authorize**.

         * The authorized role will be displayed in the role list of the Identity and Access Management (IAM) platform. Deleting the authorized role may cause cross\-service access failures. Proceed with caution.

         * If the authorization role is deleted and you need to continue using the PrivateLink service, you must re\-authorize the role.

      2. In the left navigation tree, click **Endpoint** again.

   3. Click **Create Endpoint** and configure the parameters according to the table below.

      
      |Parameters |Notes |Example |
      |---|---|---|
      |**Basic information** |||
      |Region |Select the region of endpoint. |China (Beijing) |
      |Name |Enter the name of endpoint. |endpoint01 |
      |Type |Select the type of endpoint. |Interface |
      |**Endpoint service** |||
      |Add method |Select the method for associating an endpoint service. It supports two methods: Add by Service Name and Select available service. |Select available service |
      |Endpoint service |Select the endpoint service created in the previous steps. |com.volces.privatelink.cn\-guangzhou.epsvc\-2fe630gurkl37k5gfuy33\*\*\*\* |
      |**Network configuration** |||
      |VPC |Select the VPC to which the endpoint belongs. |VPC\-User |
      |Availability Zone and Subnet |Check the box for the Availability Zones of the endpoint service where you need to establish connections and select the corresponding subnet for each.<br><br>After a subnet is selected, the system will automatically create an endpoint network interface for you. |Availability zone A, subnet01, Auto\-assign IP |
      |Security Group |Select the security group(s) to be associated with the endpoint's network interface. |Default\-sg |
      

   4. Click **Confirm order** according to the console instructions to review and confirm the Legal.

   5. Click **Buy now** to check whether the creation is successful.

   6. Click **Go to console** to view and record the domain name of the successfully created endpoint, as it will be needed for verification.


<span id="y6Mhoiqm"></span>
## Verify


1. Remotely log in to the Elastic Compute Service (ECS) in VPC\-User. For specific actions, see [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the `curl http://endpoint domain:listener port` command to test network connectivity.

   For example, if the endpoint domain name is `ep-2fegvybuk2yv459gp68nbk2e7.epsvc-2fegvxu3a2h3459gp67rdzvhe.cn-guangzhou.privatelink.volces.com` and the listening port of the service resource NLB instance is 80, execute `curl http://ep-2fegvybuk2yv459gp68nbk2e7.epsvc-2fegvxu3a2h3459gp67rdzvhe.cn-guangzhou.privatelink.volces.com:80`.

   If the returned result displays the content of the backend service page configured on the backend server, it indicates successful network connectivity.
