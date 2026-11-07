---
title: "Policy allowing public traffic to access specified ports"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Policy_allowing_public_traffic_to_access_specified_ports_inbound"
---

This article describes how to configure inbound policy settings, allowing only business traffic on certain ports to be open to the internet.


---



<span id="deb908ca"></span>
# Example scenario

ECS (host) bound EIP is `180.100.1.1/32`, and it is necessary to set all public (`0.0.0.0/0`) traffic to only allow access to the host's TCP ports 80 and 443. When no policy is configured, the cloud firewall allows all traffic by default, so in this scenario, it is necessary to configure 2 access policies. One is a high\-priority allow policy, allowing all public traffic to access the host's ports 80 and 443; the other is a low\-priority deny policy, blocking all public traffic accessing all ports of the host.

<span id="f6144bef"></span>
# Steps


1. Log in to [Cloud Firewall Console](https://console.byteplus.com/firewall/overview).

2. **Add new port address book**:

   1. In the left navigation bar, select **Access Control \> Address Book Management.** 

   2. Click **Add Address Book,**  and configure the port address book for ports 80 and 443.



|**Configuration item** |**Configuration description** |**Configuration parameters** |
|---|---|---|
|**Address book <Data type\>**  |Select the type of address book, here select port address book. Configure the port address book for ports 80 and 443.<br><br><br>* **IP address book**: A single address book can add up to 2000 IP addresses.<br><br>* **Port address book**: A single address book can add up to 2000 port addresses. |Port address book |
|**Address book name** |Custom address book name. It is recommended to enter a name that makes it easy for you to effectively distinguish between different address books. |Web service port |
|**Port** |Input port. Separate multiple ports with half\-width commas (,). Enter ports 80 and 443 here. |80,443 |
|**Address book description** |Input the current address book content and usage scenarios. This helps you identify and apply the address book. |Web business ports, 80 and 443 |



3. **Add release policy**：

   1. In the left navigation bar, select **Access Control \> Internet Boundary**. On the **Inbound Rules** tab, click **Add.** 

   2. Add a high\-priority release policy to allow all public traffic accessing ports 80 and 443 of this host.



|**Configuration item** |**Configuration description** |**Configuration parameters** |
|---|---|---|
|**Rule priority** |Select the priority for this strategy, here choosing the highest priority. After configuration is complete, you can also click **Move** in the access control policy list to customize the priority of the policy.<br><br><br>* **Highest priority**: refers to the highest priority for the access control policy to take effect, making it effective first.<br><br>* **Lowest priority**: refers to the lowest priority for the access control policy to take effect, making it effective last. |Highest priority |
|**Access source type** |You need to select the source type and enter the source address according to the source type. Here, select the IP type and enter `0.0.0.0/0`, allowing all external source IPs to access `180.100.1.1/32` host.<br><br><br>* When selecting **IP** type, you need to enter an IP address or IP address range. For example, `180.184.1.1` or `180.184.0.0/16`, `0.0.0.0/0` represents all.<br><br>* When selecting **address book** type, you need to create the IP address book in advance.<br><br>* When selecting **data type**, you need to choose the area where the source address is located. Optional domestic areas or international areas. |IP |
|**Access source** ||0.0.0.0/0 |
|**Access purpose type** |You need to select an access purpose data type and enter the access purpose address according to the access purpose data type. Here, select the IP data type and enter `180.100.1.1/32` for all external access source IPs that can access the `180.100.1.1/32` host.<br><br><br>* When selecting **IP** data type, you need to enter an IP address or IP address range. Such as `180.184.1.1` or `180.184.0.0/16`, `0.0.0.0/0` means all.<br><br>* When selecting **address book** data type, you need to create an IP address book in advance. |IP |
|**Access purpose** ||180.100.1.1/32 |
|**Protocol type** |Transport layer protocol type, supports settings as: **TCP**, **UDP**, **ICMP**, **ANY**. If the specific protocol is uncertain, **ANY** can be chosen. Since the destination ports configured this time are 80 and 443, **TCP** or **ANY** can be selected. |TCP |
|**Destination port type** |Set the destination port type and destination port. This time, the selected address book needs to configure ports 80 and 443.<br><br><br>* When selecting **port** type, you need to enter the port or port range, such as 22, 80/88, 0/65535.<br><br>* **Address book**: When selecting **address book** type, you need to create the port address book in advance. |Address book |
|**Destination port** ||Web service port address book |
|**Action** |Set the traffic matching success conditions for release under this policy.<br><br><br>* **Release**: Release this traffic, access control logs will not be recorded, only traffic logs will be recorded.<br><br>* **Block**: Intercept this traffic and block logs will be recorded in the access control logs.<br><br>* **Observe**: Release this traffic. Block logs will be recorded in the access control logs. |Release |
|**Description** |Enter the current policy content and usage scenario. Facilitates your identification and application of the address book. |Web service 80 & 443 port release policy |
|**Policy switch** |Set the policy switch. If the policy was not enabled when you created the policy, you can enable the policy in the policy list. |Keep it enabled |



4. **Add block policy**：

   1. In the left navigation bar, select **Access Control \> Internet Boundary**. On the **Inbound Rules** tab, click **Add.** 

   2. Add a low\-priority block policy to block all public traffic accessing all ports of this host.

   
   |**Configuration items** |**Configuration parameter** |
   |---|---|
   |**Rule priority** |Lowest priority |
   |**Access source type** |IP |
   |**Access source** |0.0.0.0/0 |
   |**Access purpose data type** |IP |
   |**Access purpose** |180.100.1.1/32 |
   |**Protocol type** |ANY |
   |**Action** |Block |
   |**Description** |Block public network traffic access to all ports |
   |**Policy switch** |Keep it enabled |
