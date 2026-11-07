---
title: "Configuring policies for internet firewall"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Configuring_policies_for_internet_firewall"
---

The internet firewall allows you to implement access control on the traffic between Elastic IP Address assets and the internet. Cloud Firewall allows all inbound and outbound traffic by default upon activation. You can configure access control policies in Cloud Firewall to restrict unauthorized communication between your assets and the internet.

<span id="c0f5fed1"></span>
## Background

Cloud Firewall internet access policies include outbound policies and inbound policies:


* **Inbound rules**: Control inbound traffic, which goes from the internet to your internal network.

* **Outbound rules**: Control outbound traffic, which goes from your internal network to the internet.


<span id="Prerequisites"></span>
## Prerequisites


* You have enabled the firewall for the relevant assets. For more information about how to enable the firewall for an asset, refer to [Enabling the internet firewall](https://docs.byteplus.com/en/docs/99/1249437).

* The number of your outbound and inbound policies has not exceeded the limit specified by the instance specifications. In other words, the available balance is not 0.


<span id="Inbound policies"></span>
## Configuring an inbound policy


1. Log in to the Cloud Firewall console.

2. On the left side of the page, click **Access control** \> **Internet boundary**.

3. Select **Inbound rules**, click **Add rules**, and then fill in the required parameters for the rule.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af2552655dcc4515b11a2a6d858389fd~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Description** |
   |---|---|
   |Rule priority |Sets the priority of the policy. You can adjust it later by clicking the **Move** button of the policy in the access control policy list.<br><br><br>* **Highest priority**: Indicates the access control policy will have the highest priority and will be applied first.<br><br>* **Lowest priority**: Indicates the access control policy will have the lowest priority and will be applied last. |
   |Source type |You need to select the type of access source, and enter the corresponding access source address.<br><br><br>* If you select the **IP** type, you must enter an IP address or a CIDR block. For example, `180.184.1.1` or `180.184.0.0/16`. `0.0.0.0/0` indicates "all".<br><br>* If you select the **Address book** type, you must create an address book in advance.<br><br>* If you select the **Region** type, you must select the region where the source address is located. You can select a region that is inside or outside China. |
   |Source ||
   |Destination type |You need to select the type of access destination and enter the corresponding address of the destination.<br><br><br>* If you select the **IP** type, you must enter an IP address or a CIDR block. For example, `180.1.1.1` or `180.1.0.0/16`. `0.0.0.0/0` indicates "all".<br><br>* If you select the **Address book** type, you must create an address book in advance. |
   |Destination ||
   |Protocol |Sets the transport layer protocol type.<br><br><br>* Supports: **TCP**, **UDP**, **ICMP**, and **ANY**.<br><br>* If you are unsure which protocol to use, select **ANY**. |
   |Destination port type |Sets the destination port type and destination port.<br><br><br>* If you select the **Port** type, you must enter a port or port range, such as `22`, `80/88`, and `0/65535`.<br><br>* **Address book**: If you select the **Address book** type, you must create a port address book in advance. |
   |Destination port ||
   |Actions |The actions to take when the policy is triggered. There are three types:<br><br><br>* Allow: Allows traffic that matches the policy and logs hit count and traffic but not access control activities.<br><br>* Block: Intercepts traffic that matches the policy and logs hit count and access control activities but not traffic.<br><br>* Observe: Allow traffic that matches the policy and logs hit count, access control activities, and traffic. |
   |Description |A description of the policy, such as its purpose and usage. Up to 100 characters. |
   |Policy on/off |A switch that can be used to enable or disable the policy. If you do not enable the policy during its creation, you can enable it later by using the switch in the policy list. |
   

4. Click **Add**.

   Once the inbound policy is created, you can view its details and hit count, and edit or delete it from the address book list.


<span id="Outbound policies"></span>
## Configuring an outbound policy


1. Log in to the Cloud Firewall console.

2. On the left side of the page, click **Access control** \> **Internet boundary**.

3. Select **Outbound rules**, click **Add rules**, fill in the policy parameters.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ae80375f1c24e29b90b63e0b7af2541~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Description** |
   |---|---|
   |Rule priority |Sets the priority of the policy. You can adjust it later by clicking the **Move** button of the policy in the access control policy list.<br><br><br>* **Highest priority**: Indicates the access control policy will have the highest priority and will be applied first.<br><br>* **Lowest priority**: Indicates the access control policy will have the lowest priority and will be applied last. |
   |Source type |You need to select the type of access source, and enter the corresponding access source address.<br><br><br>* If you select the **IP** type, you must enter an IP address or a CIDR block. For example, `180.184.1.1` or `180.184.0.0/16`. `0.0.0.0/0` indicates "all".<br><br>* If you select the **Address book** type, you must create an address book in advance. |
   |Source ||
   |Destination type |You need to select the type of access destination and enter the corresponding address of the destination.<br><br><br>* If you select the **IP** type, you must enter an IP address or a CIDR block. For example, `180.1.1.1` or `180.1.0.0/16`. `0.0.0.0/0` indicates "all".<br><br>* If you select the **Address book** type, you must create an address book in advance.<br><br>* If the \*\*Domain name \*\*type is selected, you must enter the destination domain. Can be a single domain (`example.com`), wildcard domain (`*.example.com`), and multi\-level domain (`example1.example2.com`).<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Do not include the protocol part such as HTTP (S)in the domain name.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Domain\-based access control policies rely on domain names extracted from the Host header in HTTP packets and the Server Name field in the Client Hello message of HTTPS packets for policy matching. If the data packets in your business traffic do not contain these two fields, the domain policy will not work.   </div><br>   <br><br>* If you select the **Region** type, you must select the region where the source address is located. You can select a region that is inside or outside China. |
   |Destination ||
   |Protocol |Sets the transport layer protocol type.<br><br><br>* Supports: **TCP**, **UDP**, **ICMP**, and **ANY**.<br><br>* If you are unsure which protocol to use, select **ANY**.<br><br>* Domain\-based access control policies are only applicable to **HTTP** and **HTTPS** protocols. Therefore, when the destination type is a domain, **TCP must be used**. |
   |Destination port type |Sets the destination port type and destination port.<br><br><br>* If you select the **Port** type, you must enter a port or port range, such as `22`, `80/88`, and `0/65535`.<br><br>* **Address book**: If you select the **Address book** type, you must create a port address book in advance.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">As domain\-based access control policies are only applicable to the HTTP and HTTPS protocols, ensure that the destination ports use either the HTTP or HTTPS protocol.</div><br> |
   |Destination port ||
   |Actions |The actions to take when the policy is triggered. There are three types:<br><br><br>* Allow: Allows traffic that matches the policy and logs hit count and traffic but not access control activities.<br><br>* Block: Intercepts traffic that matches the policy and logs hit count and access control activities but not traffic.<br><br>* Observe: Allow traffic that matches the policy and logs hit count, access control activities, and traffic. |
   |Description |A description of the policy, such as its purpose and usage. Up to 100 characters. |
   |Policy on/off |A switch that can be used to enable or disable the policy. If you do not enable the policy during its creation, you can enable it later by using the switch in the policy list. |
   

4. Click **Add**.

   Once the outbound policy is created, you can view its details and hit count, and edit or delete it from the address book list.
