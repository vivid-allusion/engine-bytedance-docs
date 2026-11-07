---
title: "Traffic access control between VPC and dedicated line (automatic traffic redirection configuration)"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Access_control_for_traffic_between_a_VPC_and_an_instance"
---

This article introduces the automatic traffic redirection configuration through the cloud firewall, helping you complete traffic access control between VPC and dedicated line.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This article contains important tips that you need to pay attention to. Ignoring this information may affect your business, so please read it carefully.</div>



---



<span id="e7e07386"></span>
# **Scenario introduction**


* Complete the traffic redirection from VPC1 to the cloud firewall via the dedicated line.

* Configure access control policy: VPC\-01 `10.1.0.0/26` segment can access dedicated line\-02.

* Configure access control policy to block all other access.

   
   |**Resource type** |**Belonging region** |**VPC/Dedicated line subnet** |**Subnet segment** |
   |---|---|---|---|
   |vpc\-01 |South China 1 (Guangzhou) |10.1.0.0/16 |sunnet\-01：10.1.0.0/24 |
   |Dedicated line\-02 ||N/A |sunnet\-01：192.168.161.0/24 |
   |VPN\-03 (if there are VPN instances, refer to configuration step three) ||10.3.0.0/16 |N/A |
   |tr transit router |South China 1 |N/A |N/A |
   


<span id="ab94bb33"></span>
# **Requirements**


* The required VPC and subnet creation has been completed. For detailed steps, please refer to [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* The creation of cloud server instances in each VPC has been completed. For detailed steps, please refer to [Purchase Cloud Server Instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) to continue.

* The creation of transit router instances and network instance connections has been completed. For detailed steps, please refer to [Create Transit Router Instances](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-01).

* Cloud firewall enterprise edition and above sales specifications have been purchased.


<span id="2330e55e"></span>
# **Usage Restrictions**


* When there are static routes within `100.64.0.0/10` in the transit router's routing table, the configuration of traffic diversion is not supported.

* The traffic diversion configuration for VPC network instances with routing conflicts is not supported, including routing conflicts between VPC network instances and routing conflicts between VPC network instances and firewall VPCs; otherwise, after configuring automatic traffic diversion scenarios, the network will be interrupted. It is recommended to plan the firewall VPC segment and the VPC network instance segment reasonably according to business needs.

* The subnet mask of the VPC network instance must be less than or equal to 31 bits.


<span id="28cd19e5"></span>
# Step 1: Create VPC Boundary Firewall


1. Log in to [Cloud Firewall Console](https://console.byteplus.com/firewall/overview). In the left navigation bar, click **Firewall Switch**.

2. On the **Firewall Switch** page, click **VPC Boundary Firewall**.

3. Locate the forwarding router under the cloud enterprise network instance at the target VPC boundary firewall, and click on the **Action** column to **Create Cloud Firewall**.

4. Select **Automatic Drainage** mode, and click Submit and Next. In automatic drainage mode, the VPC boundary firewall will automatically configure routes on the transit router based on the drainage scenario.

5. Create the VPC boundary firewall with the following configuration parameters. The cloud firewall is expected to take about 10 minutes to set up.


<div style="text-align: center">
</div>



|**Configuration item** |**Configuration Description** |**Configuration parameter** |
|---|---|---|
|Firewall name |Define the name of the VPC boundary firewall. This name is used to identify the VPC boundary firewall instance. It is recommended to enter a meaningful name based on the actual situation of the business. |Dedicated line and VPC boundary protection |
|Firewall VPC subnet |Allocate a network segment for the automatically created cloud firewall's VPC, and divide 3 subnets from the allocated VPC segment. 。 The subnet mask of the three child networks of the cloud firewall must be less than or equal to 28 bits and cannot conflict with the planned network segments. |192.168.0.0/24 |
|VPC subnet 1 network segment ||192.168.0.16/28 |
|VPC subnet 2 segment ||192.168.0.32/28 |
|VPC subnet 3 network segment ||192.168.0.48/28 |


<span id="624d41a4"></span>
# Step Two: Create Drainage Scenario


1. After the VPC firewall is created, click **Submit Next**.

   * Configure the drainage scenario as described in the table below.

   * You can also choose not to configure the drainage scenario temporarily and configure it later as needed. In the **VPC Boundary Firewall** tab, locate the target transit router instance, click on **Action** column under **Details**, and click **Create Drainage Scenario** to configure.



|**Configuration item** |**Configuration description** |**Configuration Parameter** |
|---|---|---|
|**Traffic diversion scenario name** |Define the name of the traffic diversion scenario. This name is used to label the type of traffic diversion scenario, and it is recommended that you input a meaningful name based on the actual business situation. |Dedicated line and VPC traffic redirection |
|**Traffic Redirection Scenario Selection** |Select the traffic diversion scenario type based on the protection requirements of network instances (VPC, dedicated line, VPN). If the example type only needs to protect the traffic from the dedicated line to three VPCs in the cloud, then point\-to\-multipoint can be selected. If protection is needed for both the traffic from the dedicated line to the cloud's three VPCs and the traffic between the three VPCs, then multipoint interconnection can be selected.<br><br><br>* **Point\-to\-point**: The traffic between two network instances is controlled by the cloud firewall. Suitable for simple network topology environments.<br><br>* **Point\-to\-multipoint**: The traffic between one network instance and multiple network instances is controlled by the cloud firewall. Suitable for star network topology environments;<br><br>* **Multipoint interconnection**: The traffic between multiple network instances is controlled by the cloud firewall. Suitable for **Full Mesh** network topology environments. |Multi\-point interconnection |
|**Instance selection** |Configuration needs to drain the network instances (multi\-point interconnection) |VPC\-01<br\>Dedicated Line\-02 |



2. After the drainage scenario is created, the cloud firewall will automatically create the drainage routing table information on the TR transit router for you, enabling traffic protection between network instances connected to the forwarding router.

   * A VPC for the cloud firewall will be added to the TR network instance connection, with the connection name as **CFW_system_please_do_not_edit**.

   * The cloud firewall will create 3 routing tables named **CFW_system_please_do_not_edit**, which will be associated with VPC\-01, Dedicated Line\-02, and the cloud firewall respectively. Taking the traffic direction from **VPC\-01** to **Dedicated Line\-02** as an example to illustrate routing principles.



|**Routing table** |**Associated forwarding** |**Route entry description** |
|---|---|---|
|Routing table 1 |VPC\-01 |**Taking the routing table 1 associated with VPC\-1 as an example:** <br><br><br>1. The system will automatically learn the route pointing to the dedicated line \-02.<br><br>2. The cloud firewall will split each self\-learning route pointing to the dedicated line \-02 into 2 static routes that execute **higher priority** pointing to the cloud firewall. If **the destination subnet is** **`192.168.161.0/24`**, **the self\-learning route with a next hop of VPC\-02 will be split into the following two static routes:** <br><br>   * **`192.168.161.0/25`** next hop is **CFW_system_Do not edit**<br><br>   * **`192.168.161.128/25`** ** next hop is CFW_system_Do not edit**<br><br>3. Thus, the traffic pointing from VPC\-01 to dedicated line\-02 will **point to the cloud firewall** for the purpose of protection by the cloud firewall. |
|Firewall routing table |CFW_system_Do not edit (Cloud Firewall VPC) |**Associated forwarding cloud firewall VPC routing table description:** <br><br><br>1. Will automatically learn routes pointing to VPC01 and dedicated line\-02.<br><br>2. Traffic from VPC\-01 directed to the cloud firewall will be forwarded to dedicated line\-02 after passing through the protection cleaning by the cloud firewall, based on the destination subnet `192.168.161.0/24` and the next hop being **dedicated line\-02**. |


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>



* <div data-tips="true" data-tips-type="danger"><strong>Please do not modify the system routing table: after creating a diversion scenario, the cloud firewall will automatically create a fallback route for you in the system routing table.</strong> <strong>When the diversion scenario on the VPC cloud firewall is turned off, deleted, the VPC cloud firewall is upgraded, fails, is deleted, or when the VPC firewall instance expires and unsubscribes</strong>, the cloud firewall will enable the <strong>Bypass</strong> mechanism, switching the associated forwarding network instances of VPC\-01 and Dedicated Line\-02 from the firewall routing to the <strong>system routing table</strong>, ensuring business stability through the fallback route. Please do not edit the <strong>system routing table</strong> to avoid causing business interruption risks.</div>


* <div data-tips="true" data-tips-type="danger"><strong>Please do not edit the routing table created by the cloud firewall: to avoid impacting your business, do not edit the routing table named CFW_system_please_do_not_edit created by the cloud firewall to avoid the risk of routing forwarding failure.</strong></div>


* <div data-tips="true" data-tips-type="danger"><strong>VPN network instance routing configuration</strong>: If the TR originally connected to a VPN instance, you need to manually configure the VPN static routing strategy when creating a new diversion scenario or reopening a previously closed diversion scenario to ensure the connectivity of the VPN network. For strategy configuration, see <a href="https://docs.byteplus.com/en/docs/6516/1172120#d8b695fc">Step 3: Manually configure VPN network instance routing (this step can be skipped if the TR network instance is not connected to VPN)</a>.</div>



<span id="d8b695fc"></span>
# Step 3: Manually configure VPN network instance routing (this step can be skipped if the TR network instance is not connected to VPN)

If your TR transit router is still connected to a VPN network instance, after completing steps one and two, the VPN\-03 instance will not be able to communicate with VPC\-01 and Dedicated Line\-02 network instances. You will need to manually configure the VPC routing. \nYou need to separately add network instances pointing to VPN in the two routing tables associated with forwarding VPC\-01 and Dedicated Line\-02, taking the VPC\-01 route as an example.


|**Routing table** |**Associated forwarding** |**Route Entry Description** |
|---|---|---|
|Route Table 1 |VPC\-01 |1. Add the destination subnet as `10.3.0.0/16`, with the next hop being the static route of VPN\-03. |


<span id="e37e3bdd"></span>
# Step 4: Access control policy configuration

When controlling traffic between VPCs, you need to first reject suspicious or malicious traffic, or allow trusted traffic first and then reject access from other addresses. Example configuration of VPC boundary access control policy, the policy configuration parameters are as follows.


1. Log in to [Cloud Firewall Console](https://console.byteplus.com/firewall/overview).

2. In the left navigation bar, select **Access Control**.\>**VPC Boundary.**  On the **VPC Boundary** page, select **The associated VPC firewall** and click **Add Policy**.

3. The cloud firewall defaults to allow access without any policies. Therefore, it is necessary to configure 2 access control policies: one to allow **VPC\-01**. The **10.1.0.0/26** subnet traffic can access the dedicated line\-02 primary allow policy, and one to block all traffic in the opposite direction with a low\-priority blocking policy.

4. **Add allow policy**.



|**Configuration item** |**Configuration Description** |**Configuration parameter** |
|---|---|---|
|**Rule priority** |Select the priority of this policy; here we choose the highest priority. After the configuration is complete, you can also click **Move** in the access control policy list to customize the adjustment of the policy priority.<br><br><br>* **Highest priority**: Refers to the highest priority for the access control policy to take effect, taking effect first.<br><br>* **Lowest priority**: Refers to the lowest priority for the access control policy to take effect, taking effect last. |Highest priority |
|**Access source type** |You need to select the access source type and enter the access source address according to the access source type. Select the IP type here and enter `10.1.0.0/26`.<br><br><br>* When selecting **IP** type, you need to enter an IP address or IP address range. Such as `180.184.1.1` or `180.184.0.0/16`, `0.0.0.0/0` represents all.<br><br>* When selecting **address book** type, you need to create an IP address book in advance.<br><br>* When selecting **region** type, you need to select the region where the source address is located. You can choose domestic regions or international regions. |IP |
|**Access source** ||10.1.0.0/26 |
|**Access purpose type** |You need to select the access <a i=1\>data type</a\> and enter the access address based on the access <a i=1\>data type</a\>. Select the IP `data type` here and enter <a i=1\>192.168.161.0/24</a\>.<br><br><br>* When selecting **IP** <a i=1\>data type</a\>, you need to enter the IP address or IP address range. For example, `180.184.1.1` or `180.184.0.0/16`, `0.0.0.0/0` represents all.<br><br>* When selecting **address book** <a i=1\>data type</a\>, you need to create an IP address book in advance. |IP |
|**Access destination** ||192.168.161.0/24 |
|**Protocol type** |Transport layer protocol type, supports setting to: **TCP**, **UDP**, **ICMP**, **ANY**. If the specific protocol is uncertain, you can choose **ANY.**  |ANY |
|**Action** |Set the release conditions for traffic matching this policy.<br><br><br>* **Release**: Release the traffic, record the release log in the access control log, and log the traffic in the traffic session.<br><br>* **Block**: Intercept the traffic, and a block log will be recorded in the access control log.<br><br>* **Observe**: Release the traffic. A log of observation will be recorded in the access control log. |Release |
|**Description** |Enter the current policy content and usage scenario. This helps you identify and apply the address book. |VPC1 access dedicated line\-02 |
|**Policy switch** |Set the Policy switch. If you did not enable the policy when creating it, you can turn on the policy in the policy list. |Keep it enabled |



5. \*\*Add blocking policy:\*\* Configure a low\-priority traffic blocking policy. **Blocking** access control policy configuration parameters are as follows:



|**Configuration Item** |**Configuration Parameter** |
|---|---|
|**Rule priority** |Minimum Priority |
|**Access source type** |IP |
|**Access Source** |0.0.0.0/0 |
|**Access purpose type** |IP |
|**Access purpose** |0.0.0.0/0 |
|**Protocol type** |ANY |
|**Destination port type** |Port |
|**Destination port** |0/65535 |
|**Action** |Block |
|**Description** |Block other access policies |
|**Policy switch** |Keep it enabled |
