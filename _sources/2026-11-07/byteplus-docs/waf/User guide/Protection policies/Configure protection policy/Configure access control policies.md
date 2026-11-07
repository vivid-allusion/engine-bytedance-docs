---
title: "Configure access control policies"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/docs-configuring-access-control-policies"
---

The access control policy refers to the control and restriction of the access behavior of a specific IP that meets the set rules or all IP access behaviors from a specific region. You can set the access source by manually adding IP addresses, referencing the IP address group, or selecting the geographic location of the IP. In addition, setting specific access characteristic paths can help control the scope of policy effectiveness. Supports setting up blocklists and allowlists.

<span id="3750eb8d"></span>
## Precautions


* When you delete the address group or domain group associated with a rule, if there are no other valid associated groups for that rule, the system will automatically delete that rule.

* You can flexibly choose different configuration methods to achieve the same protection effect. For example, you can either directly configure protection rules for the domain name or add the domain name to a domain group and then configure group\-level rules. If multiple related rules exist at the same time, it is recommended that you refer to [Explanation of blocklist policy matching priority](https://docs.byteplus.com/en/docs/waf/Priority_of_blocklist_policies) to understand the specific priority of rule effectiveness.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have connected the website that needs to be protected to the WAF instance. For more details, see [Comparison of website association methods](https://docs.byteplus.com/en/docs/6511/935148)

<span id=".5pON5L2c5q2l6aqk"></span>
## Add a blocklist

Add a specific IP to the network blocklist, and the relevant access behavior under this IP will be directly intercepted, and you can check the access records in the attack log.


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. In the top menu bar, select the region of your instance.

3. In the left navigation, select **Protection Policy \> Access Control**.

4. Turn on the blocklist feature.

   1. Click **Blocklist**.

   2. Turn on the policy switch.

5. Click **Add**, configure the rule parameters.

   
   |**Parameter** |**Note** |**Example** |
   |---|---|---|
   |Basic Information |||
   |Rule name |Protection rule name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Start with a letter or digit.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Allowed characters include letters, digits, Chinese characters, periods (.), underscores (_), and hyphens (\-).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The length must be between 1 and 128 characters.</div><br> |Block_rule1 |
   |Rule description |Fill in relevant remarks about the rules, such as the reason for interception. |Intercept access from the corresponding IP. |
   |Protected domain |* **Select domain**: Select domains that have been integrated with protection, supports selecting multiple domains.<br><br>* **Select domain group**: Select already created domain groups, supports selecting multiple domain groups. |Select domain group |
   |Rule conditions |||
   |IP address |* **Manually add**: Manually enter the IP address to be added to the blocklist, supports entering a single IP address, IP address range, or all IP addresses (\*).<br><br>* **Reference address group**: Select an already created IP address group, supports selecting multiple address groups.<br><br>* **Select geographic location**: Check the IP source areas to be restricted, supports selecting multiple regions. |192.1.1.1 |
   |Feature Description |* **Request path**: Fill in the website path that needs protection, which can be a specific page path or all paths under the entire website.<br><br>   * **Match specific path**: A specific page path, for example, if you need to intercept access to `test.com/test.html`, just fill in the path information after the domain name `/test.html`.<br><br>   * **Match all paths under the directory**: Use`*`to match all paths, and`*`must be at the end of the path.<br><br>      * To match all paths under the entire website, just fill in `/*`.<br><br>      * To match all paths under a specific directory, use`*`at the corresponding directory path. For example, `/test/*` indicates matching all paths under the `/test/` directory.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2"><code>/test/*/abc.html</code> and <code>/test/*</code> both indicate matching all paths under the <code>/test/</code> directory.      </div><br>      <br><br>* **Add conditions**: Set other matching fields, logical operators, and matching content. For details on matching fields and logical operators, please refer to [Advanced Condition Configuration Instructions](https://docs.byteplus.com/en/docs/6511/1356289).<br><br>* There is an `AND` relationship between **request path** and **Add conditions**, meaning that the rule will only be triggered when both the request path and the add conditions are met.<br><br>* **Multiple request path matching**: If you need the rule to be effective for multiple request paths, first configure the main request path to match all paths under the directory, then add conditions that match fields for the request path. For example, to configure `/test/123.html` and `/test/abc.jpg`, you can refer to the following steps:<br><br>   1. Set the **request path** to `/test/*`.<br><br>   2. Add 2 conditions:<br><br>      * Condition 1: `Request path` equals `/test/123.html`<br><br>      * Condition 2: `Request path` equals `/test/abc.jpg`<br><br>   3. The relationship between the two conditions is set to `or`. |* Request path: /test.html<br><br>* Add condition: `Request method` `Equals` `POST` |
   |Execute action |* Observe: Allow the traffic to pass through, but record the behavior in the attack log.<br><br>* Block: Block the traffic and report the behavior in the attack log. If a custom interception response page is configured, WAF will return the configured interception response page information to the client side. |Block |
   |Effective configuration |||
   |Enable |Turn on or off the current rule. |Keep it enabled |
   

6. Click **OK** to complete the rule configuration.

   After the configuration is complete, you can view the rule information in the list and perform rule close/open, edit and delete operations.


<span id="38c28e6a"></span>
## Add an allowlist

Add a specific IP to the network Allowlist, and the relevant access behavior under this IP will not be affected by all detection and interception rules; you can view the access records in the access logs.


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. In the top menu bar, select the region of your instance.

3. In the left navigation, select **Protection Policy \> Access Control**.

4. Enable the Allowlist feature.

   1. Click **Allowlist**.

   2. Turn on the policy switch.

5. Click **Add**, configure the rule parameters.

   
   |**Parameter** |**Description** |Example |
   |---|---|---|
   |Basic Information |||
   |Rule name |Protection rule name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Start with a letter or digit.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Allowed characters include letters, digits, periods (.), underscores (_), and hyphens (\-).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The length must be between 1 and 128 characters.</div><br> |Allow_rule1 |
   |Rule description |Fill in remarks related to the rule, such as the reason for allowing access. |Allow access to corresponding IP |
   |Protected domain |* Select domain: Choose the domains that have already been protected, supports selecting multiple domains.<br><br>* Select domain group: Choose the created domain groups, supports selecting multiple domain groups. |Select Domain Group |
   |Rule condition |||
   |IP address |* Manually add: manually input the IP addresses that need to be added to the Allowlist, supporting the entry of a single IP address, IP address range, or all IP addresses (\*).<br><br>* Reference IP address group: select the already created IP address groups, supporting the selection of multiple address groups.<br><br>* Select geographical location: check the IP source regions that need to be restricted, supporting the selection of multiple regions. |192.1.1.1 |
   |Feature description |* **Request path**: fill in the website path that needs protection, which can be a specific page path or all paths under the entire website.<br><br>   * **Match specific path**: a specific page path, for example, if you need to intercept access to `test.com/test.html`, just fill in the path information after the domain name `/test.html`.<br><br>   * **Match all paths under directory**: use`*`can match all paths, and`*`must be at the end of the path.<br><br>      * To match all paths under the entire website, just fill in `/*`.<br><br>      * To match all paths under a specific directory, use it under the corresponding directory path.`*`Done. For example, `/test/*` indicates matching all paths under the `/test/` directory.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2"><code>/test/*/abc.html</code> and <code>/test/*</code> both indicate matching all paths under the <code>/test/</code> directory.      </div><br>      <br><br>* **Add conditions**: Set other matching fields, logical operators, and matching content. Please refer to the [Advanced Condition Configuration Instructions](https://docs.byteplus.com/en/docs/6511/1356289) for related explanations on matching fields and logical operators.<br><br>* The relationship between **request path** and **Add conditions** is `AND`, that is, the rule can be triggered only when both the request path and added conditions are met.<br><br>* **Multiple request path matching**: If you need rules to apply to multiple request paths, first set the main request path to all paths under the directory, then add conditions for matching fields as the request path. For example, to configure `/test/123.html` and `/test/abc.jpg`, you can refer to the following operations:<br><br>   1. Set the **request path** to `/test/*`.<br><br>   2. Add 2 conditions:<br><br>      * Condition 1: `Request path` equals `/test/123.html`<br><br>      * Condition 2: `Request path` equals `/test/abc.jpg`<br><br>   3. The relationship between the two conditions is set to `or`. |* Request path: /test.html<br><br>* Add condition: `Request method` `Equals` `GET` |
   |Execute action |All requests are allowed, meaning that requests satisfying the conditions are not affected by any detection and interception rules. |No configuration required |
   |Effective Configuration |||
   |Enable |Turn on or off the current rule. |Keep it enabled |
   

6. Click **OK** to complete the rule configuration.

   After the configuration is complete, you can view the rule information in the list and perform rule close/open, edit and delete operations.
