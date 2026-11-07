---
title: "Custom Error Pages"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-custom-error-pages_1"
---

The Custom Error Page feature allows you to improve user experience by replacing standard CDN error pages (status codes 400\-599) with your own user\-friendly pages. When an error occurs, BytePlus CDN can redirect the user request to your specified URL, which can provide helpful troubleshooting information.

This document describes how to configure this feature and lists its exceptions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In certain situations, this configuration will not take effect. See <a href="https://docs.byteplus.com/en/docs/18/6575#exceptions">Exceptions</a>.</div>


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e83eaa41416fb7851d659f497ec72022.png) </span>

<span id="steps"></span>
## Steps


1. Open the **Custom Error Pages** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to Enabled.

3. Click **Add Rule**.

   You can add up to 50 rules.

4. See the following table for configuration details.

5. After you finish configuring the rules, click **Save**.



|**Configuration** |**Description** |
|---|---|
|Priority |Indicates the priority of the rule. A priority of 1 is the highest. The highest\-priority rule is applied first. If a request matches a rule, only that rule is applied. You can drag the rules to adjust their priority. |
|Status Code |Enter a status code in the range of 400\-599. You can also enter 4xx to indicate any status code between 400\-499. |
|Redirect Style |Select the response status code for redirection. The options for this configuration are **301**, **302**, **303**, **307**, **308**.<br><br>&nbsp;<br><br>Note that:<br><br><br>* For 301 and 302, if the method used by the original request is not GET, the method used by the new request sent by the client to the new URL may be changed to GET.<br><br>* For 303, the method used by the new request is always GET.<br><br>* For 307 and 308, the method used by the new request is the same as the original request and will not change. |
|Target URL |Enter the target URL for redirection, with a length not exceeding 1,024 characters. The target URL must comply with URL specifications, including protocol, domain name, and path.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The target URL's domain name cannot be the same as the accelerated domain to be bound to the policy; otherwise, the configuration will not take effect.</div><br> |


<span id="exceptions"></span>
## Exceptions

If an error status code is triggered for any of the following reasons, the CDN returns the standard error page instead of redirecting to your configured target URL:


* The user request is rejected by the CDN because it matches your configured access control rules.

* The request URL has been blocked by the CDN.


Additionally, if the CDN does not receive a response from the origin server when requesting a file, the CDN will not redirect the user request to the target URL you configured.
