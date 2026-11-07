---
title: "Traffic access control between VPN and dedicated line (manual flow configuration)"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Access_control_for_traffic_between_a_VPN_and_an_instance"
---

This article introduces the manual flow configuration through the cloud firewall, helping you complete traffic access control between VPC and dedicated line (manual flow configuration).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This article contains important prompt information that you need to pay attention to; ignoring this information may affect your business, so please read carefully.</div>


<span id="a3b57db1"></span>
# Scenario Introduction


* Redirecting traffic between VPC\-01 and VPN\-02 to the cloud firewall.

* Configuration access control policy: Only allow the `10.2.0.0/26` subnet in VPN\-02 to access the cloud VPC, and deny access from other subnets.

   
   |**Resource type** |**Region** |**VPC/dedicated line segment** |**Subnet Network Segment** |
   |---|---|---|---|
   |VPC\-01 |South China 1 (Guangzhou) |10.1.0.0/16 |sunnet\-01：10.1.0.0/24 |
   |VPN\-02 |Third\-party cloud |10.2.0.0/16 |10.2.0.0/24 |
   |tr Transfer Router |South China 1 |N/ |N/A |
   


<span id="d2b36ec8"></span>
# **Requirements**


* The required VPC and subnet creation has been completed. For detailed steps, please refer to [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* The creation of cloud server instances in each VPC has been completed. For detailed steps, please refer to [Purchase Cloud Server Instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) to continue.

* The creation of transit router instances and network instance connections has been completed. For detailed steps, please refer to [Create Transit Router Instances](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-01).

* Cloud firewall enterprise edition and above sales specifications have been purchased.


<span id="92056104"></span>
# **Usage restrictions**


* When there are static routes within `100.64.0.0/10` in the routing table of the transit router, draining configuration is not supported.

* Draining configuration is not supported for network instances (VPC, dedicated line, VPN) with routing conflicts, including routing conflicts between network instances and routing conflicts between network instances and firewall VPC. After configuring automatic draining scenarios, the network will be interrupted; it is recommended to reasonably configure the firewall VPC segment based on business needs.


<span id="bb5a759a"></span>
# Step 1: Create VPC boundary firewall


1. Log in to [Cloud Firewall Console](https://console.byteplus.com/firewall/overview). In the left navigation bar, click **Firewall Switch**.

2. On the **Firewall Switch** page, click **VPC Boundary Firewall**.

3. Locate the forwarding router under the cloud enterprise network instance of the target VPC boundary firewall, and click **Action** column's **Create Cloud Firewall**.

4. Select **Manual Draining** mode, and click submit and next. You can manually create a VPC boundary firewall and configure routes on the TR transit router according to your business situation to direct traffic to the VPC boundary firewall.

5. Create a VPC boundary firewall, configure the parameters as follows. The cloud firewall is expected to take 10 minutes during the creation process.

   
   |**Configuration item** |**Configuration description** |**Configuration parameter** |
   |---|---|---|
   |Firewall name |Define the name of the VPC boundary firewall. This name is used to identify the VPC boundary firewall instance. It is recommended that you enter a meaningful name based on the actual business situation. |Dedicated Line and VPC Boundary Protection |
   |Firewall VPC subnet |Assign a subnet to the automatically created cloud firewall's VPC and divide three subnet segments from the assigned VPC subnet. The subnet mask of the 3 subnets of the cloud firewall must be less than or equal to 28 bits and must not conflict with the subnets planned in the network. |192.168.0.0/24 |
   |VPC Subnet 1 Network Segment ||192.168.0.16/28 |
   |VPC subnet 2 segment ||192.168.0.32/28 |
   |VPC subnet 3 segment ||192.168.0.48/28 |
   

6. After the flow diversion scenario is created, the TR network instance connection will include the cloud firewall's VPC, with the connection name **CFW_ststem_please do not edit**.


<span id="646ae9af"></span>
# Step 2: Manual route configuration

You can manually create a VPC boundary firewall and configure the route on TR’s transit router based on your business situation, directing traffic to the VPC boundary firewall. The following example illustrates the flow diversion between VPC\-01 and VPN\-02 for reference only.


|**Routing table** |**Associated forwarding** |**Routing entry description** |
|---|---|---|
|System routing |None |1. Add **VPC\-01** instance's self\-learning route.<br><br>2. Manually add a static route with destination `10.2.0.0/16` and next hop **VPN\-02**. Note: Adding routes for VPC and VPN in the system routing table is to provide fallback protection when bypassing the firewall. |
|Routing table 1 |**Associated forwarding VPC\-01** |1. Add a static route with the destination `10.2.0.0/16` and next hop **CFW_system_please_do_not_edit**. <br><br>2. Note: To direct traffic from VPC\-01 to VPN through the cloud firewall for protection. |
|Routing table 2 |**Associate with forwarding <a i=2\>VPN\-02</a\>**  |1. Add a static route with the destination of `10.1.0.0/16` and the next hop of **CFW_system_please do not edit**. \nNote: To direct the traffic from VPN to VPC\-01 to the cloud firewall for protection. |
|Firewall routing table |**CFW_ststem_please do not edit.**  |1. Add a static route with a destination of `10.1.0.0/16` and next hop as **VPC\-01**.<br><br>2. Add a static route with a destination of `10.2.0.0/16` and next hop as **VPN\-02**. Note: To forward traffic protected and cleaned by the cloud firewall to the business destination network instance. |


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>



* <div data-tips="true" data-tips-type="danger">When the VPC cloud firewall <strong>flow diversion scenario is closed, deleted, or the VPC cloud firewall is upgraded, malfunctions, or deleted</strong>, as well as when <strong>the VPC firewall instance expires and unchecks</strong>, the cloud firewall will enable the Bypass mechanism, switching routes associated with the next hop <strong>CFW_ststem_please do not edit</strong> to the system route to ensure no service disruption. Therefore, users need to configure fallback routes in the system routes to avoid impacting services.</div>


* <div data-tips="true" data-tips-type="danger">After the VPC cloud firewall Bypass, you need to manually switch the VPN\-02 and VPC\-01 network instances from the system route to route table 1 and route table 2 promptly to ensure timely protection for the services.</div>



<span id="9f4c211b"></span>
# Step 3: Access control policy configuration

When managing traffic between VPCs, you first need to reject suspicious or malicious traffic, or first allow trusted traffic, then deny access from other addresses. For the configuration example of VPC boundary access control policies, the policy configuration parameters are as follows. Example: Only **VPN\-02** subnet `10.2.0.0/26` is allowed to access the cloud VPC, other subnets are not allowed to access.


1. Log in to the [Cloud Firewall Console](https://console.byteplus.com/firewall/overview).

2. In the left navigation bar, select **Access Control**.\>VPC boundary. On the **VPC Boundary** page, select **the VPC firewall to which it belongs** and click **Add Policy**.

3. The Cloud Firewall allows traffic by default without policies. Therefore, you need to configure 2 access control policies, one to allow traffic from **VPN\-02** subnet `10.2.0.0/26` to access the cloud VPC with a high priority allow policy, and another to block all **VPN\-02** traffic from accessing this host with a low priority block policy.

4. **Add Allow Policy**.



|**Configuration item** |**Configuration description** |**Configuration parameter** |
|---|---|---|
|**Rule priority** |Select the priority of this policy. Here, choose the highest priority. After configuration is complete, you can also click **Move** in the access control policy list to customize the priority of the policy.<br><br><br>* **Highest priority**: Refers to the highest priority at which the access control policy takes effect, taking effect first.<br><br>* **Lowest priority**: Refers to the lowest priority at which the access control policy takes effect, taking effect last. |Highest priority |
|**Access Source Type** |You need to select the access source <Data type\> and enter the access source address according to the access source <Data type\>. Select IP <Data type\> here and enter `10.2.0.0/26`.<br><br><br>* When selecting **IP** <Data type\>, you need to enter an IP address or IP address range. Such as `180.184.1.1` or `180.184.0.0/16`, `0.0.0.0/0` represents all.<br><br>* When selecting **address book** <Data type\>, you need to create an IP address book in advance. |IP |
|**Access source** ||**10.2.0.0/26** |
|**Access Destination Type** |You need to choose the data type of access destination, and input the access destination address based on the data type. Select the IP data type and enter `0.0.0.0/0`.<br><br><br>* When selecting **IP** type, you need to enter the IP address or IP address range. For example, `180.184.1.1` or `180.184.0.0/16`, `0.0.0.0/0` represents all.<br><br>* When selecting **address book** type, you need to create an IP address book in advance.<br><br>* When selecting **domain name** type, you need to enter the target domain name address.<br><br>   * Entering the domain name supports single domain `example.com`, wildcard domain `*.example.com`, and multi\-level domain `example1.example2.com`.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Please do not enter protocol contents such as http(s).   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The empty policy principle of domain name access is to match control based on the Host information in the HTTP protocol data and the Server Name information in the Client Hello of the HTTPS protocol data packet. If your business traffic data packets do not contain these two fields, the domain name policy will not take effect.   </div><br>    |IP |
|**Access destination** ||0.0.0.0/0 |
|**Protocol type** |Transport layer protocol type, supports configuration as: **TCP**, **UDP**, **ICMP**, **ANY**. If the specific protocol is uncertain, **ANY** can be selected. |ANY |
|**Action** |Set the result of allowing matched traffic in this policy.<br><br><br>* **Allow**: Allow this traffic, record allow logs in the access control log, and record traffic logs in the traffic session.<br><br>* **Block**: Intercept this traffic, block logs will be recorded in the access control log.<br><br>* **Observe**: Allow this traffic. Observation logs will be recorded in the access control log. |Allow |
|**Description** |Input the current policy content and usage scenarios. To help you identify and apply address book |10.4.0.0/26 access to cloud VPC |
|**Policy switch** |Set the <Policy switch\>. If you have not enabled the policy when creating it, you can turn on the policy in the policy list. |Keep it enabled |



5. **Add Block Policy**: Configure a low priority block policy for all Dedicated Line\-04 traffic accessing this host. The **block** access control policy configuration parameters are as follows:

   
   |**Configuration item** |**Configuration parameter** |
   |---|---|
   |**Rule priority** |Minimum priority |
   |**Access source type** |IP |
   |**Access source** |0.0.0.0/0 |
   |**Access destination type** |IP |
   |**Access purpose** |0.0.0.0/0 |
   |**Protocol type** |ANY |
   |**Destination port type** |Port |
   |**Destination port** |0/65535 |
   |**Action** |Block |
   |**Description** |Block dedicated line \- All port access for flow 04 |
   |**Policy switch** |Keep it enabled |
