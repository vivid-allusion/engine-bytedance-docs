---
title: "Configure policies to prevent sensitive information leakage"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Configure_data_leak_prevention_policies"
---

The sensitive information leakage prevention rules can filter user sensitive information in the server's return content, such as ID card numbers, mobile phone numbers, and bank card information, desensitizing the display of sensitive information to prevent the leakage of user privacy information.

<span id="5c9ef53c"></span>
## Requirements

You have connected the website that needs to be protected to the WAF instance. For more details, see [Comparison of website association methods](https://docs.byteplus.com/en/docs/6511/935148).

<span id="1101749b"></span>
## Procedure


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. Select the instance region in the top menu bar.

3. In the left navigation, select **Protection policy \> Sensitive information leakage prevention**.

4. Enable the sensitive information leakage prevention feature for the domains to be protected.

   1. Select the domain that needs to add the policy.

   2. (Optional) Confirm that the protection mode of the current domain is "Protection enabled". Otherwise, click **Change protection mode** to modify it.

   3. Turn on the policy enable switch.

5. Click to add configuration and configure sensitive information leakage rule parameters.

   
   |**Parameter** |**Description** |Example |
   |---|---|---|
   |Rule name |Protection rule name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Start with a letter or digit.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Allowed characters include letters, digits, periods (.), underscores (_), and hyphens (\-).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The length must be between 1 and 128 characters.</div><br> |Prevent sensitive information leakage_1 |
   |Rule description |Fill in relevant remarks. |Prevent leakage of user sensitive information |
   |Request path |Fill in the website paths that need protection, which can be a specific page path or all paths under the entire website.<br><br><br>* **Match specific path**: A specific page path, for example, to intercept access to `test.com/test.html`, directly fill in the path information after the domain name `/test.html`.<br><br>* **Match all paths under the directory**: Use`*`Can match all paths, and`*`Must be at the end of the path.<br><br>   * To match all paths under the entire website, fill in `/*`.<br><br>   * To match all paths under a specific directory, use`*`In the corresponding directory path. For example, `/test/*` indicates matching all paths under the `/test/` directory.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><code>/test/*/abc.html</code> and <code>/test/*</code> both indicate matching all paths under the <code>/test/</code> directory.   </div><br>    |/test.html |
   |Action |* Observe: Allow the traffic to pass through, but record the behavior in the attack log.<br><br>* Intercept: Intercept the request traffic and report the request behavior to the attack log. If a custom interception response page is configured, WAF will return the configured interception response page information to the client side. |Block |
   |Enable |Turn on or off the current rule. |Keep it enabled |
   |Matching content |Hope WAF detects ID cards, mobile numbers, bank cards, email addresses, birth dates, and names. |ID card, name |
   |Advanced conditions |* Set other matching fields, logical operators, and matching content. Please refer to the [Advanced conditions configuration instructions](https://docs.byteplus.com/en/docs/6511/1356289) for related explanations on matching fields and logical operators.<br><br>* The relationship between **request path** and **advanced conditions** is a `conjunction`, meaning that the rules can only be triggered when both the request path and the added conditions are satisfied.<br><br>* **Multi\-request path matching**: If rules need to take effect on multiple request paths, please first configure the main request path to include all paths under the directory, and then add the matching fields as conditions for the request path. For example, if you need to configure `/test/123.html` and `/test/abc.jpg`, you can refer to the following operations:<br><br>   1. Set the **request path** to `/test/*`.<br><br>   2. Add 2 conditions:<br><br>      * Condition 1: `request path` equals `/test/123.html`<br><br>      * Condition 2: `request path` equals `/test/abc.jpg`<br><br>   3. The condition relationship of both is set to `OR`. |None |
   

6. Click **OK** to complete the rule configuration.

   After configuration is complete, you can view rule information in the sensitive information leakage rule list and perform rule disable/enable, edit, and delete operations.
