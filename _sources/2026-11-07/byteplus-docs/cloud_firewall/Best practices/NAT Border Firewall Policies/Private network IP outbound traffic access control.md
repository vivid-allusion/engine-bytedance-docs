---
title: "Private network IP outbound traffic access control"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Private_network_IP_outbound_traffic_access_control"
---

This article introduces the configuration of cloud firewall traffic diversion, helping you complete access control in the scenario of private network IP outbound traffic.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This article contains important reminder information that you need to pay attention to; ignoring this information may impact your business, so please read carefully.</div>



---



<span id="50451b62"></span>
# Example scenario

Two ECS (hosts) with private network IPs under the NAT gateway are `192.168.1.1` and `192.168.2.1`, which need to be configured to allow access only to the `console.example.com` domain. The cloud firewall allows all traffic by default when no policies are configured, so in this scenario, 2 access policies need to be configured. One is a high priority allow policy that permits outbound traffic to the `console.example.com` domain; the other is a low priority deny policy that blocks all outbound traffic from this host.

<span id="e62eb63f"></span>
# **Usage restrictions**


* The VPC subnet where the NAT gateway is located cannot contain any other business resources.

* The route table of the VPC subnet where the NAT gateway is located cannot contain other task business subnets.

* The route table in the subnet where the NAT gateway is located cannot be a system route table; it must be a custom route table.


<span id="1a1e4126"></span>
# Create NAT firewall


1. Log in to [the Cloud Firewall Console](https://console.byteplus.com/firewall/overview), and click **Firewall Switch** in the left navigation bar.

2. On the **Firewall Switch** page, click **NAT Boundary Firewall**.

3. Select the NAT gateway that needs protection from the table below and click **New Cloud Firewall**.

4. The Cloud Firewall will start a status check to verify the creation conditions for the current NAT firewall, which must meet the following three conditions.

   * The VPC subnet where the NAT gateway is located cannot contain any other business resources.

   * The route table of the VPC subnet where the NAT gateway is located cannot contain other task business subnets.

   * The route table of the subnet where the NAT gateway is located cannot be a system route table; it must be a custom route table.

5. Refer to the table below to configure the relevant Parameter.



|**Parameter** |**Note** |**Sample values** |
|---|---|---|
|Firewall name |Customize the NAT firewall name based on the actual business situation, used to identify the NAT firewall instance. |Develop NAT firewall |
|Protective bandwidth specification |You need to allocate protective bandwidth for this NAT firewall based on the actual business traffic size. When the business traffic bandwidth exceeds the protective bandwidth, the cloud firewall will send alarm notifications via SMS, email, and in\-site messages. |500Mbps |
|Firewall subnet configuration |For NAT firewall configuration, the recommended network bits for the subnet segment are between 16\-28. |192.168.4.0/24 |


<span id="ca0abfec"></span>
# Draining configuration

<span id="4c98cc2a"></span>
## Route planning

Before proceeding with configuration, you need to plan the routing data information of various network resources in the network diagram in advance.


1. Business subnet and routing table, NAT gateway subnet and routing table, NAT firewall subnet and routing table, as shown in the table below.



|Subnet type |Subnet segment |Bind routing table |
|---|---|---|
|Business subnet |192.168.1.0/24 |Business subnet routing table (system routing table) |
|Business subnet |192.168.2.0/24 ||
|NAT firewall subnet |192.168.4.0/24 |Firewall subnet routing table |
|NAT gateway subnet |192.168.3.0/24 |NAT gateway subnet routing table |



2. The routing table planning is shown in the diagram below.

   1. The business subnet routing table 0.0.0.0/0 points to the Firewall drain node, directing outgoing traffic to the cloud firewall for filtering and auditing.

   2. The NAT firewall subnet routing table 0.0.0.0/0 points to the NAT gateway, directing outgoing traffic after filtering by the cloud firewall to the NAT gateway. The system default route is used for inbound traffic drainage, and has no impact on outbound drainage, for details refer to [Private IP inbound traffic access control](https://docs.byteplus.com/en/docs/cloud_firewall/Access_control_for_private_network_IP_inbound_traffic).


<span id="bbbb5043"></span>
## Drainage operation

You need to complete the drainage configuration according to the above routing table planning.


1. Complete the drainage configuration from the NAT firewall to the NAT gateway. After the cloud firewall is created, the following resources will be created by default, and the drainage configuration between the NAT firewall and the NAT gateway will be completed automatically.



|Resource type |Resource parameter |Resource Description |
|---|---|---|
|Subnet |Subnet segment: `192.168.4.0/24` |Used for deploying NAT firewall diversion nodes. |
|Auxiliary network card |Name: eni\-for\-ep\-\*\*\*\*\*\*\nDescription: Created by PrivateLink |The auxiliary network card uses BytePlus PrivateLink service to redirect outbound traffic to the cloud firewall for filtering and auditing. |
|Routing table |Name: NAT_Firewall_RT\-nfw\-\*\*\*\*\*\* |This routing table forwards traffic filtered by the NAT firewall to the NAT gateway. The cloud firewall will by default configure a route pointing `0.0.0.0/0` to the NAT gateway. |
|Routing table |Name: NAT_Firewall\-Bypass_RT\-nfw\-\*\*\*\*\*\* |This routing table will be used for incoming traffic protection during bypass, with no impact on outgoing traffic. For details, please refer to [Private Network IP Incoming Traffic Access Control](https://docs.byteplus.com/en/docs/cloud_firewall/Access_control_for_private_network_IP_inbound_traffic) |



2. Complete the drainage configuration from the business subnet to the NAT firewall manually.

   1. In the business subnet routing table, first delete the route for 0.0.0.0/0 pointing to the NAT gateway.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Deleting the route for 0.0.0.0/0 pointing to the NAT gateway will impact service interruption, it is recommended to perform this operation during low business peak periods.</div>



2. Add a route that directs traffic destined for 0.0.0.0/0 to the diversion node of the auxiliary network card created by the cloud firewall.

   * Target subnet: 0.0.0.0/0;

   * Next hop type: Gateway Load Balancing Interruption Node;

   * Next hop: NAT_Firewall_Endpoint\-nfw (eni\-for\-ep\-\*\*\*\*\*\*).


<span id="8ac90746"></span>
# Create Policy

When configuring control for private IP outbound traffic, you need to first deny suspicious or malicious traffic, or allow trusted traffic first and then deny access from other addresses. Regarding the configuration example of NAT boundary access control policies, the policy configuration parameters are as follows.


1. Log in to [Cloud Firewall Console](https://console.byteplus.com/firewall/overview).

2. In the left navigation bar, select **Access Control**.\>**NAT boundary**.

3. On the **NAT boundary** page, select the **associated NAT firewall**, choose **outbound rules**, and click **add policy**.


<span id="04f34ecc"></span>
## **Add allowance policy**


|**Configuration item** |**Configuration Description** |**Configuration parameter** |
|---|---|---|
|**Rule priority** |Select the priority of this policy; here, choose the highest priority. After configuration, you can also click **Move** in the access control policy list to customize the adjustment of the policy priority.<br><br><br>* **Highest Priority**: Refers to the highest priority at which the access control policy is effective, taking effect first.<br><br>* **Lowest Priority**: Refers to the lowest priority at which the access control policy is effective, taking effect last. |Highest priority |
|**Access source type** |You need to select the access source type and input the access source address based on the access source type. Select the address book type here. And choose to add an IP address book, adding `192.168.1.1` and `192.168.2.1`.<br><br><br>* When selecting **IP** type, you need to input the IP address or the IP address range. Such as `180.184.1.1` or `180.184.0.0/16`, `0.0.0.0/0` represents all.<br><br>* When selecting **address book** type, you need to create the IP address book in advance. |Address book |
|**Access Source** |||
|**Access destination type** |You need to choose the access purpose type and input the access destination address according to the access purpose type. Here, select the domain name type and enter `console.example.com`.<br><br><br>* When selecting **IP** type, you need to enter the IP address or IP address range. Such as `180.184.1.1` or `180.184.0.0/16`, `0.0.0.0/0` represents all.<br><br>* When selecting **address book** type, you need to create an IP address book in advance.<br><br>* To select the **domain** type, you need to enter the destination domain address<br><br>   * The input domain supports single domain `example.com`, wildcard domain `*.example.com`, and multi\-level domain `example1.example2.com`<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Please do not enter content such as http(s) protocols.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The principle of domain access control policy is to match control based on the domain data obtained from the Host information in the HTTP protocol data and the Server Name information in the Client Hello of the HTTPS protocol data packets. If your business traffic data package does not include these two fields, the domain policy will not take effect.   </div><br>    |Domain name. |
|**Access destination** ||`console.example.com` |
|**Protocol type** |Transport layer protocol type, supports settings for: **TCP**, **UDP**, **ICMP**, **ANY**. When the specific protocol is uncertain, **ANY** can be selected. |TCP |
|**Action** |Set the allowance status of traffic that matches successfully in this policy.<br><br><br>* **Allow**: Allow this traffic, log the allowance in the access control log, and record the traffic log in the traffic session.<br><br>* **Block**: Intercept this traffic, and log the block in the access control log.<br><br>* **Monitor**: Allow this traffic. Monitoring logs will be recorded in the access control log. |Allow |
|**Description** |Enter the current policy content and usage scenarios. This helps you identify and apply the policy. |Visit the domain `console.example.com` |
|**Policy switch** |Set the policy switch. If you did not enable the policy when creating it, you can turn on the policy in the policy list. |Keep it enabled |


<span id="658bf125"></span>
## **Add block policy**

Configure a low\-priority full\-block policy. The configuration parameters for the **block** access control policy are as follows:


|**Configuration item** |**Configuration parameters** |
|---|---|
|**Rule priority** |Minimum priority |
|**Access source type** |IP |
|**Access source** |0.0.0.0/0 |
|**Access purpose type** |IP |
|**Access purpose** |0.0.0.0/0 |
|**Protocol type** |ANY |
|**Destination port type** |Port |
|**Destination port** |0/65535 |
|**Action** |Block |
|**Description** |Block other access policies |
|**Policy switch** |Keep it enabled |


<span id="63a760aa"></span>
# Delete NAT firewall

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before deleting the NAT firewall, you need to complete the traffic diversion configuration within the VPC, redirecting business traffic away from the firewall before performing the deletion operation. Due to the impact on business during the route switching period, it is recommended to carry out this operation during off\-peak business hours.</div>



1. First, delete the route in the business subnet that points 0.0.0.0/0 to the NAT firewall diversion node.

2. After deletion, add a route pointing 0.0.0.0/0 to the NAT gateway to complete the traffic migration.

3. Finally, delete the NAT firewall instance in the Cloud Firewall console.


<span id="09fedf27"></span>
# NAT Firewall Abnormality Description

When the cloud firewall instance is abnormal, the cloud firewall will enable Bypass mode, automatically diverting business traffic from the firewall. Bypass logic description:


1. The NAT firewall will first delete the route pointing from 0.0.0.0/0 in the business subnet to the NAT firewall diversion node, redirecting traffic away from the NAT firewall.

2. After deletion, the NTA firewall will add a route pointing from 0.0.0.0/0 to the NAT gateway to complete the traffic migration.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Ensure that the 0.0.0.0/0 route is not occupied by other business routes to avoid being unable to create a new route when the NAT firewall is in Bypass mode, which can lead to business interruption.</div>
