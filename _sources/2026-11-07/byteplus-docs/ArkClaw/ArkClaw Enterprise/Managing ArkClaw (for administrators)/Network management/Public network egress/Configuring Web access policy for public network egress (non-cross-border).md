---
title: "Configuring Web access policy for public network egress (non-cross-border)"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring-Web-access-policy-for-public-private-network-egress-non-cross-border"
---

You can configure Web Access Policy to finely control access requests to public network domains, enforcing precise access control and egress assignment.

<span id="dYNLYzDH"></span>
## Before you begin

Public Network Egress must be [enabled](https://docs.byteplus.com/en/docs/ArkClaw/Enabling_or_disabling_access_log_for_public_network_egress).

<span id="2ReDK1Nh"></span>
## Instructions


* Web access policies consist of managed rules​ and custom rules, both of which count toward your [Web access policy quota](https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_Network_Configuration_overview#x9vYT0lB).

   * Managed rule: System\-predefined public access rules to **allow** ArkClaw cloud services to access the public network, ensuring normal cloud service operation. Managed rules only support addition and deletion. We recommend assigning them a higher priority.

   * Custom rules: User\-defined public access rules to **allow** or **block** public network access from custom sources.

* After Web access policy is enabled, the system automatically sets a default access rule​ with the lowest priority​ and an action of "Allow". Any traffic not matching any other rule will be handled by this default rule.

* To configure cross\-border acceleration rules, see [Configuring cross-border acceleration policy](https://docs.byteplus.com/en/docs/ArkClaw/Configuring-cross-border-acceleration-policy-new-version).


<span id="SKy8dXEC"></span>
## Enable or disable Web access policy


1. Log in to the [ArkClaw Enterprise Edition console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Select the "Space Egress" tab.

4. In the "Public network egress" section, click the "Security controls \> Web access policy" section.

5. Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b4801ed68f363d255f8acaecb67192fa.png) </span>icon to the right of Policy ID.

6. In the pop\-up dialog box, select to enable or disable Web access policy.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After the Web access policy is disabled, all rules no longer take effect, but the configuration is retained.   </div>
   

7. (Optional) Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b4801ed68f363d255f8acaecb67192fa.png) </span>icon to the right of the listening port. Editing port is supported. Up to 5 ports can be configured.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After configuring, modification is supported only when the Web access policy is disabled.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Default listening ports are <strong>80</strong> and <strong>443</strong>. The access policy applies to all TCP traffic on the listening port.   </div>
   


<span id="ryIXvrgS"></span>
## Manage a managed Web access rule


<Tabs>
<Tab zoneid="sj2uskbxie" title="Add managed access rule">
<TabTitle>Add managed access rule</TabTitle>

1. Log in to the[ ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Select the "Space Egress" tab.

4. In the "Public network egress" section, click the "Security controls \> Web access policy" section.

5. Click "Add Rule".

6. Set the priority for target service rules in the "Managed rule" tab.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Priority values must be unique across all rules.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">We recommend assigning higher priority​ (lower numeric value) to managed rules than to custom rules.   </div>
   

7. Click "Add rule" to complete this action.


</Tab>
<Tab zoneid="TZkSWrFGIC" title="Delete managed access rule">
<TabTitle>Delete managed access rule</TabTitle>

Deleting a managed access rule may affect normal operation of the related ArkClaw cloud service. Proceed with caution.


1. Log in to the[ ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Select the "Space Egress" tab.

4. In the "Public network egress" section, click the "Security controls \> Web access policy" section.

5. Click "Delete" to the right of the target managed rule.

6. Click "OK" to complete the action.


</Tab>
</Tabs>


<span id="27iE6AZo"></span>
## Manage a custom Web access rule


<Tabs>
<Tab zoneid="cYvXXQDYey" title="Add custom access rule">
<TabTitle>Add custom access rule</TabTitle>

1. Log in to the [ArkClaw Enterprise Edition console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Select the "Space Egress" tab.

4. In the "Public network egress" section, click the "Security controls \> Web access policy" section.

5. Click "Add Rule".

6. Click the “Custom rule” tab and configure the custom rule based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Name |The name for the custom access rule. |Access_page_123.cn |
   |Priority |Priorities of all rules must be unique​ and cannot be modified​ after creation. Plan your rules carefully.<br><br>Valid range: 1\-20000 (1 is the highest priority). |1 |
   |Action |Select **Block** or **Allow** for the access request. |Allow |
   |Egress region |Configure this parameter only when the action is set to "Allow". For a non\-cross\-border scenario, select **China Mainland**. |China Mainland |
   |Source |The request source to which the access rule applies. Up to 100 custom sources can be added. |\- |
   |Destination |Select the destination domain name for the access request. Up to 500 custom destination domains are supported. |\*.123.cn |
   

7. Click "OK" to complete the action.


</Tab>
<Tab zoneid="nziBdrP95J" title="Edit custom access rule">
<TabTitle>Edit custom access rule</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The system\-default access rule cannot be edited.</div>



1. Log in to the [ArkClaw Enterprise Edition console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Select the "Space Egress" tab.

4. In the "Public network egress" section, click the "Security controls \> Web access policy" section.

5. Click "Edit" to the right of the target rule.

6. Modify the rule configuration based on the parameters for creating a Web access rule.

7. Click "OK" to complete the action.


</Tab>
<Tab zoneid="F9sBrlHvXj" title="Delete custom access rule">
<TabTitle>Delete custom access rule</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The system\-default access rule cannot be deleted.</div>



1. Log in to the [ArkClaw Enterprise Edition console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Select the "Space Egress" tab.

4. In the "Public network egress" section, click the "Security controls \> Web access policy" section.

5. Click "Delete" to the right of the target rule.

6. Click "OK" to complete the action.


</Tab>
</Tabs>


<span id="D6nqYiOq"></span>
## Appendix

Some ArkClaw cloud services require public network access during operation. You need to add **managed rules** to ensure normal access. The table below lists the domains that must be allowed for each cloud service to function properly.


|Cloud service name |Access domain |
|---|---|
|Model gateway |ALL |
|ClawSentry |* clawsentry\-center\-ipv4.access.clawsentry.ai<br><br>* clawsentry\-sdk\-access\-cn\-hongkong.access.clawsentry.ai |
|Knowledge Center |knowledge\-center.aisearch.bytepluses.com |
|Skill Center |skills.bytepluses.com |
|Enterprise Identity Management |* auth.id.ap\-southeast\-1.bytepluses.com<br><br>* \*.userpool.auth.id.ap\-southeast\-1.bytepluses.com<br><br>* agent\-identity\-bp\-release.tos\-ap\-southeast\-1.volces.com<br><br>* auth.id.cn\-hongkong.bytepluses.com<br><br>* \*.userpool.auth.id.cn\-hongkong.bytepluses.com<br><br>* agent\-identity\-release\-hk.tos\-cn\-hongkong.volces.com |
