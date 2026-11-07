---
title: "Associate protection resources with custom rule groups"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/Associate_protection_resources_with_custom_rule_groups"
---

Associating Elastic IPs (EIPs) with a custom rule group allows you to apply a specific set of DDoS protection policies to them. This provides granular control and simplifies policy management, enabling you to apply tailored protection strategies to different groups of resources, such as applying stricter rules to critical applications. This document guides you through associating EIPs with custom rule groups for both new and existing protection resources.

<span id="0643c8d1"></span>
## Important notes


* If a resource is added to Cloud DDoS Protection without specifying a rule group, the system will automatically associate it with the default rule group.

* If the target EIP is already associated with other rule groups (including the default rule group and the expert rule group), you can change its rule group directly from the list of protected resources.


<span id="8fb8f6a4"></span>
## Scenario 1: Associate rule groups when adding protection resources

When adding resources to Cloud DDoS Protection, you can associate the resources with existing rule groups. If the current rule group list does not contain the rule group you need, you can also create a new custom rule group.

<span id="40d24291"></span>
### Prerequisites

You have purchased and activated the Cloud DDoS Protection service. For instructions, refer to [Step 1: Create a Cloud DDoS Protection instance](https://docs.byteplus.com/docs/byteplus-ddos-protection/Get_started_with_Cloud_DDoS_Protection#f147827f).

<span id="07e2c2b8"></span>
### Steps


1. Log in to the [Cloud DDoS Protection Console](https://console.byteplus.com/ddos-protection/).

2. On the left side of the page, select **Cloud DDoS Protection \> Protected resources**.

3. Click **Add EIP** and select the EIPs you want to add.

4. Select the EIP that you want to add to the list of protected resources.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If there is no available EIP, please go to the <a href="https://console.volcengine.com/eip/region:eip+cn-beijing/eips/create">EIP Product Console</a> to purchase one.   </div>
   

5. Set up protection rules for the EIPs.

   * **Select the default rule group**: Add the currently selected EIP to the default rule group. Click **View** to see all EIPs associated with this rule group.

   * **Create a new rule group**: Click **Create rule group** to create a custom rule group. After creation, the currently selected EIP will be added to this rule group.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/514e25ce98f84a76abbc3aaebf8bcfeb) </span>

6. Click **Save**.


<span id="4ef26fc9"></span>
## Scenario 2: Associate existing resources with rule groups

If your EIP has been added to a Cloud DDoS Protection instance, you can create a custom rule group and associate these EIPs with that group.

<span id="e222bc5a"></span>
### Prerequisites

The target EIP has been added to the Cloud DDoS Protection instance and is not associated with other rule groups.

<span id="8e2c3100"></span>
### Steps


1. Log in to [Cloud DDoS Protection Console](https://console.byteplus.com/ddos-protection/).

2. On the left side of the page, select **Cloud DDoS Protection \> Protection policy**.

3. Click **Create rule group**.

4. Enter a **Rule** ** group name** and **Description**.

5. Click **Create only**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2128d3b7cad94cb59958b870f96785f7) </span>

   After creation, the new rule group appears in the protection policy list. You can add protection rules to the rule group at any time.

6. Click **Associate IP** in the Actions column for the rule group.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a88c4e8df2434425b1a2bc2e25fb7967) </span>

7. Click **Associate IP**, and select the EIP to associate with the rule group from the list of available EIPs.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/e93803b613704d4ba29533c60544c2bc) </span>

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you cannot find the target EIP, it might already be associated with the default or expert rule group. You can switch the EIP's rule group directly from the protected resources list.   </div>
   

8. Click **OK**.


<span id="75276bad"></span>
## What to do next

After associating the protected resources with the custom rule group, you can update the protection rules within the rule group at any time. For instructions on configuring protection rules, see:


* [Allow request traffic from the specified IP address](https://docs.byteplus.com/docs/byteplus-ddos-protection/Allow_request_traffic_from_the_specified_IP_address)

* [Block traffic from the specified IP address](https://docs.byteplus.com/docs/byteplus-ddos-protection/Block_traffic_from_the_specified_IP_address)

* [Block requests with specific protocol](https://docs.byteplus.com/docs/byteplus-ddos-protection/Block_requests_with_specific_protocol)

* [Allow or block requests from/to specified ports](https://docs.byteplus.com/docs/byteplus-ddos-protection/Allow_or_block_requests_from_or_to_specified_ports)

* [Block traffic from the specified regions](https://docs.byteplus.com/docs/byteplus-ddos-protection/Block_traffic_from_the_specified_regions)
