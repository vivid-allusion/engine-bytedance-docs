---
title: "Quick Start"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Getting-started-with-BytePlus-Cloud-Firewall"
---

The cloud firewall provides three types of protection: Internet boundary firewall, VPC boundary firewall, and NAT boundary firewall. This article takes the Internet boundary firewall as an example to introduce how to quickly configure the cloud firewall.

<span id="a79a35b5"></span>
## Requirements


* You are familiar with the basics of the cloud firewall, including understanding [what functions the cloud firewall has](https://docs.byteplus.com/en/docs/cloud_firewall/What-is-BytePlus-Cloud-Firewall) and [what application scenarios the cloud firewall has](https://docs.byteplus.com/en/docs/cloud_firewall/Applicable-scenarios).

* You have purchased the version of the cloud firewall that suits you, taking into account the business protection needs, the functional features of different firewall versions, cost factors, and so on. For details on the features of different versions of the cloud firewall, please refer to [Version Features](https://docs.byteplus.com/en/docs/cloud_firewall/Version_Features).


<span id="807ad6d9"></span>
## Case Description

The business security protection requirements of a certain enterprise are described as follows:


* The public IP for providing external Web services is `14.100.100.175`, which needs to expose only port 443 to the outside, while all other ports are closed, reducing asset exposure to lower the risk of intrusion.

* To develop the business system `14.100.100.80`, external access to a certain data source is required, with the domain name `example.com`. Based on asset security considerations, only this asset is allowed to access `example.com`, and all other outbound connections are denied.


<span id="步骤一：开启云防火墙"></span>
## **Step 1: Enable the cloud firewall**


1. Log in to [the cloud firewall console](https://console.byteplus.com/firewall/overview), click **the firewall switch** in the left navigation bar.

2. On the **firewall switch** page, click **the internet boundary firewall**.

3. Manually turn on the firewall protection switch for public IP assets `14.100.100.175` and `14.100.100.80`.

4. (Optional) For information on other firewall application scenarios, please refer to the section below.

   
   |**Firewall Switch Type** |**Application scenarios** |
   |---|---|
   |**Internet Boundary Firewall** |Support redirecting the incoming and outgoing traffic of public EIP assets to the firewall for access control, reducing the exposure of public assets to lower intrusion risks, and effectively intercepting unauthorized access from the internal network to the public network. Enable the Internet boundary firewall, for more details, please refer to [Internet Boundary Firewall](https://docs.byteplus.com/en/docs/cloud_firewall/Enabling-Internet-firewall?type=preview). |
   |**VPC Border Firewall** |Supports redirecting traffic between private network VPC and between VPCs, as well as between VPC and on\-premises data centers (VPN or dedicated line), and between VPC and third\-party cloud (VPN or dedicated line gateway) to the firewall for access control, ensuring business isolation and effectively intercepting unauthorized access between internal networks. Enable VPC border firewall. For more details, please refer to [VPC Border Firewall Overview](https://docs.byteplus.com/en/docs/cloud_firewall/Enabling-VPC-firewall?type=preview) |
   |**NAT boundary firewall** |Supports routing traffic accessing the public network from NAT gateway private IP to the firewall for access control, effectively intercepting unauthorized access from the internal network to the public network. Enable NAT border firewall. For more details, please refer to [NAT Border Firewall](https://docs.byteplus.com/en/docs/cloud_firewall/Introduction_to_NAT_boundary_firewall) |
   


<span id="04068b50"></span>
## **Step 2: Configure access control policies** 

When your public IP asset connects to the internet boundary firewall, business traffic will be protected by the cloud firewall. Configure the corresponding access control policies based on business protection needs.


1. Log in to [the cloud firewall console](https://console.byteplus.com/firewall/overview), click **the firewall switch** in the left navigation bar.

2. In the left navigation bar, select **Access Control ＞ Internet Boundary**.

3. On the **Inbound Rules/Inbound Rules** tab, inbound/outbound rules can be added separately.

   * **Inbound Policy Configuration**: The cloud firewall allows all traffic by default when no policies are configured, so in this scenario, 2 access policies need to be configured.

      * One is a low priority blocking policy that blocks requests from all internet IPs to public IP business assets.

      * One is a high\-priority allow policy that allows requests from all internet IPs to access the `14.100.100.175` business asset on port 443.

   
   |**Rule priority** |**Access source type** |**Access source** |**Access destination type** |**Access destination** |**Protocol type** |**Destination port** |**Action** |**Entry into force** |**Description** |**Policy switch** |
   |---|---|---|---|---|---|---|---|---|---|---|
   |1 |IP |0.0.0.0/0 |IP |14.100.100.175 |TCP |443 |Allow |Always in effect |Allow access to Web port 443 |Keep it enabled |
   |2 |IP |0.0.0.0/0 |IP |0.0.0.0/0 |ANY |0/65535 |Block |Always effective |Full\-blocking fallback policy |Keep it enabled |
   

   * **Outbound Policy Configuration**: The cloud firewall allows all traffic by default when no policies are configured, so in this scenario, 2 access policies need to be configured.

      * One is a low priority blocking policy that blocks requests from public IP business assets to internet IPs.

      * One is a high\-priority allow policy that allows requests from `14.100.100.80` public IP assets to internet `example.com` domain.

   
   |**Rule priority** |**Access source type** |**Access source** |**Access purpose type** |**Access Purpose** |**Protocol type** |**Destination port** |**Action** |**Entry into force** |**Description** |**Policy switch** |
   |---|---|---|---|---|---|---|---|---|---|---|
   |1 |IP |14.100.100.80 |Domain name. |example.com |ANY |0/65535 |Allow |Always effective |Allow access to example.com domain |Keep it enabled |
   |2 |IP |0.0.0.0/0 |IP |0.0.0.0/0 |ANY |0/65535 |Block |Always effective |Full\-blocking fallback strategy |Keep it enabled |
   

4. (Optional) For more information on other firewall access control policy configurations, please refer to the section below.



|**Firewall type** |**Best practices** |
|---|---|
|**Internet border firewall** |* [Strategy that only allows public network traffic to access specified ports (incoming direction)](https://docs.byteplus.com/en/docs/cloud_firewall/Policy_allowing_public_traffic_to_access_specified_ports_inbound)<br><br>* [Strategy that only allows hosts to access specified domain names (outgoing direction)](https://docs.byteplus.com/en/docs/cloud_firewall/Policies_allowing_only_the_host_to_access_a_specified_domain)<br><br>* [Strategy that denies access from all international regions to hosts (incoming direction)](https://docs.byteplus.com/en/docs/cloud_firewall/Policy_to_reject_access_from_all_international_regions_to_the_host) |
|**VPC border firewall** |* [Access control for traffic between VPCs (automatic diversion configuration)](https://docs.byteplus.com/en/docs/cloud_firewall/Access_control_for_traffic_between_VPCs)<br><br>* [Traffic access control between VPC and dedicated line (automatic steering configuration)](https://docs.byteplus.com/en/docs/cloud_firewall/Access_control_for_traffic_between_a_VPC_and_an_instance)<br><br>* [Traffic access control between VPC and VPN (manual steering configuration)](https://docs.byteplus.com/en/docs/cloud_firewall/Access_control_for_traffic_between_a_VPC_and_a_VPN)<br><br>* [Traffic access control between VPN and dedicated line (manual steering configuration)](https://docs.byteplus.com/en/docs/cloud_firewall/Access_control_for_traffic_between_a_VPN_and_an_instance) |
|**NAT Boundary Firewall** |* [Private IP outbound](https://docs.byteplus.com/en/docs/6516/1338062)[ traffic access control](https://docs.byteplus.com/en/docs/cloud_firewall/Private_network_IP_outbound_traffic_access_control)<br><br>* [Private IP inbound traffic access control](https://docs.byteplus.com/en/docs/cloud_firewall/Access_control_for_private_network_IP_inbound_traffic) |


<span id="c4b6669a"></span>
## **Step 3: Log Management and Traffic Analysis**

Through traffic log management and traffic analysis, you can investigate the exposure of public assets, unauthorized external connections of assets, and unauthorized access between internal networks, and then adjust access control policies based on your business circumstances. This article takes the internet boundary firewall as an example to introduce asset exposure and active external connection governance.

<span id="779d1e91"></span>
### Log Management

Supports audit of access control logs and traffic session logs, and provides features such as retrieval analysis, monitoring alerts, and data visualization based on the BytePlus log service. By analyzing raw log data, one can investigate whether there are any abnormal accesses in the network and verify the effectiveness of policies. After configuring the policies, in addition to verifying effectiveness with ping/curl commands, you can also check the access control logs and traffic logs in the log management to see if the cloud firewall has corresponding log audits.


1. Log in to [the cloud firewall console](https://console.byteplus.com/firewall/overview), click **Log Management** in the left navigation bar.

2. In the basic mode page, you can see the access control logs and traffic session logs, which show the effective data of the corresponding policy.

3. In the advanced mode page, you can see visual charts through retrieval analysis. For example, you can search for outgoing traffic sizes in order to determine if there are any unexpected outgoing requests. If any abnormal accesses exist, you need to configure a blocklist in the access control policies.


<span id="57175b70"></span>
### Asset Exposure

The asset exposure analysis page of the cloud firewall provides an overview of incoming traffic to your assets, helping you identify risk ports exposed on the internet and consolidate unnecessary exposed ports. The cloud firewall detects successful external access to internal assets based on traffic session data, with the accessed asset ports being exposed on the internet. If there are unexpected IP or port information in the exposure surface analysis page, you need to configure the blocklist in the access control policy.

&nbsp;

<span id="1a7b5ad8"></span>
## **Step 4: Alert Notification** 

You can set up alert notifications to send alerts when resources such as cloud firewall traffic bandwidth, log storage, access control policy count, etc., are insufficient, so you can understand asset status and protect asset security.


1. Log in to the BytePlus console and configure internal messages, emails, and SMS notifications in [Message Center - Basic Acceptance Configuration - Security Messages - Alarm Notification](https://console.byteplus.com/message/setting).

2. Log in to [the Cloud Firewall Console](https://console.byteplus.com/firewall/overview), click on **System Management \- Alert Notification** in the left navigation bar.

3. Adjust the alert notification switch and notification thresholds according to business needs.
