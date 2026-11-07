---
title: "Configure custom response page policies"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Configure_custom_response_page_policies"
---

The custom interception response policy supports setting response codes and response page information to return specific information for requests that meet certain conditions (except for CC interception) to display customized information to the client.

<span id="3750eb8d"></span>
## Notes

Custom response for blocked requests do not apply to rate limiting rules.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have connected the website that needs to be protected to the WAF instance.

<span id="730737e1"></span>
## Steps


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. Select the instance region in the top menu bar.

3. In the left navigation, select **Protection Policy \> Custom Response Page**.

4. Turn on the custom interception response function of the domain name to be protected.

   1. Select the domain to which you want to add the policy.

   2. (Optional) Confirm that the protection mode of the current domain is "Protection enabled". Otherwise, click **Change protection mode** to modify it.

   3. Turn on the policy switch.

5. Click **Add Rule** to configure custom intercept response parameters.

   
   |**Parameter** |**Note** |Example |
   |---|---|---|
   |Rule name |Protection rule name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Start with a letter or digit.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Allow letters, digits, Chinese characters, dot “.”, underscore “_”, and hyphen “\-”.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The length must be between 1 and 128 characters.</div><br> |Response Interception_1 |
   |Rule description |Fill in the relevant notes about the rules, such as the reason for adding. |Return specific response information |
   |Request path |Please fill in the website path that requires protection, which can be a specific page path or all paths under the entire website.<br><br><br>* **Match specific path**: A specific page path, for example, to intercept access to `test.com/test.html`, directly fill in the path information after the domain name `/test.html`.<br><br>* **Match all paths under the directory**: use`*`to match all paths, and`*`must be at the end of the path.<br><br>   * To match all paths under the entire website, fill in `/*`.<br><br>   * To match all paths under a specific directory, use in the corresponding directory path`*`only. For example, `/test/*` means to match all paths under the `/test/` directory.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><code>/test/*/abc.html</code> and <code>/test/*</code> both match all paths under the <code>/test/</code> directory.   </div><br>    |/test.html |
   |Enable |Turn on or off the current rule. |Keep it enabled |
   |Response Code |Sets the response code to return when the request is intercepted. |405 |
   |Page Template |* System default: Select the system default template, support `text/html`, `text/xml`, `application/json` three page types.<br><br>* Customization: Fill in the custom page template, support `text/html`, `text/xml`, `application/json` three page types, and customize the page content.<br><br>* Redirect: Fill in the redirect path, such as `/common/info/redirect`. |* Page template: Custom<br><br>* Page type: text/html<br><br>* Page content: `<!DOCTYPE html> <html> <meta charset="utf-8"> <body> <p> You do not have access permission, please obtain authorization and try again.` `</p> </body> </html>` |
   |Advanced conditions |* Set matching fields, logical operators and matching content for other conditions.<br><br>* The **request path** and **advanced conditions** have an `and` relationship, which means that the rule can only be triggered when both the request path and added conditions are satisfied.<br><br>* **Multiple Request Path Matching**: If you need the rule to apply to multiple request paths, first configure the main request path to include all paths under the directory, and then add conditions matching fields as the request path. For example, if you need to configure `/test/123.html` and `/test/abc.jpg`, you can refer to the following operation:<br><br>   1. Set the **request path** to `/test/*`.<br><br>   2. Add 2 conditions:<br><br>      * Condition 1: `request path` equals `/test/123.html`<br><br>      * Condition 2: `request path` equals `/test/abc.jpg`<br><br>   3. Set the relationship between the two conditions to `OR`. |None |
   

6. Click **OK** to complete the rule configuration.

   After the configuration is complete, you can view the rule information in the list and perform rule close/open, edit and delete operations.
