---
title: "Configuring Web access policy for private network egress"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring-a-private-egress-web-access-policy"
---

<span id="hnZYqS8D"></span>
## Scenarios

Web access policy controls Layer\-7 private network traffic from Claw instances to your enterprise services. You can configure the Web access policy for private network egress to allow or deny Claw instances access to specific target domains.

<span id="gBHvailX"></span>
## Before you begin

Private Network Egress must be enabled. For procedure, see [Configuring private network egress](https://docs.byteplus.com/en/docs/ArkClaw/Enabling-or-disabling-the-private-egress-Old-version).

<span id="3b5T1mvp"></span>
## Instructions


* Web access policies consist of managed rules​ and custom rules, both of which count toward your [Web access policy quota](https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_Network_Configuration_overview).

   * Managed rule: System\-predefined private access rules to **allow** ArkClaw cloud services to access the private network, ensuring normal cloud service operation. Managed rules only support addition and deletion. We recommend assigning them a higher priority.

   * Custom rules: User\-defined private access rules to **allow** or **block** private network access from custom sources.

* After Web access policy is enabled, the system automatically sets a default access rule​ with the lowest priority​ and an action of "Allow". Any traffic not matching any other rule will be handled by this default rule.


<span id="CH67BteF"></span>
### Enable or disable Web access policy


1. Log in to the[ ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Click the "Space Egress \> Private network egress" tab.

4. Click the "Web access policy" tab.

   * Enable: Click the edit icon next to Policy ID, then click "OK" to enable Web access policy.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If no Policy ID is visible, please submit an <a href="https://console.byteplus.com/arkclaw/enterprise/region:arkclaw/enterprise+cn-beijing/issue-feedback?projectName=default&spaceId=csi-yehwr79wjkjjbs00n282">issue feedback</a>.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Once the Web access policy is enabled, the system creates a default rule​ that allows all traffic. This default rule has the lowest priority​ and cannot be deleted.      </div>
      

   * Disable: Click the edit icon next to Policy ID, then click "OK" to disable Web access policy.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">After the Web access policy is disabled, all configured rules will be suspended. Layer 7 traffic will be fully allowed. Existing rules are not deleted. They will take effect again when the policy is re\-enabled.      </div>
      

      <span id="LrJSEG4l"></span>
      ## Manage a managed Web access rule


<Tabs>
<Tab zoneid="BkPDX0Yxfl" title="Add managed access rule">
<TabTitle>Add managed access rule</TabTitle>

1. Log in to the[ ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Select the "Space Egress" tab.

4. In the "Private network egress" tab, click the "Security controls \> Web access policy" section.

5. Click "Add Rule".

6. Set the priority for target service rules in the "Managed rule" tab.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Priority values must be unique across all rules.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">We recommend assigning higher priority​ (lower numeric value) to managed rules than to custom rules.   </div>
   

7. Click "Add Rule" to complete this action.


</Tab>
<Tab zoneid="S5WMmTAncB" title="Delete managed access rule">
<TabTitle>Delete managed access rule</TabTitle>

Deleting a managed access rule may affect normal operation of the related ArkClaw cloud service. Proceed with caution.


1. Log in to the[ ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Select the "Space Egress" tab.

4. In the "Private network egress" tab, click the "Security controls \> Web access policy" section.

5. Click "Delete" to the right of the target managed rule.

6. Click "OK" to complete the action.


</Tab>
</Tabs>


<span id="RUT6hYLz"></span>
### Configure a Web access rule


<Tabs>
<Tab zoneid="bkvGth30" title="Add Web access rule">
<TabTitle>Add Web access rule</TabTitle>

1. Log in to the[ ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Select the "Space Egress \> Private network egress" tab.

4. On the "Web access policy" tab, click "Add Rule".

5. Configure parameters based on the table below.

   
   |Parameter |Description |
   |---|---|
   |**Basic information** ||
   |Rule name |Enter the name for the rule. |
   |Priority |Enter the priority for the rule. Valid range: 1\-10000. A smaller number indicates higher priority. |
   |Rule description |Enter the description for the rule. |
   |**Match condition** ||
   |Source type |Select the source type. Supports "Claw" and "All". |
   |Source |Configure the access source.<br><br><br>* If the source type is "Claw", select one or more specific Claw instances.<br><br>* If the source type is "All", select All, representing all Claw instances. |
   |Access destination |Configure the access destination. Choose "All"​ or "Custom".<br><br><br>* All: Matches all domains.<br><br>* Custom: Supports exact domains (e.g., a.example.com) and leftmost wildcard domains (e.g., \*.example.com).<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The wildcard \*can only appear at the far left of a domain. It replaces exactly one label. For example, \*.example.com matches a.example.com and b.example.com. It does not match example.com itself, nor multi\-level subdomains like a.b.example.com. Wildcards in the middle or right (e.g., example.\*.com) are not supported, as well as partial wildcards (e.g., \*a.example.com).   </div><br>   <br><br> |
   |**Match action** ||
   |Action |Select the action to perform on the target domain.<br><br><br>* Allow: Permit the traffic flow.<br><br>* Block: Deny the traffic flow. |
   

6. Click "OK" to complete the action.


</Tab>
<Tab zoneid="fwKH2QNq" title="Edit Web access rule">
<TabTitle>Edit Web access rule</TabTitle>

Default rules cannot be modified.


1. Log in to the[ ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Select the "Space Egress \> Private network egress" tab.

4. On the "Web access policy" tab, click "Edit" to the right of the target rule.

5. Modify parameters then click "OK" to complete the action.


</Tab>
<Tab zoneid="O2WoNmm2" title="Delete Web access rule">
<TabTitle>Delete Web access rule</TabTitle>

The default rule cannot be manually deleted. The rule is automatically removed when the private network egress is disabled.


1. Log in to the[ ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Select the "Space Egress \> Private network egress" tab.

4. On the "Web access policy" tab, click "Delete" to the right of the target rule.

5. Click "Delete" to complete the action.


</Tab>
</Tabs>


<span id="NrXlnUR2"></span>
## Appendix

Some ArkClaw cloud services require private network access during operation. You need to add **managed rules** to ensure normal private access. The table below lists the domains that must be allowed for each cloud service to function properly.


|Cloud service name |Access domain |
|---|---|
|Model gateway |ALL |
|ClawSentry |* center\-ipv4.access.clawsentry.cn<br><br>* sdk\-access\-cn\-shanghai.access.clawsentry.cn<br><br>* \*.volceapi.com |
|Knowledge Center |knowledge\-center.aisearch.volces.com |
|Skill Center |skills.bytepluses.com |
