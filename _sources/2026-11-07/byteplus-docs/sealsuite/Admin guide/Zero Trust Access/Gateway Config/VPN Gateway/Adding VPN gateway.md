---
title: "Adding VPN gateway"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-adding-a-vpn-gateway"
---

SealSuite's VPN is used to build a network environment for corporate remote work. You can deploy the SealSuite VPN component on a local server or virtual machine, connecting it to the SealSuite service to act as a SealSuite VPN gateway. Once the VPN gateway is active, employees can connect to the gateway via the client to access the corporate intranet for remote work. This article describes how to add a VPN gateway in the SealSuite Admin Console.

<span id="4ef15544"></span>
# Prerequisite

Before performing any operations in the Admin Console, please complete the following pre\-deployment checks and infrastructure preparations.

<span id="510d027a"></span>
## Pre\-Deployment Checklist


1. **Check the Number of Licensed Gateways**


The number of VPN gateways you can add is directly related to the quantity you purchased with your SealSuite subscription. For example, if you purchased 1 VPN gateway, you can only add 1 VPN gateway in the Admin Console. Before planning to deploy multiple gateways, ensure your subscription includes a sufficient number of gateway licenses.


2. **Choose a Dedicated Server Environment**


Please use a new, dedicated server to deploy the SealSuite VPN gateway. This helps to avoid conflicts with other running application services that could cause unexpected network forwarding issues.

<span id="a7cec72a"></span>
## Server Resource Requirements


|**Operating System** |**Minimum Configuration** |**Maximum Concurrency** |
|---|---|---|
|CentOS 7, Debian 9, or higher is recommended. |4\-Core CPU, 4 GB RAM |1000 |


The table above shows the reference configuration for a single VPN gateway. Concurrency refers to the number of online users the gateway can support simultaneously. If you anticipate more than 1000 concurrent users, you will need to plan and deploy multiple VPN gateways.

<span id="779320c7"></span>
## **Network Environment Requirements**


* **IP Address Planning**

   
   |**Server** |**IP Type** |**Example IP Address** |**Quantity** |**Purpose** |
   |---|---|---|---|---|
   |VPN Server |Public IP (or NAT mapping) |201.23.10.2 |N (Based on the number of gateways in your order) |Fixed public IP address. |
   ||Internal IP |192.168.1.2 |N (Based on the number of gateways in your order) |Fixed internal IP address. |
   

* **Required Network Port Openings**

   
   |**Direction** |**Destination IP** |**Destination Port** |**Protocol** |**Source IP** |**Notes** |
   |---|---|---|---|---|---|
   |Inbound |VPN Server's Public IP |443 (Default, can be changed) |TCP |Any |VPN control port, open to the internet. |
   |Inbound |VPN Server's Public IP |80 (Default, can be changed) |TCP, UDP |Any |VPN data port, open to the internet. |
   |Outbound |SealSuite Tenant Domain |443 |TCP |VPN Server |Allows the VPN gateway to initiate connections to the **SealSuit** cloud admin console to sync configurations and status. |
   


<span id="5487f129"></span>
# Add and Deploy the Gateway


1. Log in to the Admin Console.

2. In the left navigation bar, click **Zero Trust Access** \> **Gateway Config** \> **VPN Gateway**.

3. In the lower\-left corner of the **VPN Gateway** page, click **Create New Gateway**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f2e1d13570c433595ec496ca5cb6f75~tplv-goo7wpa0wc-image.image) </span>

4. In the **Configure new VPN gateway** pane, complete the following configurations.

   1. Fill in basic information and then click **Next Step**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7aa78e7ce15944b3a1859b6dec6f006d~tplv-goo7wpa0wc-image.image) </span>

      The description of each configuration item is as follows:

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Configuration items relating to IP addresses need to be filled in according to the actual system environment and configuration of the VPN gateway.      </div>
      

      
      |**Configuration Item** |**Description** |
      |---|---|
      |**Name** |Create a name both in English and Chinese for the VPN gateway. |
      |**DNS Server (Primary)**  |The primary DNS server's IP address assigned by the VPN gateway. In most cases, it is an internal DNS IP address. |
      |**DNS Server (Backup)**  |The alternate DNS server's IP address assigned by the VPN gateway. Please note that do not enter the same value as the primary DNS server IP address. |
      |**External Network Address** |The public IP address mapped by the VPN gateway. |
      |**Internal IP** |The internal IP address of the VPN gateway. |
      |**Control Port (TCP)**  |The port used for liveness probes and configuration synchronization. We recommend using Port 443. Also, you can modify the port. |
      |**Data Port (TCP/UDP)**  |The port used for transfering VPN data. We recommend using Port 80. Also, you can modify the port. |
      |**Enable Network Address Translation (NAT)**  |* **Enabled (Use Virtual IP pool)** : Use a virtual IP address pool, the IP addresses of which belong to the unsegmented portion of the corporate intranet.<br><br>* **Disabled (Use Internal IP pool)** : Use an internal virtual IP address pool, the IP addresses of which belong to the segmented portion of the corporate intranet, and all the IP addresses haven't been allocated yet. |
      |**IP Pool** |Specify the IP address pool by entering IP addresses in CIDR format, such as 10.8.8.0/24. The IP range must not conflict with the existing IP range of the corporate intranet. The maximum size of the IP pool is 1,024. If the number of IPs you need to configure exceeds 1,024, you must add additional VPN gateways to fulfill your needs. |
      |**Transport protocol** |The packet type used by the SealSuite client. You can choose either **Automatically choose TCP and UDP**, **TCP only** or **UDP only**. We recommend using the default setting, which is **Automatically choose TCP and UDP**, because UDP packet loss may occur on some networks. |
      |**Client side upload speed limit KB/s** |Specify the maximum uplink data rate limit for a single user in KB/s. The value `0` refers to no rate limiting. |
      |**Client side download speed limit KB/s** |Specify the maximum downlink data rate limit for a single user in KB/s. The value `0` refers to no rate limiting. |
      

   2. According to prompts on the **Deploy** page, deploy and install the VPN gateway on your designated server, and then click **Next Step**.

   3. Run a connectivity test to ensure the VPN Gateway can establish a stable connection with SealSuite's Portal, and then click **Complete**.

      You can view VPN gateways on the **VPN** **Management** page as soon as the configuration of your VPN gateways is completed. The deployment may take several minutes to complete.

5. Add access permissions.

   By default, the added VPN gateway is not automatically accessible to all users. To enable access, you have to configure users who have the permission to use the VPN gateway as well as the effective period. For more information about VPN access permissions, please refer to [Adding VPN access permissions](https://docs.byteplus.com/docs/sealsuite/docs-adding-vpn-access-permissions_2).


<span id="管理指定节点"></span>
# Related operations


* SealSuite VPN gateways support Full Tunnel Mode and Split Tunnel Mode. For more information about the network modes and configuration instructions, please refer to [Setting network mode for VPN gateways](https://docs.byteplus.com/docs/sealsuite/docs-setting-network-mode-for-vpn-gateways_1).

* You can create a user group for each VPN gateway. Only users within the designated user group can view and use the VPN gateway. For more information about user group management, please refer to [Configuring user groups for VPN gateways](https://docs.byteplus.com/docs/sealsuite/docs-configuring-user-groups-for-vpn-gateways).

* You can create access control rules for each VPN gateway to manage the network resources available to users. For more information about how to create access control rules, please refer to [Managing access control rules](https://docs.byteplus.com/docs/sealsuite/docs-managing-access-control-rules_2).

* You can manage basic information of VPN gateways with SealSuite. For more information, please refer to [Viewing or editing a VPN gateway](https://docs.byteplus.com/docs/sealsuite/docs-viewing-or-editing-a-vpn-gateway).
