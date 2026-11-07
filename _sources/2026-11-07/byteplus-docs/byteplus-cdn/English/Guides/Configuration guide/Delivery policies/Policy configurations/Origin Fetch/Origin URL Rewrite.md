---
title: "Origin URL Rewrite"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-path-rewrite_1"
---

This document describes how to configure Origin URL Rewrite in BytePlus CDN. This feature lets you rewrite the path and query string used in origin request URLs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use this feature, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a>.</div>


<span id="overview"></span>
## Overview

Suppose that the URLs of some files on your origin have changed. You can use one of the following solutions:


* Configure a 301 or 302 redirect on the origin to redirect the original URL to the new URL, and enable [Redirect Follow](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-redirect-follow) in CDN.

* Make no changes on the origin and configure [URL Redirect](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-url-redirect) in CDN. When a user requests the original URL, CDN returns a 301 or 302 response that instructs the browser to request the new URL.

* Make no changes on the origin and configure **Origin URL Rewrite** in CDN. When a user requests the original URL, CDN uses the new URL for the origin request.


This document describes the third solution.

<span id="request-flow"></span>
## Request Flow

After a user request matches an Origin URL Rewrite rule, the request is processed as follows:


1. A user requests the file.

2. If the file is not cached, CDN rewrites the URL for the origin request according to the rule configuration and sends the origin request by using the rewritten URL.

3. After retrieving the file, CDN returns it to the user and caches it. The cache key is based on the user request URL, not the rewritten origin request URL. For more information about cache keys, see [Cache Key](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cache-keys).


<span id="steps"></span>
## Steps


1. Open the **Origin URL Rewrite** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set the **Status** to **Enabled**.

3. Click **Add**. You can configure up to 50 rules.

4. Configure the rule as described in the following sections.

5. Click **Save**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f08686ab2ed4d29933f4c846d178cb4~tplv-goo7wpa0wc-topic.webp) </span>

<span id="configuration"></span>
## Configuration


|**Configuration** |**Description** |
|---|---|
|Rewrite Type |Specifies the rewrite type. Valid values:<br><br><br>* **Path Rewrite**: Rewrites the path in the origin request URL.<br><br>* **URL Rewrite**: Rewrites the path and query string in the origin request URL. |


<span id="path-rewrite"></span>
### Path Rewrite

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec9dff63729c4a84b5b0dfadffdf1a33~tplv-goo7wpa0wc-topic.webp) </span>

When **Rewrite Type** is **Path Rewrite**, configure the following parameters:


|**Configuration** |**Description** |
|---|---|
|User Request Path |A regular expression, up to 1,024 characters, that matches the path in the user request URL. |
|Origin Path |The rewritten path in the origin request URL. It can contain up to 1,024 characters. You can use `$1`, `$2`, `$3`, and similar references to capture groups defined in **User Request Path**. |


See [Path Rewrite Examples](https://docs.byteplus.com/en/docs/18/6592#path-rewrite-examples).

<span id="url-rewrite"></span>
### URL Rewrite

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_013250c321ba724edc691e0013023a91.png) </span>

When **Rewrite Type** is **URL Rewrite**, configure the following parameters:


|**Configuration** |**Description** |
|---|---|
|Request URL |A regular expression, up to 1,024 characters, that matches the path and query string in the user request URL. |
|Origin URL |Specifies the rewritten path and query string to use in the origin request URL. It can contain up to 1,024 characters. You can use `$1`, `$2`, `$3`, and similar references to capture groups defined in **Request URL**. |


See [URL Rewrite Examples](https://docs.byteplus.com/en/docs/18/6592#url-rewrite-examples).

<span id="rule-priority"></span>
## Rule Priority

Each rule in the rule list has a priority. The rule with priority `1` has the highest priority. When CDN receives a user request, it evaluates rules in priority order, starting with priority `1`. Once a request matches a rule, CDN stops evaluating additional rules. You can drag rules to change their priorities.

<span id="examples"></span>
## Examples

<span id="path-rewrite-examples"></span>
### Path Rewrite Examples

<span id="url-rewrite-examples"></span>
### URL Rewrite Examples

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Also refer to <a href="https://docs.byteplus.com/en/docs/18/6592#path-rewrite-examples">Path Rewrite Examples</a> for considerations when using regular expressions to match paths.</div>


<span id="path-rewrite-examples"></span>
### Path Rewrite Examples


|**Request URL Path** |**User Request Path Pattern** |**Origin Path** |**Rewritten Path** |**Description** |
|---|---|---|---|---|
|`/a/bbb/image.png` |`^/a{1,2}(.*)g$`<br><br>Matches paths that begin with `/a` or `/aa` and end with `g`. |`/food/$1` |`/food//bbb/image.pn` |The regular expression matches the request path. `(.*)` captures `/bbb/image.pn`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The rewritten path contains <code>//</code>, so the path is invalid. The file extension is also incorrect.</div><br> |
|||`/food$1g` |`/food/bbb/image.png` |The regular expression matches the request path. `(.*)` captures `/bbb/image.pn`. |
|`/aaa/bbb/image.png` |`/a{1,2}(.*)g`<br><br>Matches a substring in the request path. |`/food/$1g` |`/food/a/bbb/image.png` |* The regular expression matches the request path.<br><br>* `(.*)` captures `a/bbb/image.pn`. |
|`/food/aaa/pngs/image.png` ||`/food/$1g` |`/food/a/pngs/image.png` |* The regular expression matches the request path.<br><br>* `(.*)` captures `a/pngs/image.pn`. |
|`/aaa/bbb/image.png` |`aaa(.*)`<br><br>Matches a substring in the request path. |`/food/$1g` |`/food//bbb/image.pngg` |* The regular expression matches `aaa/bbb/image.png` in the request path.<br><br>* `(.*)` captures `/bbb/image.png`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The rewritten path contains <code>//</code>, so the path is invalid. The file extension is also incorrect.</div><br> |
|`/aaa/bbb/image.png` |`aaa/(.*)`<br><br>Matches a substring in the request path. |`/food/$1` |`/food/bbb/image.png` |* The regular expression matches `aaa/bbb/image.png` in the request path.<br><br>* `(.*)` captures `bbb/image.png`. |


<span id="url-rewrite-examples"></span>
### URL Rewrite Examples

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Also refer to <a href="https://docs.byteplus.com/en/docs/18/6592#path-rewrite-examples">Path Rewrite Examples</a> for considerations when using regular expressions to match paths.</div>



|**Request URL Path and Query String** |**Request URL Pattern** |**Origin URL** |**Rewritten URL** |**Description** |
|---|---|---|---|---|
|`/a/bbb/image.png?param=val1&param2=val2` |`^/a{1,5}/(.*).png?param=(.*)`<br><br>Matches request URLs that meet all the following conditions:<br><br><br>* The request is for a `.png` file in a directory that begins with one to five `a` characters.<br><br>* The first query parameter is `param`. |`/food/$1.png?param5=$2&size=6` |`/food/bbb/image.png?param5=val1&param2=val2&size=6` |The first `(.*)` captures `bbb/image`. The second `(.*)` captures `val1&param2=val2`. |
