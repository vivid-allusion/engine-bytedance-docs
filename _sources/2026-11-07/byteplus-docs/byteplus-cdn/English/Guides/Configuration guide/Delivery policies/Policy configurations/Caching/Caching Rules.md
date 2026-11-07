---
title: "Caching Rules"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-caching-rules"
---

This document describes the Caching Rules in BytePlus CDN.

<span id="overview"></span>
## Overview of Caching Rules

To optimize content delivery and reduce origin load, you can use Caching Rules to customize how BytePlus CDN caches your files. While the CDN defaults to caching based on your origin's headers, these rules allow you to override that behavior. This guide explains what Caching Rules are, their different policies, and how to create them to control cache duration for specific file types or URL paths.

If you need to modify the CDN's caching behavior for specific requests, you can create Caching Rules in the CDN. For example, you can create a Caching Rule to have the CDN always cache requested files for 3 days for requests that meet the following conditions:


* The path directory in the request URL is `/img/loca-food/`.

* The file name starts with `Chinese`.

* The file extension is `.png`.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The CDN caches the complete origin response, including the file, status code, and headers.</div>


* <div data-tips="true" data-tips-type="tip">When caching a file, the CDN records the value of the <code>Date</code> header from the origin response as the file's caching timestamp.</div>


* <div data-tips="true" data-tips-type="tip">A request is considered a cache hit if the requested file is present in the CDN cache and has not expired.</div>



<span id="caching-behavior"></span>
## Caching Behavior

The following table describes how each policy in the Caching Rules affects caching behavior.


|**Caching policy** |**Policy configuration** |**Caching behavior** |
|---|---|---|
|Follow CDN |Always Cache (On) |Always caches files and follows the cache TTL in the rule. |
||Always Cache (Off) |* If the origin response header contains `Cache-Control: no-store/private/no-cache`, files are not cached.<br><br>* In all other cases, files are cached according to the cache TTL in the rule. |
|Follow origin |Use Specified TTL (On) |* Follows the Cache\-Control or Expires in the origin's response headers.<br><br>* If Cache\-Control and Expires are not present, the file is cached according to the cache TTL in the rule. |
||Use Specified TTL (Off) |* Follows the Cache\-Control or Expires in the origin's response headers.<br><br>* If Cache\-Control and Expires are not present, the file is not cached. |
|Do Not Cache |N/A |Never caches files. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the origin response header contains both <code>Cache-Control: max-age</code> and <code>Cache-Control: s-maxage</code>, the latter has higher priority.</div>


<span id="create-rule"></span>
## Create Caching Rules


1. Open the **Caching Rules** configuration page. For the steps, see [Domain Name Configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Click **Add Rule**.

   You can add up to 50 rules.

3. Refer to the following [Configuration Instructions](https://docs.byteplus.com/en/docs/18/6577#configuration-instructions).

4. After completing the configuration, click **Save**.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260410072623-720002302304.png) </span>

<span id="configuration-instructions"></span>
### **Configuration Instructions**


|**Configuration** |**Description** |
|---|---|
|Priority |Indicates the priority of the rule. Rule 1 has the highest priority. You can adjust the rule priority by dragging. |
|Filter Type |Indicates the matching conditions for the rule. This configuration has the following options:<br><br><br>* **URL Path Extension**: Indicates the extension at the end of a URL path.<br><br>* **URL Path Directory**: A directory in the URL path.<br><br>* **URL Path**: The complete URL path.<br><br>* **Path RegEx**: A regular expression for matching the complete URL path. |
|Patterns |Specifies the value to match. Separate multiple values with a semicolon (;). The total length cannot exceed 1,024 characters and cannot contain the following characters:<br><br><br>* Double slashes (//), spaces, dollar signs ($), and question marks (?).<br><br><br>Additionally,<br><br><br>* If the **Filter Type** is **URL Path Extension**, each match value is a file extension and cannot start with a period (.). For example: `png;txt`.<br><br>* If the **Filter Type** is **URL Path Directory**, each match value is a directory path that must begin and end with a forward slash (/). For example: `/chs/foods/;/us/birds/`.<br><br>* If the **Filter Type** is **URL Path**, each match value is a URL path that must begin with a forward slash (/). A match value can contain an asterisk (\*) to represent one or more arbitrary characters. For example: `/chs/foods/local*sets;/us/birds/chickadee`.<br><br>* If the **Filter Type** is **Path RegEx**, each match value is a regular expression used to match a URL path. For example: `^/a{1,2}.*g$`. |
|Ignore Case |Specifies whether the match value is case\-sensitive. The default setting is **Off**, meaning the match value is case\-sensitive. For example: If the **Filter Type** is **URL Path Extension**, the patterns are `png;txt`, and **Ignore Case** is **Off**. In this case, the rule matches a request with the URL `HTTPS://www.EXAMPLE.com/image.png` but not a request with the URL `https://www.example.com/image.PNG`. |
|Bypass Cache on Set\-Cookie |Specifies whether to cache origin responses that contain the `Set-Cookie` header. By default, this switch is disabled, meaning the CDN will cache such responses.<br><br>&nbsp;<br><br>Since the `Set-Cookie` header typically contains user\-specific information such as identity credentials or personalized configurations, caching these responses may pose security risks related to user identity confusion. If the origin response contains the `Set-Cookie` header, please thoroughly evaluate the security of caching such responses.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If <strong>Policy configuration</strong> is set to <strong>Always Cache (On)</strong>, you cannot configure <strong>Bypass Cache on Set\-Cookie</strong>. Origin responses containing the <code>Set-Cookie</code> header will be cached by the CDN.</div><br> |
|Caching Policy |Describes the CDN caching behavior. See [Caching behavior](https://docs.byteplus.com/en/docs/18/6577#caching-behavior). |
|Policy Setting ||
|Cache TTL |Specifies the cache TTL for a file. The maximum cache TTL is 3,650 days.<br><br>If the cache TTL is set to `0`, files are not cached. This is equivalent to setting the **Caching Policy** to **Do Not Cache**. For user requests that match this rule, CDN passes them through to the origin. |


<span id="add00773"></span>
## How Rules Take Effect

Rules in the list are prioritized, and the rule with the highest priority is applied first. When a user request matches a rule, only that rule is applied, and the remaining rules are ignored. You can drag rules to adjust their priority.

<span id="8990e788"></span>
## **More Information**

<span id="848521a7"></span>
### Default Caching Rule

The Caching Rules list contains a system\-created rule. This default caching rule applies to all requests. The rule is configured as "Follow Origin + Use Specified TTL (Off)". This rule has the lowest priority. You cannot modify, delete, or adjust the priority of this rule.

If a user request does not match any of your created caching rules, it will match this system\-created rule.

<span id="47c480c4"></span>
### How the CDN Determines if a Cached File Has Expired

When the CDN receives a user request, if the requested file is already cached by the CDN and the following condition is met, the CDN determines that the cache has not expired and sends the cached file to the user:


* Request reception time \> File cache time + Cache TTL specified in the matching caching rule


<span id="ce6c680c"></span>
### How Caching Rules Affect Request Handling

When the CDN receives a user request, it processes the request in the following steps:


1. The CDN determines the Caching Rule that matches the user request.

2. Based on the Caching Rule's configuration, it determines whether to search for the file in the cache.

   * If the Caching Rule is configured not to cache the file, the CDN requests the file directly from the origin. After receiving the file, the CDN sends it to the user. **The process ends.** 

   * Otherwise, the CDN searches for the file in the cache.

3. It then determines if the file exists in the cache.

   * If the file exists and has not expired, the CDN sends the cached file to the user. **The process ends.** 

   * If the file exists but has expired, the CDN performs [origin validation](https://docs.byteplus.com/en/docs/18/6577#origin-validation) to check with the origin for updates. The origin validation has one of the following outcomes:

      * The file on the origin has not been updated: The CDN sends the cached file to the user. **The process ends.** 

      * The file on the origin has been updated: The origin's response contains the latest file. Continue to step 4.

   * If the file does not exist, the CDN requests the file from the origin. Continue to step 4.

4. After receiving the file, the CDN sends it to the user.

5. The CDN caches the received file based on the matched caching rule.


<span id="2702473f"></span>
### Cache Expiration for File Fragments

When the CDN receives a Range request for a cached fragment, it uses the following steps to determine if the fragment has expired:


1. Find all cached fragments of the file corresponding to the requested fragment.

2. Among these fragments (including the complete file, if it exists), identify the one that was cached first and get its caching timestamp.

3. Use the following formula to calculate the expiration time of the requested fragment:

   * Expiration time = Caching timestamp from Step 2 + Cache TTL specified in the caching rule that matches the Range request.

4. Determine if the cached fragment has expired.

   * If the CDN receives the Range request after the expiration time from Step 3, it determines that the cached fragment has expired.

   * Otherwise, the CDN determines that the cached fragment has not expired.


**Example**

The CDN receives the following requests for a file on the origin server at different times on a given day:


* 09:00: The CDN receives a request for fragment A of the file. Fragment A is cached at 09:01.

* 10:00: The CDN receives a request for fragment B. Fragment B is cached at 10:01.

* 11:00: The CDN receives a request for the complete file. The complete file is cached at 11:01.

* 13:02: The CDN receives another request for fragment B.


For the last request, assume the matching Caching Rule specifies a cache TTL of 4 hours. Since the cache expiration time is 13:01, the CDN determines that the cached fragment B has expired.

<span id="26907f71"></span>
### When the CDN does not cache origin responses

The CDN **does not** cache origin responses in any of the following situations. Also, you cannot use Caching Rules to change the CDN's behavior.


* The value of the `Content-Length` header in the origin response is `0`.

* The request method is neither GET nor HEAD.

* The origin response status code is not 2xx, and you have not configured [Negative Caching](https://docs.byteplus.com/zh-CN/docs/byteplus-cdn/docs-negative-caching) for that status code.

* The request uses the HEAD method, and the origin response includes the `Transfer-Encoding:chunked` header.


In the following situations, the CDN does not cache origin responses by default. However, you can create Caching Rules to change the CDN's caching behavior.


* The origin response includes an `Expires` header with a value that indicates a time before the CDN received the user request.


<span id="0453fd47"></span>
### **Forcing a cache update**

Suppose a file in the CDN cache has not expired, but the file on the origin has been updated. You want users to get the latest version of the file.

In this case, you can perform a [purge](https://docs.byteplus.com/zh-CN/docs/byteplus-cdn/docs-purge) operation on the file in the CDN. A purge operation forces the CDN to mark the file as expired. Then, if the CDN receives a request for the file, it performs an [origin validation](https://docs.byteplus.com/en/docs/18/6577#origin-validation). After retrieving the updated file, the CDN sends it to the user and caches it.

<span id="eb911957"></span>
### **Origin validation**

When a cached file expires and the CDN receives a request for it, the CDN requests the file from the origin. However, if the origin's response headers cached with the file contain an `ETag` or `Last-Modified`, the CDN includes the corresponding headers in the origin request. These headers are used to verify with the origin if the file has been updated. The origin validation logic is as follows:


* If an `ETag` exists, the origin request includes an `If-None-Match` header. The value of this header is the value of the `ETag`.

* If an `ETag` does not exist but a `Last-Modified` does, the origin request includes an `If-Modified-Since` header. The value of this header is the value of the `Last-Modified`.


When the origin server receives a request that contains an `If-None-Match` or `If-Modified-Since` header, it checks whether the file has been updated based on that header.


* If the file has been updated, the origin response includes the requested file, and the response status code is 200.

* If the file has not been updated, the origin response does not contain the requested file, and the response status code is 304.


Based on the status code in the origin response, the CDN performs one of the following actions:


* If the status code is 304, the CDN sends the cached file to the user. Meanwhile, the CDN retrieves the Date header from the origin response and updates the file's caching timestamp with this value.

* If the status code is 200, the CDN sends the updated file to the user and caches the updated file.
