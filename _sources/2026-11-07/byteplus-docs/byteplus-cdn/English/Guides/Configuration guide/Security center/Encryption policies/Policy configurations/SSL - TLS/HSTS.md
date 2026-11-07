---
title: "HSTS"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-hsts_1"
---

HSTS (HTTP Strict Transport Security) is a web security policy that protects your website from downgrade attacks and cookie hijacking by forcing browsers to use HTTPS. This document explains how HSTS works and guides you through enabling it for your domain names in BytePlus CDN.

<span id="overview-of-hsts"></span>
## Overview of HSTS

HSTS stands for HTTP Strict Transport Security, which is a policy mechanism for web security. The purpose of HSTS is to protect users from downgrade attacks and cookie hijacking while accessing HTTPS sites. After enabling HSTS for your site, the site's responses will include a `Strict-Transport-Security` response header. This header informs browsers that every request sent to the site must use the HTTPS protocol.

The `Strict-Transport-Security` header also includes two parameters. See [Configuration Instructions](https://docs.byteplus.com/en/docs/18/6603#configuration-instructions) for descriptions of these parameters.

<span id="hsts-and-http-redirect-to-https-configuration"></span>
## HSTS and "HTTP Redirect to HTTPS" Configuration

In the "Protocol Redirect" feature provided by CDN, there is a configuration called "HTTP Redirect to HTTPS" (hereinafter referred to as "HTTP Redirect"). The purpose of this configuration is for the CDN to redirect received HTTP requests to HTTPS requests.

Before explaining HSTS in detail, it's important to understand the difference between HSTS and HTTP Redirect.

HTTP is an insecure protocol. When a user sends a request to a site via HTTP in a browser, the request could be hijacked and redirected to a malicious site. To avoid HTTP requests from accessing your domain name, CDN provides the following two configurations:


* HTTP Redirect

* HSTS


<span id="limitations-of-http-redirect"></span>
### Limitations of HTTP Redirect

After configuring HTTP Redirect, if a browser sends an HTTP request to the CDN, the CDN will return a 301 or 302 response status code instructing the browser to redirect the HTTP request to an HTTPS request. For more information on HTTP Redirect, see [Protocol redirect](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-protocol-redirect_1).

However, even after configuring HTTP Redirect, users can still specify HTTP in the browser to send HTTP requests to the CDN. Although these will be redirected to HTTPS, these HTTP requests are still at risk of being hijacked before reaching the CDN.

<span id="advantages-of-hsts"></span>
### Advantages of HSTS

Compared to HTTP Redirect, HSTS provides a more secure solution. After enabling HSTS for your domain name, `Strict-Transport-Security` response headers will be included in CDN's responses. If the browser has successfully sent a request using HTTPS to the CDN once, the browser will cache this header. Suppose the user again uses HTTP in the browser to visit the site. Before sending the request, the browser will convert HTTP to HTTPS. Since the conversion occurs on the browser side, it significantly reduces the number of HTTP requests sent to the CDN by the browser, as well as the risk of HTTP requests being hijacked.

<span id="prerequisites-for-the-hsts-response-header-to-take-effect"></span>
#### Prerequisites for the HSTS Response Header to Take Effect

Although HSTS is more secure, the following conditions must be met for the browser to follow the `Strict-Transport-Security` header and convert HTTP to HTTPS:


* The browser has cached the `Strict-Transport-Security` response header.

* The cached header has not expired. For more information on the cache validity period of the `Strict-Transport-Security` response header, see [Configuration Instructions](https://docs.byteplus.com/en/docs/18/6603#configuration-instructions).


After enabling HSTS for the domain, the CDN will include the `Strict-Transport-Security` response header in the response to any request. However, for the browser to cache this header, the browser must have successfully sent a request to the CDN using HTTPS at least once. Therefore, when you enable HSTS, it is recommended that you also enable Protocol Redirect and set the **Policy** to **Redirect HTTP to HTTPS**.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you enable HSTS in the CDN console, the CDN will prompt you whether you need to enable the configuration for HTTP Redirect. See <a href="https://docs.byteplus.com/en/docs/18/6603#steps">Steps</a>.</div>


<span id="interaction-process-between-browser-and-cdn"></span>
#### Interaction Process Between Browser and CDN

After you have enabled both HSTS and HTTP Redirect, if a user sends an HTTP request to the CDN using a browser, the interaction process between the browser and CDN is as follows:


1. The browser checks for a cached `Strict-Transport-Security` response header.

2. Since the header is not in the browser's cache, the browser sends the HTTP request to the CDN.

3. Upon receiving the request, due to the HTTP Redirect configuration, the CDN's response status code is 301 or 302. At the same time, because of the HSTS configuration, the response includes the `Strict-Transport-Security` response header. At this point, since no request has been sent to the CDN using HTTPS, the browser does not cache the header.

4. Because of the 301 or 302 response status code, the browser sends an HTTPS request to the CDN. In the response, the CDN includes the `Strict-Transport-Security` response header again. Suppose the header's `max-age` is 10 minutes, and the HTTPS request successfully retrieves the requested file.

5. Since the HTTPS request is successful, the browser caches the `Strict-Transport-Security` response header.


Within 10 minutes, if the user uses the browser to send another HTTP request to the CDN, the interaction process between the browser and CDN is as follows:


1. The browser checks for a cached `Strict-Transport-Security` response header.

2. Because the header is in the browser's cache, the browser checks if it is still valid.

3. Since the header has not expired, the browser converts HTTP to HTTPS and sends the request to the CDN.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If the cached <code>Strict-Transport-Security</code> response header has expired, when the user sends an HTTP request to the CDN, the steps described in the <a href="https://docs.byteplus.com/en/docs/18/6603#browser-cdn-interaction">Browser and CDN Interaction Process</a> will be repeated.</div>


* <div data-tips="true" data-tips-type="tip">Even with both HSTS and HTTP Redirect enabled, it is still possible for the CDN to receive some HTTP requests. This is because the browser will not convert HTTP to HTTPS in the following situations:</div>


   * <div data-tips="true" data-tips-type="tip">The <code>Strict-Transport-Security</code> response header does not exist in the browser's cache.</div>


   * <div data-tips="true" data-tips-type="tip">The <code>Strict-Transport-Security</code> response header in the browser's cache has expired.</div>



<span id="prerequisites"></span>
### Prerequisites


1. Open the **HSTS** configuration page. For the operation steps, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to **Enabled**.

3. Refer to the [configuration instructions](https://docs.byteplus.com/en/docs/18/6603#configuration-instructions) below.

4. After configuring, click **Save**.


<span id="configuration-instructions"></span>
### Configuration Instructions


|**Configuration** |**Description** |
|---|---|
|Max\-age |Represents the expiration time for the `Strict-Transport-Security` response header cached in the client's browser. This setting corresponds to the `max-age` parameter of the `Strict-Transport-Security` response header. Before sending an HTTP request, the browser will check whether its cached `Strict-Transport-Security` response header has expired. If the header has expired, the browser will not convert HTTP to HTTPS.<br><br>&nbsp;<br><br>The maximum time you can set is 31,536,000 seconds, equivalent to 365 days. If you set the expiry time to `0`, it is effectively the same as disabling HSTS.<br><br>&nbsp;<br><br>Note: If a new response contains a Strict\-Transport\-Security header, the browser updates the cached header's expiration time with the new value from the response. |
|Include Subdomains? |Indicates whether the HSTS configuration should apply to subdomain sites. The configuration has the following options:<br><br><br>* **No**: Indicates that the HSTS configuration does not apply to subdomain sites.<br><br>* **Yes**: Indicates that the HSTS configuration applies to subdomain sites. In this case, the response header will include the `includeSubDomains` parameter.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you set this configuration to <strong>Yes</strong>, the response header returned by the CDN tells the browser that requests sent to all subdomains must also use the HTTPS protocol. If you enable this option, ensure that all corresponding subdomains are accessible via HTTPS. Furthermore, the subdomains should also have a similar setup that redirects HTTP requests made to the subdomains to HTTPS requests.</div><br> |


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21991d364f924a3bb6cc179ea7af0f6d~tplv-goo7wpa0wc-image.image) </span>

**Examples**


* Example 1: You set `Max-age` to 6 seconds and include subdomains. In this case, the actual response header returned by the CDN is:

   * `Strict-Transport-Security: max-age=6;includeSubDomains`

* Example 2: You set `Max-age` to 1 day and do not include subdomains. In this case, the actual response header returned by the CDN is:

   * `Strict-Transport-Security: max-age=86400`


<span id="more-information"></span>
## More Information

<span id="how-to-manage-hsts-settings-in-browsers"></span>
### How to Manage HSTS Settings in Browsers

This section explains how to manage HSTS settings, using Google Chrome and Microsoft Edge as examples.

In Chrome or Edge, access the following URL:


* `chrome://net-internals/#hsts`


On the page that opens, you can:


* Add a domain to the browser's HSTS cache.

* Delete a specified domain from the browser's HSTS cache.

* Query whether a domain exists in the browser's HSTS cache.

   * If the domain does not exist, the query result is `Not found`.

   * If the domain does exist, the query result will show the domain's HSTS configuration information. In the configuration information, `dynamic_sts_observed` indicates the time the browser cached the domain, in Unix timestamp format. `dynamic_sts_expiry` represents the expiration time of the domain in the HSTS cache.


When querying a domain, the result data may be delayed by 1 minute.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bceca7d3f4666d763c878521f8ae8164.png) </span>
