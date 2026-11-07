---
title: "IP Restrictions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-ip-restrictions"
---

To control which users can access your content delivered via BytePlus CDN, you can configure IP Restrictions.

This feature allows you to create an allowlist or a blocklist to filter requests based on the client's IP address.

<span id="restrictions-priority"></span>
## Restrictions Priority

CDN access restriction features have different priorities. When CDN processes user requests, these restrictions are applied in order of priority. Refer to [Access Restrictions Priority](https://docs.byteplus.com/en/docs/byteplus-cdn/access-control-priorities_en).

<span id="steps"></span>
## Steps


1. Open the **IP Restrictions** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to Enable.

3. Refer to the following configuration instructions.

4. After you configure the settings, click **Save**.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260828100622-190633119922.png) </span>

<span id="configuration-instructions"></span>
## Configuration Instructions


|Configuration |Description |
|---|---|
|Filter |This setting has the following options:<br><br><br>* **Allowlist**: Specifies which IP addresses are allowed to access your domain.<br><br>* **Blocklist**: Specifies which IP addresses are not allowed to access your domain.<br><br><br>If the source IP of a request matches the blocklist or does not match the allowlist, CDN will reject the request and return a 403 response code. |
|List Source |Indicates the source of the entries in the list. This configuration has the following options:<br><br><br>* Policy\-based List: Indicates that the entries in the list are configured in **IP Addresses**.<br><br>* Universal Catalog: Indicates that the entries in the list come from a [Universal Catalog](https://docs.byteplus.com/en/docs/byteplus-cdn/global-catalog_en). A universal catalog is used to define a large number of entries. A universal catalog can contain up to 30,000 entries. |
|IP Addresses |This field lists the IP addresses for the selected **Filter** type. You can add up to 1,000 entries, with a total length of up to 30,000 characters. This field appears when **List Source** is set to **Policy\-based List**.<br><br>Each entry can be an IP address, a CIDR block, or an IP address range. Only IPv4 addresses are supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the number of IP addresses you need to input exceeds 1,000, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/global-catalog_en">Universal Catalog</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>0.0.0.0/0</code> is not supported. To specify all IP addresses, enter both of the following CIDR blocks:</div><br><br><br>   <div data-tips="true" data-tips-type="tip"><code>0.0.0.0/1</code>   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip"><code>128.0.0.0/1</code>   </div><br>    |
|Client IP Source |Specifies the source that CDN uses to determine the client IP address.<br><br>&nbsp;<br><br>The following options are available:<br><br><br>* **Default**: CDN uses the actual connection IP to determine the client IP address. The actual connection IP is the IP address of the peer that directly establishes a network connection with the CDN node.<br><br>* **Custom**: Select one or more sources from the actual connection IP, the `X-Forwarded-For` header, and the `X-Real-IP` header to determine the client IP address. If CDN cannot obtain an IP address from a selected header, it uses the actual connection IP.<br><br>   * For an IP blocklist, CDN rejects the request if any IP address obtained from the selected sources matches a rule.<br><br>   * For an IP allowlist, CDN allows the request only if all IP addresses obtained from the selected sources match rules. |
|Response Status Code |Specifies the status code CDN returns when it denies a request. Valid values range from 200 to 999. If you do not configure this setting, CDN returns 403 by default. |


<span id="configuration-examples"></span>
## Configuration Examples

**Allowlist**

IP Addresses:

> 192.0.2.0/24

> 203.0.113.8\-203.0.113.15


Effect: Only allows IP addresses that meet any of the following conditions to send requests to your domain:


* The IP address is within the range of 192.0.2.1\-192.0.2.254 or 203.0.113.8\-203.0.113.15.


**Blocklist**

IP Addresses:

> 198.51.100.25


Effect: If the IP address meets any of the following conditions, requests from that IP address are not allowed.


* The IP address is 198.51.100.25.
