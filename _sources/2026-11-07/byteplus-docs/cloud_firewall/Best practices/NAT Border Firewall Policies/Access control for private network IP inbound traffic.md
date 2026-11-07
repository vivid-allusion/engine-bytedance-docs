---
title: "Access control for private network IP inbound traffic"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Access_control_for_private_network_IP_inbound_traffic"
---

This article introduces the cloud firewall flow configuration to help you complete access control for private network IP inbound traffic scenarios.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This article contains important tip information that you need to pay attention to; ignoring this information may impact your business, so please read carefully.</div>



---



<span id="913523de"></span>
# Example scenario

Two ECS (hosts) under the NAT gateway have private network IPs of `192.168.1.1:22` and `192.168.2.1:22`, and it is necessary to set up access only for external IP `10.0.0.1`. \nThe cloud firewall allows all traffic by default when no policy is configured; therefore, in this scenario, 2 access policies need to be configured. One is a high\-priority allow policy that allows `10.0.0.1` to access the inbound traffic of both assets on port 22; the other is a low\-priority deny policy that blocks all inbound traffic to all ports of the host.

<span id="d3c4c418"></span>
# **Usage restrictions**


* The VPC subnet where the NAT gateway is located cannot contain any other business resources.

* The route table of the VPC subnet where the NAT gateway is located cannot contain other task business subnets.

* The route table of the subnet where the NAT gateway is located cannot be a system route table; it must be a custom route table.


<span id="2bd484b3"></span>
# Create NAT firewall


1. Log in to [Cloud Firewall Console](https://console.byteplus.com/firewall/overview), click **Firewall Switch** in the left navigation bar.

2. On the **Firewall Switch** page, click **NAT Boundary Firewall**.

3. Select the NAT gateway that needs protection in the table below and click **New Cloud Firewall**.

4. Status check, verify the current NAT firewall creation conditions, which need to meet the following three conditions.

   * The VPC subnet where the NAT gateway is located cannot contain any other business resources.

   * The routing table of the VPC subnet where the NAT gateway is located cannot contain other task business subnets.

   * The routing table of the subnet where the NAT gateway is located cannot be the system routing table; it needs to be a custom routing table.

5. Refer to the table below to configure the relevant Parameter



|**Parameter** |**Note** |**Example of value** |
|---|---|---|
|Firewall name |Customize the NAT firewall name based on the actual business situation for identifying the NAT firewall instance. |Development NAT Firewall |
|Protection bandwidth specifications |You need to allocate protection bandwidth for the NAT firewall based on the actual business traffic size. When the business traffic bandwidth exceeds the protection bandwidth, the cloud firewall will send alarm notifications via SMS, email, and in\-site messages. |500Mbps |
|Firewall subnet configuration |Configure the subnet segment for the NAT firewall; the network bits of the subnet segment are recommended to be between 16 and 28. |192.168.4.0/24 |


<span id="c148d749"></span>
# Draining configuration

<span id="e53bc3da"></span>
## Route planning

Before configuration, you need to plan the routing data information for each network resource in the network topology in advance.


1. The business subnet and routing table, NAT gateway subnet and routing table, NAT firewall subnet and routing table are shown in the table below.



|Data type |Subnet segment |Bind routing table |
|---|---|---|
|Business subnet |192.168.1.0/24 |Business subnet routing table (system routing table) |
|Business subnet |192.168.2.0/24 ||
|NAT firewall subnet |192.168.4.0/24 |Firewall subnet routing table |
|NAT gateway subnet |192.168.3.0/24 |NAT gateway subnet routing table |



2. The routing table planning is shown in the figure below.

   * NAT firewall subnet routing table `192.168.1.0/24`, `192.168.2.0/24` points to the business subnet, and the inbound traffic filtered by the cloud firewall is redirected to the business subnet. The `0.0.0.0/0` route is used for outbound traffic redirection, with no impact on inbound traffic; for details, refer to [Private IP Outbound Traffic Access Control](https://docs.byteplus.com/en/docs/cloud_firewall/Private_network_IP_outbound_traffic_access_control).

   * NAT gateway subnet routing table redirects `192.168.1.0/24` and `192.168.1.0/24` to the Firewall redirection node, directing inbound traffic to the cloud firewall for filtering and auditing.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the same purpose, the routing for <code>192.168.1.0/24</code> and <code>192.168.1.0/24</code> points to the cloud firewall route, which has a higher priority than the system default.</div>


<span id="a43eff71"></span>
## Redirection operation

You need to complete the redirection configuration according to the above routing table planning.


1. Complete the redirection configuration from the NAT firewall to the business subnet. After the cloud firewall is created, the following resources will be created by default and the redirection configuration between the NAT firewall and the business subnet will be completed automatically.



|Resource type |Resource parameters |Resource Description |
|---|---|---|
|Subnet |Subnet segment: `192.168.4.0/24` |Used for deploying NAT firewall drain nodes. |
|Auxiliary network card |Name: eni\-for\-ep\-\*\*\*\*\*\*<br\>Description: Created by PrivateLink |The auxiliary NIC uses the BytePlus PrivateLink service to direct incoming traffic to the cloud firewall for filtering and auditing. |
|Routing table |Name: NAT_Firewall_RT\-nfw\-\*\*\*\*\*\* |This routing table will forward traffic filtered by the NAT firewall to the business subnet. By default, routes pointing to the business subnet for `192.168.1.0/24` and `192.168.2.0/24` will be configured. |
|Routing table |Name: NAT_Firewall——Bypass_RT\-nfw\-\*\*\*\*\*\* |This routing table will be used for incoming traffic protection bypass. |



2. Complete the traffic redirection configuration from the NTA gateway to the NAT firewall. The NAT gateway subnet route table requires you to manually add two routes:



|Destination Network Segment |Next hop type |Next hop |Note |
|---|---|---|---|
|`192.168.1.0/24` |Gateway load balancing interruption node |NAT_Firewall_Endpoint\-nfw（eni\-for\-ep\-\*\*\*\*\*\*） |Direct the `192.168.1.0/24` to the auxiliary NIC drainage node created by the cloud firewall |
|`192.168.2.0/24` |Gateway load balancing interrupt node |NAT_Firewall_Endpoint\-nfw（eni\-for\-ep\-\*\*\*\*\*\*） |Direct the `192.168.2.0/24` to the auxiliary NIC drainage node created by the cloud firewall |


<span id="540fd43d"></span>
# Create policy

When configuring control for incoming traffic to a private IP, you need to either deny suspicious or malicious traffic, or allow trusted traffic first and then deny access from other addresses. For an example of configuring NAT boundary access control policies, the policy configuration parameters are as follows.


1. Log in to [Cloud Firewall Console](https://console.byteplus.com/firewall/overview).

2. In the left navigation bar, select **Access Control**.\>**NAT Boundary**.

3. On the **NAT Boundary** page, select **The corresponding NAT firewall**, choose **Inbound Rules**, and click **Add Policy**.


<span id="c8d22d43"></span>
## **Add Policy**


|**Configuration item** |**Configuration description** |**Release policy** |**Block policy** |
|---|---|---|---|
|**Rule priority** |Select the priority of this policy; here, choose the highest priority. After configuration is complete, you can also custom adjust the policy priority by clicking **Move** in the access control policy list.<br><br><br>* **Highest priority**: Refers to the highest priority at which the access control policy takes effect, the most effective first.<br><br>* **Lowest priority**: Refers to the lowest priority at which the access control policy takes effect, the last effective. |Highest priority |Lowest priority |
|**Access source type** |You need to select the access source type and input the access source address according to the access source type.<br><br><br>* When selecting **IP** type, you need to enter the IP address or IP address range. For example, `180.184.1.1` or `180.184.0.0/16`, `0.0.0.0/0` represents all.<br><br>* When selecting **Address Book** type, you need to create an IP address book in advance. |IP |IP |
|**Access source** ||`10.0.0.1` |`0.0.0.0/0` |
|**Access purpose type** |You need to select the access destination type and enter the access destination address according to the access destination type.<br><br><br>* When selecting **IP** type, you need to enter the IP address or IP address range. Such as `180.184.1.1` or `180.184.0.0/16`, `0.0.0.0/0` represents all.<br><br>* When selecting **address book** type, you need to create an IP address book in advance.<br><br>* When selecting **domain name** type, you need to enter the destination domain name address. Supports entering domain names, including single domain `example.com`, wildcard domain `*.example.com`, and multi\-level domain `example1.example2.com`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Please do not enter protocol content such as http(s).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The principle of the domain access control policy is to match control based on the domain data obtained from the Host information in the HTTP protocol data and the Server Name information in the Client Hello of the HTTPS protocol data packet. If your business traffic data packets do not contain these two fields, the domain policy will not take effect.</div><br> |Address Book (Configure `192.168.1.1`, `192.168.2.1`) |IP |
|**Access Destination** |||`0.0.0.0/0` |
|**Protocol type** |Transmission layer protocol type, supports setting to: **TCP**, **UDP**, **ICMP**, **ANY**. When the specific protocol is uncertain, you can choose **ANY.**  |ANY |ANY |
|**Destination port type** |Set the destination port type and destination port.<br><br><br>* When selecting **port** type, you need to enter the port or port range, for example, 22, 80/88, 0/65535.<br><br>* **Address book**: When selecting **address book** type, you need to create a port address book in advance. |Port |Port |
|**Destination port** ||22 |0/65535 |
|**Action** |Set the traffic that matches successfully for the release condition of this policy.<br><br><br>* **Pass**: Allow this traffic, log the pass log in the access control log, and record the traffic log in the traffic session.<br><br>* **Block**: Intercept this traffic, and a block log will be recorded in the access control log.<br><br>* **Observe**: Allow this traffic. Observation logs will be recorded in the access control log. |Allow |Block |
|**Description** |Input the current policy content and usage scenarios. Facilitates your identification and application of the policy. |22 port open |Block other access policies |
|**Policy switch** |Set the policy switch. If you do not enable the policy when creating it, you can turn it on in the policy list. |Keep it enabled |Keep it enabled |


<span id="e40df8cc"></span>
# Delete NAT Firewall

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before deleting the NAT firewall, you need to complete the traffic migration configuration within the VPC first, redirecting the business traffic away from the firewall, and then perform the deletion operation. When you need to delete the NAT firewall, simply remove the routes pointing to the Firewall for <code>192.168.1.0/24</code> and <code>192.168.1.0/24</code> in the NAT gateway subnet route table.</div>


<span id="8dba83e3"></span>
# Firewall Abnormality Description

When the cloud firewall instance is abnormal, it will enable Bypass mode, automatically redirecting business traffic away from the firewall. Bypass logic description:

**Firewall Traffic Migration Operation Description**: During Bypass, the cloud firewall will migrate the NAT gateway from `NAT_Firewall_RT-nfw` to `NAT_Firewall-Bypass_RT-nfw` to ensure normal operation of the business. The routing table for `NAT_Firewall-Bypass_RT-nfw` is shown in the diagram below:

<div style="text-align: center">
</div>
