---
title: "Origin restrictions"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-origin-restrictions"
---

To prevent hotlinking and control which websites can access your content, you can configure Origin restrictions. This guide provides step\-by\-step instructions on how to set up an allowlist or a blocklist for your **Playback**, **Image**, and **Custom\-origin domain names** in the BytePlus VOD console.

<span id="6be48874"></span>
## Introduction

Origin is a request header in the HTTP request, indicating which site the request comes from. The Origin header contains protocol, domain name and port, but does not contain path and query parameters. Port number is optional.

One of the purposes of the Origin header is to prevent hotlinking. You can configure an Origin blocklist for your site to deny requests from specified domains. Or you can configure an Origin allowlist for your site to only accept requests from specified domains.

<span id="04037046"></span>
### **Empty Origin**

"Empty Origin" is defined as no value for the Origin header or no Origin header included in the request.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>Origin: null</code> is not considered a "null Origin" case.</div>


<span id="74be44b4"></span>
## Configuring the Origin allowlist and blocklist


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Depending on the type of your domain name, click the **Playback domain name**, **Image domain name**, or **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Access control** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **Origin allowlist and blocklist**, switch the **Status** toggle and configure the Origin restrictions:

   
   |**Configuration** |**Description** |
   |---|---|
   |Type |This configuration has the following options:<br><br><br>* **Allowlist**: You can configure an allowlist when you only want to allow requests from certain sites. If the user's request does not match the allowlist, CDN rejects the request and responds with a 403 status code<br><br>* **Blocklist**: When you only want to block requests from certain sites, you can configure a blocklist. If the user's request matches the blocklist, CDN rejects the request and responds with a 403 status code. |
   |Allowing empty Origin |Specifies whether to accept requests with no value for the Origin header or requests that do not contain the Origin header. |
   |List |Enter one or more list entries. List length cannot exceed 30,000 characters. You can enter one or more domain names (including subdomain names and wildcard domain names) and IP addresses (including IPv4 addresses, IPv6 addresses, and CIDR network segments). Multiple entries are separated with semicolons (;) or newlines. You can enter up to 1,000 entries. It should be noted that a second\-level domain name is a single domain name, not a wildcard domain name. A wildcard domain entry does not match the second\-level domain itself. For example: \*.test.com does not match the second\-level domain name test.com, but matches www.test.com, a.a.test.com, etc.<br><br>There is no limit to the number of levels a subdomain can have. For the matching logic of the Origin list, see [Origin matching logic](https://docs.byteplus.com/docs/byteplus-vod/docs-origin-restrictions#2843a66a). |
   

8. Click **Save**.


<span id="2843a66a"></span>
## Origin matching logic

Let's use the following configuration as an example to illustrate the matching logic of the Origin header. If a request does not match the allowlist or matches the blocklist, BytePlus VOD rejects the request and returns a 403 response status code.


|**Configuration** |**Origin header in user request** |**Matching or not** |**Matching logic description** |
|---|---|---|---|
|* www.test.com<br><br>* 1.1.1.1<br><br>* 2001:0db8:3c4d:0015:0000:0000:1a2f:1a2b<br><br>* \*.test.com |http://www.test.com |Yes |The domain in the Origin header matches an entry in the list. |
||http://www.test.com:80 |Yes ||
||www.test.com |No |The Origin header does not conform to the HTTP protocol specification. The specification requires that the Origin header value must be in one of the following formats:<br><br><br>* scheme://host:port<br><br>* scheme://host |
||2001:0db8:3c4d:0015:0000:0000:1a2f:1a2b |No ||
||http://2001:0db8:3c4d:0015:0000:0000:1a2f:1a2b |No |The Origin header does not conform to the HTTP protocol specification. The specification requires that when host is an IPv6 address, the address must be wrapped in `[]`. |
||http://[2001:0db8:3c4d:0015:0000:0000:1a2f:1a2b] |Yes |The IP address in the Origin header matches the list. |
||http://aaa.test.com |Yes |The multi\-level domain name in the Origin header matches the wildcard entry in the list. Wildcard domain entries match multi\-level domain names. |
||http://ss.aaa.test.com |Yes ||
||http://test.com |No |The second\-level domain in the Origin header does not match the wildcard entry in the list. The reason is that a wildcard domain entry does not match the second\-level domain name itself. |
