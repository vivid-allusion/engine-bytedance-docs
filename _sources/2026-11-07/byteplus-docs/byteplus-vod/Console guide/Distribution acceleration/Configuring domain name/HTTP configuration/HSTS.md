---
title: "HSTS"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-hsts"
---

To protect your users from downgrade attacks and cookie hijacking, you can enable HTTP Strict Transport Security (HSTS) for your acceleration domain. HSTS instructs browsers to only communicate with your site over a secure HTTPS connection, enhancing security. This guide provides step\-by\-step instructions on how to configure HSTS in the BytePlus VOD console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">HSTS applies to <strong>Custom\-origin domain</strong> <strong>name</strong>.</div>


<span id="cdd277a7"></span>
## Introduction

<span id="4e3525a7"></span>
### Overview of HSTS

HSTS stands for HTTP Strict Transport Security, which is a network security policy mechanism. The purpose of HSTS is to protect users from downgrade attacks and cookie hijacking when accessing HTTPS sites. After enabling HSTS for a site, the site's response will include the `Strict-Transport-Security` response header, which informs the browser that every request sent to the site must use the HTTPS protocol.

<span id="9d1c638b"></span>
### HSTS vs. protocol redirect

Before further explaining HSTS, it is necessary to explain the difference between HSTS and protocol redirect.

HTTP is an insecure protocol. When a user sends a request to a site using the HTTP protocol in a browser, the request may be hijacked and redirected to a malicious site. To prevent HTTP requests from accessing acceleration domains, BytePlus VOD provides the following two configurations:


* Protocol redirect: After enabling protocol redirect, you need to set the **Policy** to **HTTP to HTTPS**.

* HSTS.


<span id="93e5c859"></span>
### Limitations of protocol pedirect

After configuring protocol redirect, if a browser sends an HTTP request to the CDN, the CDN will return a 301 or 302 response status code to the browser, instructing the browser to redirect the HTTP request to an HTTPS request. For more information about protocol redirect, see [Protocol redirect](https://docs.byteplus.com/docs/byteplus-vod/docs-force-redirect).

However, even if you have configured protocol redirect, users can still specify the HTTP protocol in the browser to send HTTP requests to the CDN. Although these HTTP requests will be redirected to HTTPS requests, there is still a risk of hijacking before the HTTP requests reach the CDN.

<span id="baa8dc2f"></span>
### Advantages of HSTS

Compared to protocol redirect, HSTS provides a more secure solution. After enabling HSTS for the acceleration domain, the Content Delivery Network (CDN) response will include the `Strict-Transport-Security` response header. If the browser successfully sends a request to the CDN using the HTTPS protocol, the browser will cache this response header. Suppose the user later tries to access the CDN using the HTTP protocol in the browser. Before sending the request, the browser will convert HTTP to HTTPS. Since the conversion process happens on the browser side, it greatly reduces the number of HTTP requests sent to the CDN. It also reduces the risk of HTTP requests being hijacked.

<span id="1b8713f4"></span>
#### Preconditions for the HSTS response header to take effect

Although the HSTS solution is more secure, the following conditions must be met for the browser to follow the `Strict-Transport-Security` response header and convert HTTP to HTTPS:


* The browser has cached the `Strict-Transport-Security` response header.

* The cached response header has not expired. For the cache validity period of the `Strict-Transport-Security` response header, refer to [HSTS](https://docs.byteplus.com/docs/byteplus-vod/docs-hsts).


After enabling HSTS for the acceleration domain, the CDN will return the `Strict-Transport-Security` response header for any request. However, for the browser to cache this response header, the browser must have successfully sent a request to the CDN using the HTTPS protocol. Therefore, when you enable HSTS, it is recommended to also enable protocol redirect and set the **Policy** to **HTTP to HTTPS**.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you enable HSTS in the CDN console, the CDN will prompt you whether you need to enable the configuration for protocol redirect.</div>


<span id="1e9c9ba6"></span>
#### Interaction between the browser and the CDN

After enabling HSTS and protocol redirect, if a user sends an HTTP request to the CDN using a browser, the interaction between the browser and the CDN is as follows:


1. The browser checks whether the `Strict-Transport-Security` response header is cached.

2. Since the response header is not cached in the browser, the browser sends the HTTP request to the CDN.

3. After receiving the request, the CDN responds with a status code of 301 or 302 due to the protocol redirect configuration. At the same time, the response contains the `Strict-Transport-Security` response header due to the HSTS configuration. In this case, since the browser has not successfully sent a request to the CDN using the HTTPS protocol, the browser does not cache this response header.

4. Due to the 301 or 302 response status code, the browser sends an HTTPS request to the CDN. In the response, the CDN also includes the `Strict-Transport-Security` response header. Assuming this response header is valid for 10 minutes, the HTTPS request successfully obtains the requested file.

5. Due to the successful HTTPS request, the browser caches the `Strict-Transport-Security` response header.


Within 10 minutes, suppose the user sends an HTTP request to the CDN using the browser again. The interaction between the browser and the CDN is as follows:


1. The browser checks whether the `Strict-Transport-Security` response header is cached.

2. Since the response header is cached in the browser, the browser checks whether the response header has expired.

3. Since the response header has not expired, the browser converts HTTP to HTTPS and sends the request to the CDN.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">If the cached <code>Strict-Transport-Security</code> response header has expired, when the user sends an HTTP request to the CDN, the steps described in the <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-hsts">HSTS</a> will be repeated.</div>


* <div data-tips="true" data-tips-type="warning">It should be noted that even if you have enabled HSTS and protocol redirect, it is not possible to completely eliminate HTTP requests received by the CDN. This is because the browser will not convert HTTP to HTTPS in the following cases:</div>


   * <div data-tips="true" data-tips-type="warning">The <code>Strict-Transport-Security</code> response header is not cached in the browser.</div>


   * <div data-tips="true" data-tips-type="warning">The <code>Strict-Transport-Security</code> response header cached in the browser has expired.</div>



<span id="a1edbb1d"></span>
## Prerequisites

To enable HSTS, you must have already enabled HTTPS for the domain name.

<span id="5868b2ce"></span>
## Configuring HSTS


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Click the **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **HTTP configuration** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **HSTS**, switch the **Status** toggle.

8. If you have not yet enabled protocol redirect, or if you have configured the request protocol but the policy is not **HTTP to HTTPS**, the CDN will ask if you want to configure the request protocol and set the policy to **HTTP to HTTPS**. The reason for this is explained in [Preconditions for the HSTS response header to take effect](https://docs.byteplus.com/docs/byteplus-vod/docs-hsts#1b8713f4).

   * If you click **Confirm**, the CDN will configure protocol redirect accordingly. Before clicking **Confirm**, please fully evaluate the impact of the "redirect HTTP requests to HTTPS" setting on your business.

   * If you click **Ignore**, the CDN will keep the current settings for protocol redirect.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/272718f0e276439bbf9ad046c0134299~tplv-goo7wpa0wc-image.image) </span>

9. Configure

   
   |**Configuration** |**Description** |
   |---|---|
   |Caching duration |Indicates the caching duration of the `Strict-Transport-Security` response header in the browser. This configuration corresponds to the `max-age` parameter in the response header. Before sending an HTTP request, the browser checks whether the cached `Strict-Transport-Security` response header has expired. If the response header has expired, the browser will not convert HTTP to HTTPS.<br><br>The maximum duration you can set is 31,536,000 seconds, which is equivalent to 365 days. If you set the expiration time to `0`, it is equivalent to disabling HSTS.<br><br>It should be noted that for each response received by the browser, if the response contains the `Strict-Transport-Security` response header, the browser will use the expiration time in the received response header to replace the expiration time in the cached response header. |
   |Subdomains |Indicates whether the HSTS configuration applies to subdomains. The possible values for this configuration are:<br><br><br>* **Do not apply**: Indicates that the HSTS configuration does not apply to subdomains.<br><br>* **Apply**: Indicates that the HSTS configuration applies to subdomains. In this case, the response header will include the `includeSubDomains` parameter.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you set <strong>Subdomains</strong> to <strong>Apply</strong>, the response header returned by the CDN informs the browser that requests sent to all subdomains must also use the HTTPS protocol. In this case, the subdomains must be accessible using the HTTPS protocol. Additionally, the subdomains should also have a similar configuration to redirect HTTP requests to HTTPS.</div><br> |
   

   **Examples**

   * Example 1: You specify an expiration time of 6 seconds and include subdomains. In this case, the response header returned by the CDN is as follows:

      * `Strict-Transport-Security: max-age=6;includeSubDomains`

   * Example 2: You specify an expiration time of 1 day and exclude subdomains. In this case, the response header returned by the CDN is as follows:

      * `Strict-Transport-Security: max-age=86400`

10. Click **Save**.


<span id="9368b848"></span>
## More information

<span id="438ca628"></span>
### How to manage HSTS configuration in browsers

The following examples use Google Chrome and Microsoft Edge to explain how to manage HSTS configuration in browsers.

In Chrome or Edge, visit the following URL:


* `chrome://net-internals/#hsts`


In the opened page, you can:


* Add a domain name to the browser's HSTS cache.

* Remove a specified domain name from the browser's HSTS cache.

* Check whether a domain name exists in the browser's HSTS cache.

   * If the domain name does not exist, the query result is `Not found`.

   * If the domain name exists, the query result will display the HSTS configuration information for that domain name. In the configuration information, `dynamic_sts_observed` indicates the time when the browser cached the domain name, in Unix timestamp format. `dynamic_sts_expiry` indicates the expiration time of the domain name in the HSTS cache.


When you query a domain name, the result data may have a delay of 1 minute.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03e06809b04a43a7af3500609e258b7f~tplv-goo7wpa0wc-image.image) </span>
