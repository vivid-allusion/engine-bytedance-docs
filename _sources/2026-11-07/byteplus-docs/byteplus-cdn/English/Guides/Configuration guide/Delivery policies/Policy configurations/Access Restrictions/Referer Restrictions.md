---
title: "Referer Restrictions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-referer-restrictions"
---

<span id="referer-restrictions"></span>
## Referer Restrictions

In BytePlus CDN, you can configure "Referer Restrictions" to block requests containing specific Referers from accessing the CDN, thereby preventing your website content from being hotlinked.

If a user request is rejected by CDN due to your "Referer Restrictions" configuration, CDN responds with a 403 status code.

<span id="notes"></span>
## Notes

When a user request is rejected by the CDN, the following metrics are still recorded:


* The CDN's response is counted as outbound data transfer, although the amount of data is minimal.

* Rejected HTTPS requests are still counted towards billing.


<span id="introduction-to-referer"></span>
## Introduction to Referer

Referer is a header in HTTP requests used to record the source page of the request. Generally, a Referer is a complete URL, including scheme, domain, path, and query string.

When you click a link on webpage A, the browser sends an HTTP request to the target page of the link. The request includes a Referer header, and the header value is the URL of webpage A.

<span id="empty-referer"></span>
### Empty Referer

An empty Referer is an HTTP request that lacks a Referer header. In "Referer Restrictions," you can configure how CDN handles user requests that do not include a Referer header.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>Referer: null</code> is not regarded as an "Empty Referer".</div>


<span id="dd7d2017"></span>
## Steps

**Empty Referer Scenarios**

Typically, an empty Referer appears in any of the following scenarios:


* You access the target page through a bookmark in your browser.

* You enter a URL in your browser's address bar to access the target page.

* You click a link on an HTTPS page to access an HTTP page.

* You use the private browsing mode provided by your browser.

* If the page you visit meets any of the following conditions, when you click any link on that page, the HTTP request will not include a Referer header:

   * The page's `<meta>` tag declares `Referrer-Policy: no-referrer`.

   * The server's response for the page has a `Referrer-Policy: no-referrer` header.


<span id="restrictions-priority"></span>
## Restrictions Priority

CDN access restriction features have different priorities. When CDN processes user requests, these restrictions are applied in order of priority. Refer to [Access Restrictions Priority](https://docs.byteplus.com/en/docs/byteplus-cdn/access-control-priorities_en).

<span id="steps"></span>
## Steps


1. Open the **Referer Restrictions** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to Enable.

3. Refer to the following configuration instructions.

4. After configuring, click **Save**.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f0734d6f3ea80058b62c85eb3bb9fc33.png) </span>

<span id="configuration-instructions"></span>
## Configuration Instructions


|Configuration |Description |
|---|---|
|Filter |Specifies the type of list. This configuration has the following options:<br><br><br>* **Allowlist**: Specifies an allowlist. If the Referer in a user request does not match this list, CDN will reject the request.<br><br>* **Blocklist**: Specifies a blocklist. If the Referer in a user request matches this list, CDN will reject the request. |
|List Source |Indicates the source of entries in the list. This configuration has the following options:<br><br><br>* Policy\-based List: Indicates that the entries in the list are configured in **Regular List** and **RegEx List**.<br><br>* Universal Catalog: The list entries are sourced from a [Universal Catalog](https://docs.byteplus.com/en/docs/byteplus-cdn/global-catalog_en). Universal catalogs are used to define a large number of entries. A universal catalog can contain up to 4,000 entries. |
|List Options |Indicates the configuration options for the list, including:<br><br><br>* Regular List: Each entry in the list is an IP address or domain name, used to match and verify the hostname in the Referer.<br><br>* RegEx List: Each entry in the list is a regular expression, used to match and verify the complete URL in the Referer.<br><br>* Empty Referer: Indicates how CDN handles requests when user requests do not include a Referer header. This configuration has the following options:<br><br>   * Enable: Indicates that if a request does not include a Referer header, the request is considered to **match** the list you configured.<br><br>   * Disable: Indicates that if a request does not include a Referer header, the request is considered **not to match** the list you configured. |
|Regular List (Input Box) |Represents a regular list. If you checked **Regular List** under **List Options**, this input box will appear.<br><br>**Input Requirements**<br><br>The list can contain up to 1,000 entries, with a total length not exceeding 30,000 characters. You can enter one or more domain names and IP addresses. Domain names can be wildcard domains. IP addresses can only be IPv4 addresses or IPv4 CIDR addresses. Multiple entries are separated by semicolons (;) or each entry on a new line.<br><br>If you need to enter more than 1,000 entries, refer to [Universal Catalog](https://docs.byteplus.com/en/docs/byteplus-cdn/global-catalog_en).<br><br>**About Wildcard Domains and Subdomains**<br><br><br>* Wildcard domains do not match the domain itself. For example: `*.example.com` does not match `example.com`, but matches `www.example.com`, `a.a.example.com`, etc.<br><br>* There is no limit to the number of levels in a subdomain. For example, you can specify `aaa.bbb.ccc.ddd.eee.fff.ggg.eee.example.com` in the list. |
|Ignore Case |Indicates whether the entries in the regular list are case\-sensitive. |
|Skip Scheme Validation |Indicates whether CDN verifies the scheme in the Referer, that is, whether the Referer includes `http://` or `https://`. This configuration has the following options:<br><br><br>* Enable: Indicates that CDN does not verify whether the Referer includes a scheme. In this case, regardless of whether the Referer includes a scheme, CDN will match and verify the Referer against the list you configured.<br><br>* Disable: Indicates that CDN will first verify whether the Referer includes a scheme. CDN only checks the Referer against your configured list if the Referer includes a scheme. Otherwise, the request is considered not to match.<br><br><br>This configuration does not apply to **RegEx List**, as CDN relies on regular expressions to determine whether a Referer matches the RegEx list. |
|RegEx List (Input Box) |Represents a regular expression list, used to match and verify the complete URL in the Referer. You can specify up to 100 regular expressions, with each regular expression on a new line. If you checked **RegEx List** under **List Options**, this input box will appear. Entries in the RegEx list are not case\-sensitive. |


<span id="configuration-examples"></span>
## Configuration Examples

Suppose your configured list includes the following entries:


* www.example.com

* \*.example.com


The related settings and matching results are shown in the table below:


|**Filter** |**Referer in User Request** |**Ignore Case** |**Skip Scheme Validation** |**Empty Referer** |**Matching Result** |
|---|---|---|---|---|---|
|Blocklist |https://www.eXampLe.com/file?p=v |Enabled |N/A ||Reject Request |
|||Disabled |||Accept Request |
||www.example.com/file?p=v |N/A |Enabled |N/A |Reject Request |
||||Disabled ||Accept Request |
||Does not include Referer header |N/A ||Enabled |Reject Request |
|||||Disabled |Accept Request |
||https://www.example.com |N/A |||Reject Request |
||https://docs.www.example.com ||||Reject Request |
||https://example.com ||||Accept Request |
|Allowlist |https://www.eXampLe.com/file?p=v |Enabled |N/A ||Accept Request |
|||Disabled |||Reject Request |
||www.example.com/file?p=v |N/A |Enabled |N/A |Accept Request |
||||Disabled ||Reject Request |
||Does not include Referer header |N/A ||Enabled |Accept Request |
|||||Disabled |Reject Request |
||https://www.example.com |N/A |||Accept Request |
||https://docs.www.example.com ||||Accept Request |
||https://example.com ||||Reject Request |
