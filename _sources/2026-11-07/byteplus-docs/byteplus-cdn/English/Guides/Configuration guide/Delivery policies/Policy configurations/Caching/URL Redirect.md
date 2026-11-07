---
title: "URL Redirect"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-url-redirect"
---

With URL Redirect, you can configure CDN to return a `3xx` redirect response when a request path matches a rule. The client then sends a request to the redirect URL.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use this feature, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a>.</div>


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260916085316-903390514182.png) </span>

<span id="use-cases"></span>
## Use cases

When a frequently accessed content path changes, you can use one of the following approaches:


* Configure a redirect at the origin and enable [Redirect Follow](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-redirect-follow) in CDN.

* Configure **URL Redirect** in CDN. CDN returns a `3xx` response, and the client requests the redirect URL.

* Configure [Origin URL Rewrite](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-path-rewrite_1) in CDN. CDN uses the rewritten path only for origin requests; the client URL does not change.


This document describes the second approach.

<span id="notes"></span>
## Notes


* Ensure that the redirected URL does not match the current rule or another **URL Redirect** rule. CDN does not prevent redirect loops. If a loop occurs, the client continues to receive `3xx` responses until it reaches its redirect limit.

* If you set **Redirect Host** to a domain that is not accelerated by CDN, requests to the redirect URL are not accelerated.

* **Redirect Path** cannot contain consecutive slashes (`//`), percent signs (`%`), spaces, or question marks (`?`).


<span id="matching-and-replacement"></span>
## Matching and replacement

**Path Pattern** is a regular expression used to match the path in a request URL. It can contain up to 1,024 characters. **Redirect Path** is a replacement string that substitutes the content matched by **Path Pattern**.


* Without `^` and `$`, **Path Pattern** can match part of a path. CDN replaces only the matched content and retains unmatched prefixes and suffixes.

* With `^` and `$`, **Path Pattern** matches the entire path only.

* You can use capture groups in the regular expression. `$1`, `$2`, and so on represent the content matched by the first, second, and subsequent groups.


For example, for the request path `/old/images/logo.png`, set **Path Pattern** to `^/old/(.*)$` and **Redirect Path** to `/new/$1`. The resulting redirect path is `/new/images/logo.png`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">CDN uses <strong>Redirect Path</strong> to replace only the content matched by the regular expression; it does not necessarily replace the entire path. This differs from <strong>CDN Origin Path</strong> in <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-path-rewrite_1">Origin URL Rewrite</a>, which replaces the entire request path.</div>


<span id="steps"></span>
## Steps


1. Open the **URL Redirect** configuration page. For details, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Click **Add**.

   You can add up to 50 rules.

3. Configure the rule as described in [Configuration](https://docs.byteplus.com/en/docs/18/6579#configuration).

4. Click **OK**.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260916085145-1243604186324.png) </span>

<span id="configuration"></span>
## Configuration


|Setting |Description |
|---|---|
|Path Pattern |A regular expression used to match the path in a request URL. It supports capture groups and can contain up to 1,024 characters. For details, see [Matching and replacement](https://docs.byteplus.com/en/docs/18/6579#matching-and-replacement). |
|Redirect Status Code |The redirect status code returned by CDN. Available options are `301`, `302`, `303`, `307`, and `308`.<br><br>&nbsp;<br><br>Use `301` or `308` for permanent changes, and `302` or `307` for temporary redirects. `303` requires the client to use `GET` for the redirect URL. For `301` and `302`, clients might change a non\-`GET` request to `GET` when requesting the redirect URL. For `307` and `308`, clients retain the original request method. |
|Redirect Protocol |The protocol for the redirect URL.<br><br><br>* **Follow Request**: Uses the protocol of the original request.<br><br>* **HTTP**: Uses HTTP.<br><br>* **HTTPS**: Uses HTTPS. |
|Redirect Host |The domain name or IPv4 address in the redirect URL. The IP address must be an IPv4 address. A domain name can contain up to 1,024 characters. |
|Redirect Path |The replacement string for matched content. It can contain up to 1,024 characters and cannot contain consecutive slashes (`//`), percent signs (`%`), spaces, or question marks (`?`). |
|Parameter Handling |Specifies how query parameters in the redirect URL are handled.<br><br><br>* **Retain All**: Retains all query parameters from the original request.<br><br>* **Retain None**: Removes all query parameters from the original request.<br><br>* **Retain Specified**: Retains only parameters with specified names.<br><br>* **Retain All Except**: Removes parameters with specified names and retains the remaining query parameters. |
|Parameter Name |When **Parameter Handling** is set to **Retain Specified**, enter the parameter names to retain. When it is set to **Retain All Except**, enter the parameter names to remove. Separate multiple names with semicolons (`;`). The value can contain up to 1,024 characters and cannot contain consecutive slashes (`//`), percent signs (`%`), double quotation marks (`"`), or spaces. |


<span id="rule-priority"></span>
## Rule priority

Rules closer to the top of the list have higher priority. CDN evaluates rules from top to bottom. After a request matches a rule, CDN applies that rule and stops evaluating subsequent rules.

Place more specific rules above more general rules. For example, place `^/images/logo/(.*)$` above `^/images/(.*)$`; otherwise, a request for `/images/logo/a.png` matches the more general rule first.

You can drag rules to change their order.

<span id="examples"></span>
## Examples

<span id="match-an-entire-path"></span>
### Match an entire path

With the following rule, CDN redirects requests under `/old/images/` to `/new/images/`.


|Setting |Value |
|---|---|
|Path Pattern |`^/old/images/(.*)$` |
|Redirect Path |`/new/images/$1` |


CDN redirects `https://example.com/old/images/logo.png` to `https://example.com/new/images/logo.png`.

<span id="replace-part-of-a-path"></span>
### Replace part of a path

With the following rule, CDN replaces only the matched `legacy/` portion of a path. It retains the unmatched path prefix.


|Setting |Value |
|---|---|
|Path Pattern |`legacy/(.*)` |
|Redirect Path |`modern/$1` |


CDN redirects `https://example.com/static/legacy/logo.png` to `https://example.com/static/modern/logo.png`.

<span id="filter-query-parameters"></span>
### Filter query parameters

With the following rule, CDN retains only the query parameter named `keep`.


|Setting |Value |
|---|---|
|Path Pattern |`^/old$` |
|Redirect Path |`/new` |
|Parameter Handling |**Retain Specified** |
|Parameter Name |`keep` |


CDN redirects `https://example.com/old?keep=1&drop=2` to `https://example.com/new?keep=1`.
