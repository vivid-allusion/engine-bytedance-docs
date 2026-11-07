---
title: "Traffic access control between VPCs (automatic traffic diversion configuration)"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Access_control_for_traffic_between_VPCs"
---

This article introduces automatic traffic diversion configuration through cloud firewall, helping you complete traffic access control between VPCs.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This article contains important reminder information that you need to pay attention to. Ignoring this information may impact your business, so please read it carefully.</div>



---



<span id="2d71fffa"></span>
# **Scenario introduction**


* Complete traffic diversion between VPC1, VPC2, and VPC3 to the cloud firewall.

* Configure access control policy: VPC1 subnet can access VPC2.

* Configure access control policy: VPC2 subnet can access VPC3.

* Configure access control policy to block all other accesses.

   
   |**Resource type** |**Belonging region** |**VPC/dedicated line subnet** |**Subnet segment** |
   |---|---|---|---|
   |vpc\-01 |South China 1 (Guangzhou) |10.1.0.0/16 |sunnet\-01：10.1.0.0/24 |
   |vpc\-02 ||10.2.0.0/16 |subnet\-02：10.2.0.0/24 |
   |vpc\-03 ||10.3.0.0/16 |subnet\-03：10.3.0.0/24 |
   |VPN\-04 (if there are VPN instances, need to configure step three) ||10.4.0.0/16 |N/A |
   |tr transit router |South China 1 |N/A |N/A |
   


<span id="0dc6691c"></span>
# **Requirements**


* The required VPC and subnet creation has been completed. For detailed steps, please refer to [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* The creation of cloud server instances in each VPC has been completed. For detailed steps, please refer to [Purchase Cloud Server Instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) to continue.

* The creation of transit router instances and network instance connections has been completed. For detailed steps, please refer to [Create Transit Router Instances](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-01).

* Cloud firewall enterprise edition and above sales specifications have been purchased.


<span id="0f33a6f2"></span>
# **Usage Restrictions**


* When there is a static route within the 100.64.0.0/10 range in the routing table of the transit router, traffic diversion configuration is not supported.

* Traffic diversion configuration is not supported for VPC network instances with routing conflicts, including routing conflicts between VPC network instances and routing conflicts with firewall VPC; otherwise, the network will be interrupted after configuring automatic diversion scenarios. It is recommended to reasonably plan the firewall VPC subnet and VPC network instance subnet according to business needs.

* The subnet mask for the VPC network instance's subnet segment must be less than or equal to 31 bits.


<span id="a1f4f48a"></span>
# Step 1: Create a VPC boundary firewall


1. Log in to the [Cloud Firewall Console](https://console.byteplus.com/firewall/overview). In the left navigation bar, click on **Firewall Switch**.

2. On the **firewall switch** page, click **VPC boundary firewall**.

3. Locate the forwarding router under the cloud enterprise network instance of the target VPC boundary firewall, and click the **Actions** column's **Create cloud firewall**.

4. Select **automatic drainage** mode, and click submit and next. The automatic drainage mode VPC boundary firewall will automatically configure routing on the transit router based on the drainage scenario.

5. Create the VPC boundary firewall, and configure the parameters as shown below. The cloud firewall is expected to take about 10 minutes during the creation process.



|**Configuration item** |**Configuration Description** |**Configuration parameters** |
|---|---|---|
|Firewall name |Define the name of the VPC boundary firewall. This name is used to identify the VPC boundary firewall instance. It is recommended that you enter a meaningful name based on the actual business situation. |Dedicated line and VPC boundary protection |
|Firewall VPC network segment |Allocate segments for the automatically created cloud firewall's VPC, and divide 3 subnet segments from the allocated VPC segment. The mask for the 3 subnet segments of the cloud firewall must be less than or equal to 28 bits and must not conflict with the network planning segment. |192.168.0.0/24 |
|VPC subnet 1 network segment ||192.168.0.16/28 |
|VPC subnet 2 segment ||192.168.0.32/28 |
|VPC subnet 3 network segment ||192.168.0.48/28 |


<span id="8a6c32ff"></span>
# Step 2: Create a drainage scenario


1. After the VPC firewall creation is complete, click **Submit and Next**.

   * Refer to the table below to configure the drainage scenario.

   * You can also choose not to configure the drainage scenario temporarily and set it up later based on business needs. On the **VPC boundary firewall** tab, locate the target transit router instance, click **Actions** in the column, then **Details**, and click **Create drainage scenario** to configure.


<div style="text-align: center">
</div>



|**Configuration items** |**Configuration description** |**Configuration Parameter** |
|---|---|---|
|**Traffic scenario name** |Definition of the name for the traffic scenario. This name is used to mark the traffic scenario type, and it is recommended that you input a meaningful name based on the actual situation of the business. |Dedicated line and VPC drainage |
|**Drainage scenario selection** |Select the traffic diversion scenario type based on the protection requirements for network instances (VPC, dedicated lines, VPN). If the example type only needs to protect traffic between 3 VPCs connected to the cloud via a dedicated line, point\-to\-multipoint can be selected. If protection is needed for both the traffic between 3 VPCs connected to the cloud via a dedicated line and the traffic between the 3 VPCs, multipoint interconnection can be selected.<br><br><br>* **Point\-to\-point**: Traffic between two network instances is controlled by the cloud firewall. Suitable for simple network topology environments.<br><br>* **Point\-to\-multipoint**: Traffic between one network instance and multiple network instances is controlled by the cloud firewall. Suitable for star network topology environments.<br><br>* **Multi\-point interconnection**: Traffic between multiple network instances is controlled by cloud firewall. Applicable to **Full Mesh** mesh network topology environment. |Multi\-point interconnection |
|**Instance selection** |Configure the network instance that needs to be drained (multi\-point interconnection) |VPC\-01<br><br>VPC\-02<br><br>VPC\-03 |



2. Once the drainage scenario is created, the cloud firewall will automatically create drainage route table information on the TR transit router for you, thus achieving traffic protection for the network instances connected to the transit router.

   * The TR network instance connection will add a cloud firewall VPC, with the connection name **CFW_system_please_do_not_edit**

   * The cloud firewall will create four route tables named **CFW_ststem_Don't_edit**, associated with forwarding for VPC\-01, VPC\-02, VPC\-03, and the cloud firewall. This explains the routing principle using the traffic from VPC\-01 to VPC\-02 as an example.



|**Routing table** |**Associated forwarding** |**Routing entry description** |
|---|---|---|
|Route table 1 |VPC\-01 |**Taking the routing table 1 associated with forwarding VPC\-1 as an example:** <br><br><br>1. The system will automatically learn the routes pointing to VPC\-02 and VPC\-03.<br><br>2. The cloud firewall will split each self\-learning route pointing to VPC\-02 and VPC\-03 into 2 static routes with **higher priority pointing to the cloud firewall** based on the automatically learned routes. If the **destination subnet is** **`10.2.0.0/24`** **and the next hop is VPC\-02**, the self\-learning route will be split into the following two static routes:<br><br>   * `10.2.0.0/25` next hop is **CFW_system_do not edit**<br><br>   * `10.2.0.128/25` next hop is **CFW_system_do not edit**<br><br>3. Thus, the traffic from VPC\-01 to VPC\-02 and VPC\-03 will all point to **the cloud firewall** for protection. |
|Firewall routing table |CFW_system_do not edit (Cloud Firewall VPC) |**Description of the routing table associated with the forwarding cloud firewall VPC:** <br><br><br>1. Will automatically learn routes pointing to VPC01, VPC\-02, and VPC\-03.<br><br>2. Traffic from VPC\-01 points to the cloud firewall, which, after being protected and cleaned by the cloud firewall, is forwarded to VPC2 based on the destination subnet `10.2.0.0/24` with the next hop being **VPC\-02**. |


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>



* <div data-tips="true" data-tips-type="danger"><strong>Please do not modify the system route table</strong>: After creating the drainage scenario, the cloud firewall will automatically create a fallback route for you in the system route table. When the drainage scenario on the VPC cloud firewall is <strong>closed, deleted, when the VPC cloud firewall is upgraded, fails, deleted, or when the VPC firewall instance expires and unsubscribes</strong>, the cloud firewall will enable the <strong>Bypass</strong> mechanism, switching the associated forwarding network instances of VPC\-01, VPC\-02, VPC\-03 from the firewall routing to the <strong>system route table</strong>, ensuring business stability through fallback routing. Please do not edit the <strong>system route table</strong> to avoid causing risks of business interruptions.</div>


* <div data-tips="true" data-tips-type="danger"><strong>Please do not edit the route table created by the cloud firewall</strong>: To avoid affecting your business, please do not edit the route table created by the cloud firewall named <strong>CFW_system_请勿编辑</strong> to avoid the risk of route forwarding failure.</div>


* <div data-tips="true" data-tips-type="danger"><strong>VPN network instance route configuration</strong>: If a VPN instance was originally connected in TR, you need to manually configure the VPN static routing policy when creating a new drainage scenario or reopening a previously closed drainage scenario to ensure VPN network connectivity; for policy configuration, please see <strong>Step Three: Manually Configure VPN Network Instance Routing (If the TR network instance is not connected to VPN, this step can be skipped</strong>).</div>



<span id="806842bf"></span>
# Step Three: Manually configure VPN network instance routing (If the TR network instance is not connected to VPN, this step can be skipped). 

If your TR router is still connected to the VPN network instance, after completing Steps One and Two, the VPN\-04 instance will not be able to connect to the networks of VPC\-01, VPC\-02, and VPC\-03 and needs to manually configure VPC routing. You need to add routes pointing to the VPN network instance in the associated forwarding route tables of VPC\-01, VPC\-02, and VPC\-03, using the VPC\-01 route as an example.


|**Routing table** |**Associated forwarding** |**Routing entry description** |
|---|---|---|
|Routing table 1 |VPC\-01 |1. Add the destination subnet as 10.4.0.0/16, with the next hop as a static route for VPN\-04. |


<span id="d22e4a43"></span>
# Step 4: Access Control Policy Configuration. 

When controlling traffic between VPCs, you need to either reject suspicious or malicious traffic first, or allow trusted traffic first and then reject access from other addresses.


1. Log in to [Cloud Firewall Console](https://console.byteplus.com/firewall/overview).

2. In the left navigation bar, select **Access Control**.\>**VPC Boundary**.

3. On the **VPC Boundary** page, select the **associated VPC firewall** and click **Add Policy**.

4. The cloud firewall defaults to allow traffic without policies. Therefore, it is necessary to configure three access control policies: one allowing traffic from the **VPC\-01** segment to access the **VPC\-02** high\-priority allow policy, and one blocking all traffic with a low\-priority blocking policy.

5. Add a policy allowing the VPC\-01 segment to access the VPC\-02 segment.


<div style="text-align: center">
</div>



|**Configuration item** |**Configuration description** |**Configuration parameter** |
|---|---|---|
|**Rule priority** |Select the priority of this policy, here we choose the highest priority. After configuration, you can also click **move** in the access control policy list to customize the priority adjustment.<br><br><br>* **Highest priority**: refers to the highest priority of the access control policy taking effect, taking effect first.<br><br>* **Lowest priority**: refers to the lowest priority of the access control policy taking effect, taking effect last. |Highest priority |
|**Access source type** |You need to select the access source type and enter the access source address according to the access source type. Here select IP type and enter `10.1.0.0/24`.<br><br><br>* When selecting **IP** type, you need to enter an IP address or IP address segment. For example, `180.184.1.1` or `180.184.0.0/16`, `0.0.0.0/0` indicates all.<br><br>* When selecting the **address book** type, you need to create the IP address book in advance. |IP |
|**Access source** ||10.1.0.0/24 |
|**Access purpose type** |You need to select the access destination type and enter the access destination address based on the access destination type. Here select IP type and enter `10.2.0.0/24.`<br><br><br>* When selecting **IP** type, you need to enter the IP address or IP address range. Such as `180.184.1.1` or `180.184.0.0/16`, `0.0.0.0/0` represents all.<br><br>* When selecting **Address Book** type, you need to create the IP address book in advance.<br><br>* When selecting **Domain Name** type, you need to enter the destination domain name address.<br><br>   * Input domain names support entering a single domain name `example.com`, wildcard domain name `*.example.com`, multi\-level domain name `example1.example2.com`<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Please do not enter http(s) and other protocol content.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The domain access empty policy principle is to obtain domain data for matching control based on the Host information in the HTTP protocol data, and the Server Name information in the Client Hello of the HTTPS protocol data packet. If your business traffic data packet does not contain these two fields, the domain policy cannot be effective.   </div><br>    |IP |
|**Access destination** ||10.2.0.0/24 |
|**Protocol type** |The transport layer protocol type supports settings for: **TCP**, **UDP**, **ICMP**, **ANY**. If unsure of the specific protocol, you can choose **ANY.**  |ANY |
|**Action** |Set the traffic flow that matches successfully in this policy to be allowed.<br><br><br>* **Allow**: Allow this traffic, record the allow log in the access control log, and log the traffic in the traffic session.<br><br>* **Block**: Intercept this traffic, and block logs will be recorded in the access control log.<br><br>* **Observe**: Allow this traffic. The observation log will be recorded in the access control log. |Release |
|**Description** |Input the current policy content and usage scenarios. Convenient for you to identify and apply the address book |VPC1 accesses VPC2 |
|**Policy switch** |Set the policy switch. If you did not enable the policy when creating it, you can enable the policy in the policy list. |Keep it enabled |



6. **Add a policy allowing VPC\-02 segment to access VPC\-03 segment**, access control policy configuration parameters are as follows.

   
   |**Configuration item** |**Configuration parameters** |
   |---|---|
   |**Rule priority** |Highest priority |
   |**Access source type** |IP |
   |**Access source** |10.2.0.0/24 |
   |**Access purpose type** |IP |
   |**Visit purpose** |10.3.0.0/24 |
   |**Protocol type** |ANY |
   |**Destination port type** |Port |
   |**Destination port** |0/65535 |
   |**Action** |Release |
   |**Description** |VPC1 accesses VPC3 |
   |**Policy switch** |Keep it enabled |
   

7. **Add Blocking Policy**: Configure a low\-priority blocking policy for all Direct Connect\-04 traffic accessing this host. **Access control** policy configuration <参数\>parameters are as follows:

   
   |**Configuration item** |**Configuration parameter** |
   |---|---|
   |**Rule priority** |Lowest priority |
   |**Access source type** |IP |
   |**Access source** |0.0.0.0/0 |
   |**Access destination type** |IP |
   |**Access purpose** |0.0.0.0/0 |
   |**Protocol type** |ANY |
   |**Destination port type** |Port |
   |**Destination port** |0/65535 |
   |**Action** |Block |
   |**Description** |Block other access policies |
   |**Policy switch** |Keep it enabled |
