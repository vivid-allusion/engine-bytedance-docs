---
title: "Configuring DNS access policy"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring-DNS-access-policy"
---

<span id="FZ6OwE88"></span>
## Scenarios

DNS Access Policy for Private Network Egress blocks DNS resolution for specified domains from Claw instances. You can enable the control by configuring this policy for the private network egress.

<span id="LFAxiKk7"></span>
## Before you begin

The private network egress is enabled with DNS resolution configured. For procedure, see [Enabling private network egress (new version)](https://docs.byteplus.com/en/docs/ArkClaw/Enabling-or-disabling-the-private-egress-New-version) and [Configuring DNS custom resolution (new version)](https://docs.byteplus.com/en/docs/ArkClaw/Configuring-the-private-egress-domain-resolution-New-version).

<span id="ECUjIAgv"></span>
### Enable or disable DNS access policy


1. Log in to the[ ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Click the "Space Egress \> Private network egress" tab.

4. Click the "DNS access policy" tab.

   * Enable: Click the edit icon next to Policy ID, then click "OK" to enable DNS access policy.

   * Disable: Click the edit icon next to Policy ID, then click "OK" to disable DNS access policy.


<span id="L0BWIXlj"></span>
### Configure a DNS access rule


<Tabs>
<Tab zoneid="HpUAmp7s" title="Add DNS access rule">
<TabTitle>Add DNS access rule</TabTitle>

1. Log in to the[ ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Click the "Space Egress \> Private network egress" tab.

4. On the "DNS access policy" tab, click "Add Rule".

5. Configure parameters based on the table below.

   
   |Parameter |Description |
   |---|---|
   |Rule name |Enter the name for the rule. |
   |Rule description |Enter the description for the rule. |
   |Domain to block |Enter the domains to block from Claw instances.<br><br><br>* Supports exact domains (e.g., a.example.com) and leftmost wildcard domains (e.g., \*.example.com).<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The wildcard \*can only appear at the far left of a domain. It replaces exactly one label. For example, \*.example.com matches a.example.com and b.example.com. It does not match example.com itself, nor multi\-level subdomains like a.b.example.com. Wildcards in the middle or right (e.g., example.\*.com) are not supported, as well as partial wildcards (e.g., \*a.example.com).   </div><br>   <br><br>* Duplicate domains are not allowed under the same policy.<br><br><br> |
   |Effective scope |Supports "Claw" and "All". |
   |Source Claw |Select the Claw instance.<br><br><br>* If the source type is "Claw", select one or more specific Claw instances.<br><br>* If the source type is "All", select All, representing all Claw instances. |
   

6. Click "OK" to complete the action.


</Tab>
<Tab zoneid="fe18hflJ" title="Edit DNS access rule">
<TabTitle>Edit DNS access rule</TabTitle>

1. Log in to the[ ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Click the "Space Egress \> Private network egress" tab.

4. On the "DNS access policy" tab, click "Edit" to the right of the target rule.

5. Modify parameters then click "OK" to complete the action.


</Tab>
<Tab zoneid="sDPI4Wva" title="Delete DNS access rule">
<TabTitle>Delete DNS access rule</TabTitle>

1. Log in to the[ ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Click the "Space Egress \> Private network egress" tab.

4. On the "DNS access policy" tab, click "Delete" to the right of the target rule.

5. Click "Delete" to complete the action.


</Tab>
</Tabs>


<span id="wOccz9Xo"></span>
###
