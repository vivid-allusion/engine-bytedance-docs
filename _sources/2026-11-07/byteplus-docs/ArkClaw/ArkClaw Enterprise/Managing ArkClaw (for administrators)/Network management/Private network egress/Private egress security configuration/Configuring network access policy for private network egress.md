---
title: "Configuring network access policy for private network egress"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring-a-private-egress-network-access-policy"
---

<span id="eiklVEVY"></span>
## Scenarios

Network Access Policy controls Layer\-4 private network traffic from Claw instances to your corporate services. You can configure the network access policy for a private network egress​ to allow or deny​ Claw instances access to specific target IPs and ports.

<span id="sPwFwgn5"></span>
## Before you begin

Private Network Egress must be enabled. For procedure, see [Configuring private network egress](https://docs.byteplus.com/en/docs/ArkClaw/Enabling-or-disabling-the-private-egress-Old-version).

<span id="jHajQXLM"></span>
## Enable or disable network access policy


1. Log in to the[ ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Click the "Space Egress \> Private network egress" tab.

4. Click the "Network access control" tab.

   * Enable: Click the edit icon next to Policy ID, then click "OK" to enable network access policy.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If no Policy ID is visible, please submit an <a href="https://console.byteplus.com/arkclaw/enterprise/region:arkclaw/enterprise+cn-beijing/issue-feedback?projectName=default&spaceId=csi-yehwr79wjkjjbs00n282">issue feedback</a>.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Once the network access policy is enabled, the system creates a default rule​ that allows all traffic. This default rule has the lowest priority​ and cannot be deleted.      </div>
      

   * Disable: Click the edit icon next to Policy ID, then click "OK" to disable network access policy.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">After the network access policy is disabled, all configured rules will be suspended. Layer 4 traffic will be fully allowed. Configured rules are not deleted. They will take effect again when the policy is re\-enabled.      </div>
      

<span id="djaVRavl"></span>
## Configure a network access rule


<Tabs>
<Tab zoneid="xB3Byse2" title="Add network access rule">
<TabTitle>Add network access rule</TabTitle>

1. Log in to the[ ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Click the "Space Egress \> Private network egress" tab.

4. On the "Network access policy" tab, click "Add Rule".

5. Configure parameters based on the table below.

   
   |Parameter |Description |
   |---|---|
   |**Basic information** ||
   |Rule name |Enter the rule name. |
   |Priority |Enter the priority. Valid range: 1\-10000. A smaller number indicates higher priority. |
   |Rule description |Enter the description for the rule. |
   |**Match condition** ||
   |Protocol |Select the protocol. Supported options:<br><br><br>* **All**: Matches all protocols (TCP + UDP + ICMP). Suitable for allowing or blocking all traffic.<br><br>* **TCP**: Matches TCP traffic. Suitable for managing HTTP/HTTPS, database connections, and SSH.<br><br>* **UDP**: Matches UDP traffic. Suitable for managing DNS (port 53) and video streaming.<br><br>* **ICMP**: Matches ICMP traffic. Suitable for managing network diagnostics like ping and traceroute. |
   |Source type |Select the source type. Supports "Claw" and "All". |
   |Source Claw |Select the source Claw instance.<br><br><br>* If the source type is "Claw", select one or more specific Claw instances as the traffic source.<br><br>* If the source type is "All", select All, representing all Claw instances. |
   |Destination IP |Enter the IP address of the corporate service that the Claw instance needs to access.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">"All" represents all destination IPs.</div><br> |
   |Destination port |Enter a single port or port range for the enterprise service.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">"All" represents all destination ports.</div><br> |
   |Action |Select the action.<br><br><br>* Allow: Permits the traffic flow.<br><br>* Block: Deny the traffic flow. |
   

6. Click "OK" to complete the action.




</Tab>
<Tab zoneid="TugWlCuV" title="Edit network access rule">
<TabTitle>Edit network access rule</TabTitle>

Default rules cannot be modified.


1. Log in to the[ ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Click the "Space Egress \> Private network egress" tab.

4. On the "Network access policy" tab, click "Edit" to the right of the target rule.

5. Modify parameters then click "OK" to complete the action.


</Tab>
<Tab zoneid="wFhBfHsy" title="Delete network access rule">
<TabTitle>Delete network access rule</TabTitle>

The default rule cannot be manually deleted. The rule is automatically removed when the private network egress is disabled.


1. Log in to the[ ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Click the "Space Egress \> Private network egress" tab.

4. On the "Network access policy" tab, click "Delete" to the right of the target rule.

5. Click "Delete" to complete the action.


</Tab>
</Tabs>


<span id="UKmBVAjO"></span>
##
