---
title: "Create a custom rule group"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/Create_a_custom_rule_group"
---

To efficiently manage IP assets that share the same protection requirements, you can create custom rule groups. This guide provides step\-by\-step instructions on how to create a new rule group, which allows for centralized management and ensures your different assets receive more targeted security protection.

<span id="e0f15696"></span>
## Notifications


* Each instance supports a maximum of 50 custom rule groups.

* When a custom rule group is deleted, the rules within that group are also deleted. The protected IPs associated with the rule group will be added to the default rule group.


<span id="e8788f4c"></span>
## Prerequisites

Ensure that you have configured fewer than 50 custom rule groups.

<span id="870f321a"></span>
## Steps


1. Log in to [Cloud DDoS Protection Console](https://console.byteplus.com/ddos-protection/).

2. On the left side of the page, select **Cloud DDoS Protection \> Protection policy**.

3. Click **Create rule group**.

4. Enter the **Rule** ** group name** and **Description**.

   * **Rule group name**: Enter a name to identify the rule group.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Supports letters, digits, dashes (\-) and underscores (_).      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The name can be up to 20 characters long.      </div>
      

   * **Description**: Describe the purpose or scope of the rule group.

5. Complete the rule group creation.

   * Click **Create only** to complete the rule group creation. The rule group is created immediately, but it contains no rules and is not associated with any IP resources.

   * Click **Create and configure rules** to go to the rules configuration page for the new group, where you can configure different types of rules.


<span id="edb4b0f1"></span>
## Next steps


1. Configure rules within the rule group, including IP blocklists and allowlists, protocol blocking rules, port filtering rules, and regional blocking rules.

   Refer to the following instructions:

   * [Allow request traffic from the specified IP address](https://docs.byteplus.com/docs/byteplus-ddos-protection/Allow_request_traffic_from_the_specified_IP_address)

   * [Block traffic from the specified IP address](https://docs.byteplus.com/docs/byteplus-ddos-protection/Block_traffic_from_the_specified_IP_address)

   * [Block requests with specific protocol](https://docs.byteplus.com/docs/byteplus-ddos-protection/Block_requests_with_specific_protocol)

   * [Allow or block requests from/to specified ports](https://docs.byteplus.com/docs/byteplus-ddos-protection/Allow_or_block_requests_from_or_to_specified_ports)

   * [Block traffic from the specified regions](https://docs.byteplus.com/docs/byteplus-ddos-protection/Block_traffic_from_the_specified_regions)

2. Associate the rule group with the target IP; for specific operations, please refer to[ ](https://docs.byteplus.com/docs/byteplus-ddos-protection/Associate_protection_resources_with_custom_rule_groups).
