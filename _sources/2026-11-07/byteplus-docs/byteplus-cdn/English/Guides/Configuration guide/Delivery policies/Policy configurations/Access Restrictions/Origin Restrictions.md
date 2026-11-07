---
title: "Origin Restrictions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-restrictions"
---

To prevent unauthorized hotlinking and control access to your CDN resources, you can configure Origin restrictions. This guide shows you how to set up an allowlist or a blocklist to filter requests based on their Origin header.

The Origin is an HTTP request header that indicates the domain the request originates from. The Origin header includes the protocol, domain, and port, but it does not include the path and query string. The port number is optional.

<span id="hotlinking-prevention"></span>
## Origin Restrictions

One of the uses of the Origin header is to prevent hotlinking. You can configure an origin blocklist to reject requests from specified domains for your site. Alternatively, you can configure an origin allowlist that only accepts requests from specified domains.

<span id="about-empty-origin"></span>
### **Empty Origin**

An empty origin is defined as a request where the Origin header has no value or the request does not contain an Origin header.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>Origin: null</code> is not regarded as an empty origin.</div>


<span id="steps"></span>
## Steps


1. Open the **Origin Restrictions** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to **Enable**.

3. Refer to the following configuration instructions.

4. After configuring, click **Save**.



|**Configuration** |**Description** |
|---|---|
|Filter |The configuration has the following options:<br><br><br>* **Allowlist**: Configure an allowlist when you only want to allow requests from certain domains. If a user's request does not match the allowlist, the CDN will deny the request and respond with a 403 status code.<br><br>* **Blocklist**: Configure a blocklist when you only want to prevent requests from certain domains. If a user's request matches the blocklist, the CDN will deny the request and respond with a 403 status code. |
|Origins |Enter up to 100 origins, with a total length not exceeding 30,000 characters. Supported entries include domain names (with subdomain and wildcard support) and IP addresses (IPv4, IPv6, and CIDR blocks). Separate multiple entries with a semicolon (;) or a new line. A wildcard entry, such as \*.test.com, matches its subdomains (for example, www.test.com and abc.wwww.test.com) but does not match the base domain itself (test.com).<br><br>&nbsp;<br><br>The number of levels in a subdomain is not limited. For the matching logic of the origin list, see [Origin Matching Logic](https://docs.byteplus.com/en/docs/18/6562#origin-matching-logic). |
|Requests with Empty Origin |Specifies how the CDN handles requests in an [Empty Origin](https://docs.byteplus.com/en/docs/18/6562#empty-origin) scenario.<br><br><br>* If **Filter** is **Blocklist**, this option is **Allow Requests with Empty Origin**.<br><br>* If **Filter** is **Allowlist**, this option is **Deny Requests with Empty Origin**. |
|Ignore Case |Indicates whether Origin is case\-sensitive when used to filter requests. |


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22cc40aeb09245ffad1208c7a5a5c1b9~tplv-goo7wpa0wc-image.image) </span>

<span id="origin-matching-logic"></span>
## Origin Matching Logic

We explain the matching logic of the Origin header using the following list configuration as an example. If a request does not match the allowlist or matches the blocklist, the CDN will deny the request and return a 403 response status code.


|**List Configuration** |**User Request's Origin Header** |**Match?**  |**Comment** |
|---|---|---|---|
|* www.test.com<br><br>* 1.1.1.1<br><br>* 2001:0db8:3c4d:0015:0000:0000:1a2f:1a2b<br><br>* \*.test.com |http://www.test.com |Yes |The domain in the Origin header matches the list. |
||http://www.test.com:80 |Yes ||
||www.test.com |No |The Origin header does not conform to the HTTP protocol specification. The specification requires the Origin header value to be in one of the following formats:<br><br><br>* scheme://host:port<br><br>* scheme://host |
||2001:0db8:3c4d:0015:0000:0000:1a2f:1a2b |No ||
||http://2001:0db8:3c4d:0015:0000:0000:1a2f:1a2b |No |The Origin header does not conform to the HTTP protocol specification. The specification requires that when the host is an IPv6 address, the address must be enclosed in `[]`. |
||http://[2001:0db8:3c4d:0015:0000:0000:1a2f:1a2b] |Yes |The IP address in the Origin header matches the list. |
||http://aaa.test.com |Yes |The subdomain in the Origin header matches the wildcard domain entry in the list. |
||http://ss.aaa.test.com |Yes ||
||http://test.com |No |The base domain in the Origin header does not match the wildcard entry, because a wildcard pattern like \*.test.com does not match the base domain test.com. |
