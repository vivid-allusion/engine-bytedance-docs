---
title: "Traffic access control between VPC and VPN (manual traffic diversion configuration)"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Access_control_for_traffic_between_a_VPC_and_a_VPN"
---

This article introduces automatic traffic diversion configuration through the cloud firewall to help you complete traffic access control between VPC and VPN (manual traffic diversion configuration).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This article contains important tips that you need to pay attention to; ignoring this information may impact your business, so please read carefully.</div>


<span id="a3b57db1"></span>
# Scenario introduction


* Redirect traffic from VPC\-01 to VPN\-02 to the cloud firewall.

* Configure access control policy: only allow the `10.2.0.0/26` subnet in VPN\-02 to access the cloud VPC, disallowing access from other subnets.

   
   |**Resource type** |**Affiliated Region** |**VPC/Dedicated line subnet** |**Subnet segment** |
   |---|---|---|---|
   |VPC\-01 |South China 1 (Guangzhou) |10.1.0.0/16 |sunnet\-01：10.1.0.0/24 |
   |VPN\-02 |Third\-party cloud |10.2.0.0/16 |10.2.0.0/24 |
   |tr transit router |South China 1 |N/A |N/A |
   


<span id="d2b36ec8"></span>
# **Requirements**


* The required VPC and subnet creation has been completed. For detailed steps, please refer to [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* The creation of cloud server instances in each VPC has been completed. For detailed steps, please refer to [Purchase Cloud Server Instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) to continue.

* The creation of transit router instances and network instance connections has been completed. For detailed steps, please refer to [Create Transit Router Instances](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-01).

* Cloud firewall enterprise edition and above sales specifications have been purchased.


<span id="92056104"></span>
# **Usage restrictions**


* When there are static routes within `100.64.0.0/10` in the routing table of the transit router, flow configuration is not supported.

* Flow configuration is not supported for network instances with routing conflicts (VPC, dedicated line, VPN), including routing conflicts between network instances, and routing conflicts between network instances and the firewall VPC. After configuring automatic flow scenarios, the network will be interrupted. It is recommended to reasonably configure the firewall VPC segment according to business needs.


<span id="bb5a759a"></span>
# Step 1: Create a VPC boundary firewall


1. Log in to the [cloud firewall console](https://console.byteplus.com/firewall/overview). In the left navigation bar, click on **Firewall Switch**.

2. On the **Firewall Switch** page, click **VPC Boundary Firewall**.

3. Locate the forwarding router under the cloud enterprise network instance of the target VPC boundary firewall, and click **Action** column’s **Create Cloud Firewall**.

4. Select **Manual Flow** mode, and click Submit and Next. You can manually create a VPC boundary firewall on the TR transit router and configure routing according to your own business situation, pulling the traffic to the VPC boundary firewall.

5. Create a VPC boundary firewall, configure the following parameters. The cloud firewall is expected to take 10 minutes during the creation process.

   
   |**Configuration item** |**Configuration description** |**Configuration parameter** |
   |---|---|---|
   |Firewall name |Define the name of the VPC boundary firewall. This name is used to identify the VPC boundary firewall instance, and it is recommended that you enter a meaningful name based on the actual situation of the business. |Dedicated line and VPC boundary protection |
   |Firewall VPC subnet |Allocate a subnet for the automatically created cloud firewall's VPC, and divide the allocated VPC subnet into 3 subnet segments. 。 The mask for the 3 subnet segments of the cloud firewall must be less than or equal to 28 bits and must not conflict with the planned network segments. |192.168.0.0/24 |
   |VPC subnet 1 segment ||192.168.0.16/28 |
   |VPC subnet segment 2 ||192.168.0.32/28 |
   |VPC subnet 3 segment ||192.168.0.48/28 |
   

6. After the traffic diversion scenario is created. In the TR network instance connection, the VPC of the cloud firewall will be added, and the connection name will be **CFW_system_please_do_not_edit**.


<span id="646ae9af"></span>
# Step 2: Manual routing configuration

You can manually create a VPC boundary firewall and configure the routing on the TR intermediate router based on your business situation, redirecting traffic to the VPC boundary firewall. The following example is for reference only for traffic diversion between VPC\-01 and VPN\-02.


|**Routing table** |**Associated forwarding** |**Routing entry <a i=1\>Description</a\>**  |
|---|---|---|
|System routing |None |1. Add self\-learning routes for **VPC\-01** instances.<br><br>2. Manually add a static route with a destination of `10.2.0.0/16` and a next hop of **VPN\-02**. Note: Adding routes for VPC and VPN in the system routing table is intended for fallback protection when the firewall is bypassed. |
|Routing Table 1 |**Associated forwarding VPC\-01** |1. Add a static route with the destination of `10.2.0.0/16` and the next hop of **CFW_system_please_do_not_edit**. Note: This is to direct the traffic from VPC\-01 to the VPN towards the cloud firewall for protection. |
|Routing table 2 |**Associated forwarding to VPN\-02** |1. Add a static route with the destination `10.1.0.0/16` and next hop **CFW_ststem_please do not edit**. Note: The purpose is to direct VPN traffic to VPC\-01 for protection by the Cloud Firewall. |
|Firewall Routing Table |**CFW_ststem_please do not edit.**  |1. Add a static route with destination `10.1.0.0/16` and next hop **VPC\-01**.<br><br>2. Add a static route with destination `10.2.0.0/16` and next hop **VPN\-02**. Note: This is to forward traffic that has gone through cloud firewall protection and cleaning to the business destination network instance. |


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>



* <div data-tips="true" data-tips-type="danger">When the <strong>traffic diversion scenario of the VPC cloud firewall is closed or deleted, and the VPC cloud firewall is upgraded, fails, or deleted</strong>, and when the <strong>VPC firewall instance expires or is unsubscribed</strong>, the cloud firewall will activate the Bypass mechanism, switching the routing table associated with forwarding instances that contain the next hop as <strong>CFW_system_please_do_not_edit</strong> to the system routing to ensure that business continuity is not interrupted. Therefore, users need to configure a fallback route in the system routing to avoid business impact.</div>


* <div data-tips="true" data-tips-type="danger">After the VPC cloud firewall Bypass, you need to manually switch the VPN\-02 and VPC\-01 network instances in the system routing to routing table 1 and routing table 2 in a timely manner to ensure that the business is promptly protected.</div>



<span id="eb78c168"></span>
# Step 3: Access control policy configuration

When managing traffic between VPCs, you need to first reject suspicious or malicious traffic, or allow trusted traffic before rejecting access from other addresses. Regarding the configuration example of VPC boundary access control policies, the policy configuration parameters are as follows. Example: Only allow **VPN\-02** in the `10.2.0.0/26` subnet to access the cloud VPC, while denying access to other subnets.


1. Log in to [Cloud Firewall Console](https://console.byteplus.com/firewall/overview).

2. In the left navigation bar, select **Access Control**.\>**VPC Boundary.**  On the **VPC Boundary** page, select **The corresponding VPC firewall**, then click **Add Policy**.

3. Cloud firewall defaults to allow traffic without policies. Therefore, it is necessary to configure two access control policies: one to allow traffic from the **VPN\-02** `10.2.0.0/26` subnet to access the cloud VPC as a high\-priority allow policy, and another to block all **VPN\-02** traffic from accessing the host as a low\-priority block policy.

4. **Add Allow Policy**.


<div style="text-align: center">
</div>



|**Configuration item** |**Configuration Description** |**Configuration parameters** |
|---|---|---|
|**Rule priority** |Select the priority of this policy, here we choose the highest priority. After configuration is complete, you can also click **move** in the access control policy list to customize the adjustment of policy priority.<br><br><br>* **Highest priority**: refers to the highest effective priority of the access control policy, taking effect first.<br><br>* **Lowest priority**: refers to the lowest effective priority of the access control policy, taking effect last. |Highest priority |
|**Access source type** |You need to select the data source type and enter the data source address according to the data source type. Here select the IP type and enter `10.2.0.0/26`.<br><br><br>* When selecting **IP** type, you need to enter the IP address or IP address range. Such as `180.184.1.1` or `180.184.0.0/16`, `0.0.0.0/0` represents all.<br><br>* When selecting **Address Book** type, you need to create an IP address book in advance. |IP |
|**Access source** ||**10.2.0.0/26** |
|**Access purpose type** |You need to select the type of access destination and enter the access destination address according to the selected type. Select the IP type here and enter `0.0.0.0/0`.<br><br><br>* When selecting **IP** type, you need to enter an IP address or an IP address range. For example, `180.184.1.1` or `180.184.0.0/16`, `0.0.0.0/0` represents all.<br><br>* When selecting **address book** type, you need to create an IP address book in advance.<br><br>* When selecting **domain name** type, you need to enter the destination domain name address.<br><br>   * Enter the domain name, supporting a single domain name `example.com`, wildcard domain name `*.example.com`, and multi\-level domain name `example1.example2.com`.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Please do not enter protocol content such as http(s).   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The principle of domain access empty policy is to obtain domain name data for matching control based on the Host information in the HTTP protocol data and the Server Name information in the Client Hello of the HTTPS protocol packet. If your business traffic data packets do not contain these two fields, the domain policy cannot take effect.   </div><br>    |IP |
|**Access destination** ||0.0.0.0/0 |
|**Protocol type** |Transport layer protocol type, supports setting to: **TCP**, **UDP**, **ICMP**, **ANY**. If the specific protocol is uncertain, you can choose **ANY.**  |ANY |
|**Action** |Set the situation of allowing matching successful traffic in this policy.<br><br><br>* **Allow**: Allow this traffic, record allow logs in the access control log, and record traffic logs in the traffic session.<br><br>* **Block**: Intercept this traffic, logs will be recorded in the access control log.<br><br>* **Observe**: Allow this traffic. The observation log will be recorded in the access control logs. |Release |
|**Description** |Input current policy content and usage scenarios. To help you identify and apply the address book |10.4.0.0/26 access to the cloud VPC |
|**Policy switch** |Set the Policy switch. If you did not enable the policy when creating it, you can turn on the policy in the policy list. |Keep it enabled |



5. **Add Block Policy**: Configure a low\-priority block policy that denies access to the host for all Dedicated Line\-04 traffic. **Blocking** access control policy configuration parameters are as follows:

   
   |**Configuration item** |**Configuration Parameter** |
   |---|---|
   |**Rule priority** |Lowest priority |
   |**Access source type** |IP |
   |**Access source** |0.0.0.0/0 |
   |**Access purpose type** |IP |
   |**Access destination** |0.0.0.0/0 |
   |**Protocol type** |ANY |
   |**Destination port type** |Port |
   |**Destination port** |0/65535 |
   |**Action** |Block |
   |**Description** |Block dedicated line \- All port access for flow |
   |**Policy switch** |Keep it enabled |
