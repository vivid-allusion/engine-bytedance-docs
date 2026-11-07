---
title: "Migrating from CLB to NLB"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Migrating-from-CLB-to-NLB"
---

This topic describes how to migrate Layer\-4 load balancer from a CLB instance to an NLB instance.

<span id="75jDO0OG"></span>
## Background introduction

For Layer\-4 load balancer, NLB offers the following advantages over CLB:


* **Higher performance**: Compared to CLB, NLB supports higher\-performance elastic forwarding capabilities for Layer 4 load balancing, helping you easily handle high\-concurrency tasks (a single instance supports up to billions of concurrent connections and 100Gbps bandwidth).

* **More reliable disaster recovery**: Features active\-active deployment across Availability Zones with seamless failover during faults (CLB uses an active\-standby mode, which involves a delay during switchover).

* **Richer feature set**: For example, NLB supports multiple all\-port listeners and allows custom definition of health check ports.


Example: A company initially used CLB to set up Layer\-4 load balancer for distribution and high availability. As business expanded, CLB's performance could no longer meet the demands for high concurrency and low latency, prompting a seamless migration to NLB.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d122b9f6eba47b25de910162d5afabec.png) </span>

<span id="qZif5p5J"></span>
## Data planning


* **Backend server**

   
   |Resource type |Resource name |CIDR block/IP address |Comment |
   |---|---|---|---|
   |VPC |VPC\-X |192.168.0.0/16 |Located in China (Beijing) |
   |Subnet |Subnet\-A |192.168.1.0/24 |Located in Availability Zone A |
   ||Subnet\-B |192.168.2.0/24 |Located in Availability Zone B |
   |ECS |ECS\-A |192.168.1.11 |Not bound to EIP |
   ||ECS\-B |192.168.2.22 |Not bound to EIP |
   

* **Classic Load Balancer**

   The business domain is `www.example.com`, and a temporary domain is `abc.example.com`.

   
   |Resource type |Resource name |Network type |Domain name |
   |---|---|---|---|
   |CLB |CLB\-X |Public |\-\- |
   |NLB |NLB\-X |Public |nlb\-11zm8k4m6wa9s49\*\*\*\*.nlb.cn\-beijing.volces.com |
   


<span id="qZif5p5J"></span>
## Prerequisites

A CLB instance has been deployed and is accessible via a DNS domain name.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This topic uses BytePlus DNS as an example.</div>


<span id="IWNEzVlt"></span>
## Precautions


* Note that CLB and NLB have different billing methods, so the migration will involve a change in billing. See the billing rules for details:

   * NLB: see [Pay-by-CU](https://docs.byteplus.com/en/docs/clb/NLB-Pay-by-LCU).

   * CLB: see [Billing overview](https://docs.byteplus.com/en/docs/clb/Billing-01).

* The backend servers remain unchanged; only the CLB is replaced with an NLB instance.

* After migration, it is recommended to release the CLB instance to avoid continued billing.


<span id="IWNEzVlt"></span>
## Configuration procedures

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following steps only describe parameters required for this configuration. Keep other parameters at their default values. For more information about parameters, see <a href="https://docs.byteplus.com/en/docs/clb/Creating-an-NLB-instance">User Guide</a>.</div>


<span id="GefWmRy2"></span>
### Step 1: Configure NLB instance


1. **Create an NLB instance**

   1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">During initial login, follow the on\-screen instruction to complete cross\-service role authorization.      </div>
      

   2. Click **Create NLB**, and configure related parameters according to the table below.

      
      |Parameter |Notes |Example value |
      |---|---|---|
      |**Basic Information** |||
      |Region |Keep consistent with the region of the CLB instance. |China (Beijing) |
      |Name |Type the name of NLB instance. |NLB\-X |
      |**Network configuration** |||
      |IP Version |Select the private IP address type of the NLB instance. |IPv4 |
      |Network Type (IPv4) |Select the network type for the NLB instance's IPv4 address. |Public |
      |VPC |Keep consistent with the CLB instance's VPC. |VPC\-X |
      |Availability Zone and Subnet |Select the supported Availability Zone for the NLB instance, and specify the subnet, IP address, and Elastic IP (EIP) for each availability zone.<br><br><br>* Subnet: Provides a private network deployment environment for the NLB instance. The system automatically creates a network interface within the subnet and attaches it to the NLB.<br><br>* IPv4 address: Select the allocation method for the IPv4 address of the NLB instance. After the instance is created, all assigned IPv4 addresses cannot be modified.<br><br>* EIP: Provides internet capabilities for the NLB instance. Configure this parameter only when the network type (IPv4) is **Internet**. |* AZ\-A<br><br>   * Subnet\-A \| 192.168.1.0/24<br><br>   * Auto\-assign IP<br><br>   * Newly purchased EIP<br><br>* AZ\-B<br><br>   * Subnet\-B \| 192.168.2.0/24<br><br>   * Auto\-assign IP<br><br>   * Newly purchased EIP |
      |SecurityGroup |Select at least one security group for the NLB instance. |default |
      

   3. In the **Configuration Details** window on the right side of the page, check and confirm the Legal as guided by the console.

   4. Click **Submit order** to complete the instance creation.

   5. Click **Go to console** to view and record the domain name of the newly created NLB instance.

2. **Create server group and add backend server**

   1. In the left navigation pane, select **Server Group**.

   2. Click **Create server group**, and configure related parameters by referring to the table below.

      
      |Parameter |Notes |Example value |
      |---|---|---|
      |Name |Enter server group name |rsp01 |
      |Server group type |Keep consistent with the type of the CLB instance's backend server group. |Server type |
      |IP Version |Keep consistent with the protocol type of the CLB instance's backend servers' private IP addresses. |IPv4 |
      |VPC |Select a server group in the same Virtual Private Cloud (VPC) as the NLB instance. |VPC\-X |
      |Protocol |The protocol used by the NLB instance to forward requests to the backend server. |TCP |
      |Load balancing algorithm |Select the rules that the server group follows to forward requests. Keep consistent with the CLB instance. |Weighted Round Robin (WRR) |
      |Allow Backend Security Group Traffic |Enable the **Allow backend security group** feature. After enabling, the security group of backend servers in the Server Group no longer validates NLB traffic and is allowed by default. |**On** |
      

   3. Enable **Health check**, keep the remaining parameters at their default values.

   4. Click **Create** to complete the creation of the server group.

   5. Click  **··· \> Add Server** on the right side of the target server group.

   6. Click **Add Server** and select the target Elastic Compute Service (ECS) instance.

   7. Click **Next** to configure ports and weights for the added backend servers.

         
         |Parameter |Notes |Example value |
         |---|---|---|
         |Port |Keep consistent with the service ports provided by the CLB instance's backend servers. |80 |
         |Weight |Keep consistent with the weights of the CLB instance's backend servers. |100 |
         

   7. Click **Create** to complete the action.

3. **Add listener**

   1. In the left\-side navigation pane, select **Instances**.

   2. Click **Configure Listener** on the right side of the target NLB instance.

   3. Click **Add Listener** and refer to the table below to configure relevant parameters.

      
      |Parameter |Notes |Example value |
      |---|---|---|
      |Listener name |Enter the listener name. If left blank, it defaults to **Protocol\-port**, such as TCP\-80. |listener01 |
      |Listener protocol |Keep consistent with the protocol of the CLB instance's listener. |TCP |
      |Listener port |Keep consistent with the CLB instance's listener port. |80 |
      |Timeout |Set the timeout period. If no data is transferred over the connection within the timeout period, it will be automatically disabled. The value ranges from 10 to 900 seconds, with a default of 900 seconds. |900 seconds |
      

   4. Click **Next**, then select the server group created above.

   5. Click **Next** to confirm the configuration information.

   6. Click **Add** to complete the action.

4. **Configure security group and network ACL**

   * **Configure security group**

      For actions, see [Adding a security group rule](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules). Example configuration in this topic:

      * Security group associated with the NLB instance

         
         |Rule direction |Priority |Policy |Protocol  |Port range |Source/destination address |Description |
         |---|---|---|---|---|---|---|
         |Inbound |1 |permit |TCP |80 |Source address: 0.0.0.0/0 |Allow client access traffic to the NLB (in this case, TCP traffic on port 80) |
         ||1 |permit |ICMP |ALL |100.64.0.0/10 |Allow traffic to detect the availability of the NLB instance private IPv4 address |
         ||1 |deny |TCP |80 |Access to the NLB's IP address is not allowed |Deny specified IP addresses from accessing the NLB |
         |Outbound |100 |permit |ALL |ALL |Destination: 0.0.0.0/0 |Allow\-all fallback policy |
         

      * Security group associated with the backend servers.

         
         |Rule direction |Priority |Policy |Protocol  |Port range |Source address |Description |
         |---|---|---|---|---|---|---|
         |Inbound |1 |permit |TCP |80 |192.168.1.0/24、192.168.2.0/24 |Allow both request forwarding traffic and health check traffic from NLB to backend servers |
         

   * **Configure Network ACL**

      For actions, see [Adding a Network ACL rule](https://docs.byteplus.com/en/docs/vpc/Managing-network-ACL-rules). If no subnet associated with the NLB has a Network ACL attached, the NLB example can be ignored. If no subnet associated with the backend servers has a Network ACL attached, the backend server example can be ignored.

      * NLB instance

         
         |Rule direction |Priority |Policy |Protocol |Source address/Destination address |Destination port |Description |
         |---|---|---|---|---|---|---|
         |Inbound |1 |permit |TCP |0.0.0.0/0 |80 |Allow inbound client traffic to the NLB |
         ||2<br><br> |<div style="text-align: center"><br>permit</div><br><br><br><div style="text-align: center"><br></div><br> |TCP |192.168.1.11、<br><br>192.168.2.22 |80 |Allow health check response traffic from backend servers to the NLB, allow client\-originated response traffic from backend servers to the NLB |
         ||3 |permit |ICMP |100.64.0.0/10 |ALL |Allow traffic for system probes to detect the availability of the NLB private IPv4 address |
         |Outbound |1 |permit |ALL |0.0.0.0/0 |ALL |Allow all IPv4 traffic |
         

      * Backend server

         
         |Rule direction |Priority |Policy |Agreement |Source/destination address |Destination port |Description |
         |---|---|---|---|---|---|---|
         |Inbound<br><br> |1 |permit<br><br> |TCP |192.168.1.0/24、192.168.2.0/24 |80 |Allow both request forwarding traffic and health check traffic from NLB to backend servers |
         |Outbound |1 |permit |ALL |0.0.0.0/0 |ALL |Release all traffic |
         

      For more details, see [Configuring NLB security groups and Network ACLs](https://docs.byteplus.com/en/docs/clb/Configuring-security-group-and-Network-ACL-for-NLB) and [Configuring backend server security groups and Network ACLs](https://docs.byteplus.com/en/docs/clb/NLB-Configuring-backend-server-security-group-and-Network-ACL).


<span id="ZKveYiRz"></span>
### Step 2: Modify DNS configuration for CLB

If the business domain is `www.example.com`, add a temporary domain `abc.example.com` and configure its DNS resolution to point to the EIP address of the CLB instance.


1. **Add a temporary domain record**

   1. Log in to the [DNS console](https://console.byteplus.com/TrafficRoute/dns/public-zone).

   2. Click the target domain name. This topic uses example.com.

   3. Click **Add record**.

   4. Refer to the table below to configure the relevant parameters.

      
      |Parameter |Description |
      |---|---|
      |Domain name |Set it to the host record (domain prefix) of your own domain name. For example: `abc.example.com`. |
      |Record type |Set to **A**. |
      |Record value |Set to the EIP of the CLB instance (in this case, `12.XX.XX.78`). |
      |<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For parameters not mentioned above, please keep the default values.</div><br> ||
      

   5. Click **Buy now** to complete the action.

2. **Modify the original DNS record**

   1. Log in to the [DNS console](https://console.byteplus.com/TrafficRoute/dns/public-zone).

   2. Click the target domain name. This topic uses example.com.

   3. Click the business domain name. This topic uses www.example.com.

   4. Click **Edit** in the upper right corner to modify the following:

      * Change the **Record type** from **A** to **CNAME.** 

      * Change the **Record value** from `12.XX.XX.78` to `abc.example.com`.

      * Change the weight to 100.

   5. Click **Buy now** to complete the action.


<span id="U9OtaIDN"></span>
### Step 3: Migrate traffic from CLB to NLB


1. **Add the NLB record value**

   1. Log in to the [DNS console](https://console.byteplus.com/TrafficRoute/dns/public-zone).

   2. Click the target domain name. This topic uses example.com.

   3. Click the business domain name. This topic uses www.example.com.

   4. Click **Add record value** and add the following content:

      * Enter the NLB instance domain. For example, `nlb-11zm8k4m6wa9s49****.nlb.cn-beijing.volces.com`.

      * Set the weight to **1.** 

      * Enable the record.

   5. Click **Add** to complete the action.

2. **Adjust record weight**

   Monitor the service operation and, without affecting the service, **gradually increase the weight of the NLB record value while decreasing the weight of the CLB record value.** 

   1. Click the business domain name. This topic uses www.example.com.

   2. Click **Edit** to the right of the target record value to adjust the weight.

   3. Click **Buy now** to complete the action.

3. **Disable the CLB record value**

   When the CLB's weight is reduced to 1 and you confirm it does not affect the service, disable the CLB record. Complete the migration from CLB to NLB.

   1. Click the business domain name. This topic uses www.example.com.

   2. Turn off the Enable switch on the right side of the CLB record value.

   3. After confirming the information is correct, click **Remove** to complete the action.



&nbsp;
