---
title: "Configuring network access policy for public network egress"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring_network_access_policy_for_public_network_egress"
---

Network Access Policy​ controls public network traffic. Based on the policies you configure, the system will block​ or allow​ traffic, providing fine\-grained access control and security protection. Once enabled, the policy takes effect immediately. The system automatically configures a default rule​ with the lowest priority​ and an action of "Allow", which permits all traffic. You can then add custom rules with the action "Block"​ to manage access for specific traffic.

<span id="T5NgDRDG"></span>
## Before you begin

[Public Network Egress](https://www.volcengine.com/docs/87732/2277042) must be enabled.

<span id="H5rLDkO3"></span>
## Enable or disable network access policy


1. Log in to the [ArkClaw Enterprise Edition console](https://console.volcengine.com/arkclaw/enterprise)[ArkClaw Terminal](https://console.volcengine.com/arkclaw/enterprise/omni).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Select the "Space Egress" tab.

4. In the "Public network egress" section, click the "Security controls \> Network access policy" section.

5. Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b4801ed68f363d255f8acaecb67192fa.png) </span>icon to the right of Policy ID.

6. In the pop\-up dialog box, select to enable or disable network access policy.

7. Click "OK" to complete the action.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After the network access policy is disabled, all rules no longer take effect, but the configuration is retained.   </div>
   

<span id="cpmzjTay"></span>
## Manage network access policy


<Tabs>
<Tab zoneid="Ux1rR1By" title="Add network access rule">
<TabTitle>Add network access rule</TabTitle>

1. Log in to the [ArkClaw Enterprise Edition console](https://console.volcengine.com/arkclaw/enterprise)[ArkClaw Terminal](https://console.volcengine.com/arkclaw/enterprise/omni).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Select the "Space Egress" tab.

4. In the "Public network egress" section, click the "Security controls \> Network access policy" section.

5. Click "Add Rule", and configure the network access rule based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Rule name |The rule of the network access policy. |Deny_access_123.cn |
   |Priority |Priorities of all rules must be unique​ and cannot be modified​ after creation. Plan your rules carefully.<br><br>Valid range: 1–10000 (1 is the highest priority). |2 |
   |Action |Select **Block** or **Allow** for the traffic. |Block |
   |Protocol |Select the transport protocol that the network access rule applies to. "ALL"​ applies the rule to all protocol types. |ALL |
   |Source type |Select the type of traffic source that the network access rule applies to. |Claw instance |
   |Source instance |Select the ID of the source instance. Up to 100 IDs are supported. |claw\-19dfang3\*\*\* |
   |Destination IP |The destination IP address​ that the traffic is attempting to access. IPv4 address only. Up to 20 IPs are supported. |134.XX.XX.8 |
   |Destination port |The destination port​ that the traffic is attempting to access. Up to 20 ports are supported. |80 |
   

6. Click "OK" to complete the action.


</Tab>
<Tab zoneid="3vIKZ5EH" title="Edit network access rule">
<TabTitle>Edit network access rule</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The system\-default access rule cannot be edited.</div>



1. Log in to the [ArkClaw Enterprise Edition console](https://console.volcengine.com/arkclaw/enterprise)[ArkClaw Terminal](https://console.volcengine.com/arkclaw/enterprise/omni).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Select the "Space Egress" tab.

4. In the "Public network egress" section, click the "Security controls \> Network access policy" section.

5. Click "Edit" to the right of the target rule.

6. Modify the rule configuration based on the parameters for creating a network access rule.

7. Click "OK" to complete the action.


</Tab>
<Tab zoneid="hYTzofda" title="Delete network access rule">
<TabTitle>Delete network access rule</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The system\-default access rule cannot be deleted.</div>



1. Log in to the [ArkClaw Enterprise Edition console](https://console.volcengine.com/arkclaw/enterprise)[ArkClaw Terminal](https://console.volcengine.com/arkclaw/enterprise/omni).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Select the "Space Egress" tab.

4. In the "Public network egress" section, click the "Security controls \> Network access policy" section.

5. Click "Delete" to the right of the target rule.

6. Click "OK" to complete the action.


</Tab>
</Tabs>
