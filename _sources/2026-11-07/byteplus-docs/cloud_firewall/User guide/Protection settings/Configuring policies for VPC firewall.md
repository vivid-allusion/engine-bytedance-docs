---
title: "Configuring policies for VPC firewall"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Configuring_policies_for_VPC_firewall"
---

The VPC firewall can detect and control the traffic between two Virtual Private Clouds (VPCs). By default, it allows all traffic. You can configure it with access control policies to manage traffic between two VPCs, block suspicious or malicious traffic, and allow trusted traffic.

<span id="cce37fb9"></span>
## Prerequisites


* You have turned on the VPC firewall switch. For more information about how to turn on the VPC firewall switch, refer to [Enabling the VPC firewall](https://docs.byteplus.com/en/docs/99/1249438).

* The number of configured policies is less than the allowed quantity specified by the instance specifications. In other words, the policy balance is not 0.


<span id="543d6607"></span>
## Steps


1. Log in to the Cloud Firewall console.

2. On the left side of the page, click **Access control** \> **VPC boundary**.

3. Select the VPC firewall to which the policy belongs, click **Add policy**, then fill in the policy parameters.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e14fd0a988384303a192f1235de244fb~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Description** |
   |---|---|
   |Policy priority |Sets the priority of the policy. You can adjust it later by clicking the **Move** button of the policy in the access control policy list.<br><br><br>* **Highest priority**: Indicates the access control policy will have the highest priority and will be applied first.<br><br>* **Lowest priority**: Indicates the access control policy will have the lowest priority and will be applied last. |
   |Source IP type |You need to select the type of access source, and enter the corresponding access source address.<br><br><br>* If you select the **IP** type, you must enter an IP address or a CIDR block. For example, `180.184.1.1` or `180.184.0.0/16`. `0.0.0.0/0` indicates "all".<br><br>* If you select the **Address book** type, you must create an address book in advance. |
   |Source ||
   |Destination type |You need to select the type of access destination and enter the corresponding address of the destination.<br><br><br>* If you select the **IP** type, you must enter an IP address or a CIDR block. For example, `180.1.1.1` or `180.1.0.0/16`. `0.0.0.0/0` indicates "all".<br><br>* If you select the **Address book** type, you must create an address book in advance.<br><br>* If the **Domain name** type is selected, you must enter the destination domain. Can be a single domain (`example.com`), wildcard domain (`*.example.com`), and multi\-level domain (`example1.example2.com`).<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Do not include the protocol part such as HTTP (S)in the domain name.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Domain\-based access control policies rely on domain names extracted from the Host header in HTTP packets and the Server Name field in the Client Hello message of HTTPS packets for policy matching. If the data packets in your business traffic do not contain these two fields, the domain policy will not work.   </div><br>    |
   |Destination ||
   |Protocol |Sets the transport layer protocol type.<br><br><br>* Supports: **TCP**, **UDP**, **ICMP**, and **ANY**.<br><br>* If you are unsure which protocol to use, select **ANY**.<br><br>* Domain\-based access control policies are only applicable to **HTTP** and **HTTPS** protocols. Therefore, when the destination type is a domain, **TCP must be used**. |
   |Destination port type |Sets the destination port type and destination port.<br><br><br>* If you select the **Port** type, you must enter a port or port range, such as `22`, `80/88`, and `0/65535`.<br><br>* **Address book**: If you select the **Address book** type, you must create a port address book in advance.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">As domain\-based access control policies are only applicable to the HTTP and HTTPS protocols, ensure that the destination ports use either the HTTP or HTTPS protocol.</div><br> |
   |Destination port ||
   |Action |The actions to take when the policy is triggered. There are three types:<br><br><br>* Allow: Allows traffic that matches the policy and logs hit count and traffic but not access control activities.<br><br>* Block: Intercepts traffic that matches the policy and logs hit count and access control activities but not traffic.<br><br>* Observe: Allow traffic that matches the policy and logs hit count, access control activities, and traffic. |
   |Description |A description of the policy, such as its purpose and usage. Up to 100 characters. |
   |Policy on/off |A switch that can be used to enable or disable the policy. If you do not enable the policy during its creation, you can enable it later by using the switch in the policy list. |
   

4. Click **Add**.

   Once the policy is created, you can view its details and hit count, and edit or delete it from the address book list.
