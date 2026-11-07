---
title: "Configure access control policies"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Configure_access_control_policies"
---

To manage and restrict traffic to your protected assets, you can configure access control policies in the LLM Application Firewall. This guide provides step\-by\-step instructions on how to create blocklists to deny access from specific IP addresses and allowlists to grant access to trusted IPs.

<span id="7a0ee19a"></span>
## Background information

The allowlist complements the blocklist and is used to grant access to specific IP addresses. However, allowed traffic will still be inspected by other protection policies. If the traffic does not meet the requirements of other protection policies, it may still be blocked.

Requests are blocked if and only if the source IP address matches the blocklist but not the allowlist. In all other cases, traffic is inspected by the configured LLM policies.


|Blocklist |Allowlist |Result |Note |
|---|---|---|---|
|Match |Match |Pass |Request traffic will be inspected by other protection policies. |
|Match |Mismatch |Block |Blocks the corresponding requests without further inspection by other protection policies. |
|Mismatch |Match |Pass |Request traffic will be inspected by other protection policies. |
|Mismatch |Mismatch |Pass |Request traffic will be inspected by other protection policies. |


<span id="3750eb8d"></span>
## Prerequisites

You have already integrated your services that require protection from the LLM Application Firewall. For integration instructions, see [Introduction to assets integration](https://docs.byteplus.com/docs/LLM-Application-Firewall/introduction_to_assets_integration).

<span id=".5pON5L2c5q2l6aqk"></span>
## Configure a blocklist

Add an IP address to the blocklist to block access from that IP. You can view access records in the attack log.


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. Select the instance's region in the top bar.

3. In the left navigation, select **Protection \> Access control \> Blocklist**.

4. Click **Add rule**, and configure the rule parameters.

   
   |**Parameters** |Description |**Configuration example** |
   |---|---|---|
   |Rule name |Enter the name of the access control policy.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Must start with a letter or a digit.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Only letters, numbers, periods, underscores, and hyphens are allowed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Length should be between 1 and 128 characters.</div><br> |Block_rule1 |
   |Asset |Select the assets or paths to match. If you select an asset, the rule applies to all of its configured paths. |asset1 |
   |IP address |Manually enter the IP addresses to be added to the blocklist. You can enter single IPv4 addresses or IPv4 address ranges. You can enter multiple addresses by using line breaks.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">Supports up to 100 entries.</div><br> |192.0.2.1 |
   |Rule switch |Enable or disable the current rule. |Enable |
   

5. Click **OK** to save the rule.


<span id="38c28e6a"></span>
## Configure an allowlist

Adding an IP address to the allowlist allows its requests to bypass the blocklist.


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. In the top bar, select the instance's region.

3. In the left navigation, select **Protection \> Access control \> Allowlist**.

4. Click **Add rule**, and configure rule parameters.

   
   |**Parameters** |Description |**Configuration example** |
   |---|---|---|
   |Rule name |Enter the name of the access control policy.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Must start with letters, or digits.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Only letters, digits, periods(.), underscores(_), and hyphens are allowed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Length should be between 1 and 128 characters.</div><br> | Allow_rule1 |
   |Asset |Select one or more assets that are protected by the firewall. |123test.com |
   |IP address |Manually enter the IP addresses that need to be added to the allowlist. You can enter single IPv4 addresses or IPv4 address ranges. You can enter multiple addresses by using line breaks.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">Supports up to 100 entries.</div><br> |192.0.2.1 |
   |Rule switch |Enable or disable the current rule. |Enable |
   

5. Click **OK** to save the rule.


&nbsp;


&nbsp;

&nbsp;
