---
title: "Configure web tamper protection policies"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Configure_web_tamper-proofing_policies"
---

The web tamper protection strategy supports caching the pages of the website that needs to be protected. When a request is received for the protected website, a cached page is returned to ensure the security of the website's content against the risk of hackers tampering.

<span id="1f2e6db9"></span>
## Prerequisites

You have connected the website that needs to be protected to the WAF instance. For access\-related operations, please refer to [Comparison of website association methods](https://docs.byteplus.com/en/docs/6511/935148).

<span id="73a33f97"></span>
## Procedure


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. Select the instance region in the top menu bar.

3. In the left navigation, select **Protection Policies \> Web Tamper Protection**.

4. Enable the web tamper protection feature for the domain name to be protected.

   1. Select the domain name to which you want to add a policy.

   2. (Optional) Confirm that the protection mode of the current domain is "Protection enabled". Otherwise, click **Change protection mode** to modify it.

   3. Turn on the policy enable switch.

5. Click **Add** to configure the web tamper protection rule parameters.

   
   |**Parameter** |**Description** |Example |
   |---|---|---|
   |Rule name |Protection rule name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Start with a letter or digit.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Allowed characters include letters, digits, periods (.), underscores (_), and hyphens (\-).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The length must be between 1 and 128 characters.</div><br> |tamper_protection_1 |
   |Rule description |Fill in the relevant notes for the rule. |Prevent key page information from being tampered with |
   |Request path |Fill in the exact path to be protected, for example: `/test.html`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Please fill in the request path starting with<code>/</code>the precise path that ends with <code>html</code>, <code>shtml</code>, <code>txt</code>, <code>js</code>, <code>css</code>, <code>jpg</code>, <code>png</code>, and does not support wildcards (like <code>/test/*</code>) or parameters, and the page size must not exceed 32 KB.</div><br> |/test.html |
   |Regular switch off |Turn on or off the current rule. |Keep it enabled |
   

6. Click **OK** to complete the rule configuration.


<span id="f60c2435"></span>
## Optional actions

After configuration is complete, you can view rule information in the web tamper protection rule list and perform rule disabling/enabling, cache updating, editing, and deletion operations. <br/\>Updating the cache refers to updating the cached page to the current latest page, applicable in scenarios where website content has been updated.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the protected page with configured rules has updated content, you need to update the cache under the corresponding protection rule; otherwise, the WAF will return the most recent cached record.</div>
