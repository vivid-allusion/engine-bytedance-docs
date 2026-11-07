---
title: "Caching rules"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-caching-rule"
---

Caching rules in BytePlus VOD are a set of instructions that control how content is stored on CDN edge nodes and for how long. By configuring these rules, you can optimize content delivery, reduce origin server load, and ensure users receive the most up\-to\-date files. This document explains the caching mechanism, details the available caching policies, and provides step\-by\-step instructions for creating your own custom rules.


* Caching rules instruct BytePlus VOD how to cache files from the origin server at its edge nodes.

* When BytePlus VOD receives a user request, caching rules instruct it whether to search the cache for a matching file.


<span id="26c31acc"></span>
## How it works

<span id="83351b4f"></span>
### Upon receiving user requests

When the CDN receives a user request, it matches the user request to caching rules in descending order of priority, from highest to lowest. After matching one rule, the CDN stops matching the remaining rules. The matched rule can specify one of the following actions:


* Do not cache the file. In this case, the CDN directly requests the file from the origin server. Upon receiving the file, the CDN responds to the user request with the file and does not cache it.

* The file needs to be cached. In this case, the CDN checks whether the request hits the cache according to the [Cache key](https://docs.byteplus.com/docs/byteplus-vod/docs-cache-key) rules. The check results can be as follows:

   * The request hits the cache, and the cached file has not expired. In this case, the CDN serves the file from the cache.

   * The request hits the cache, but the cached file has expired. In this case, the CDN performs origin verification.

   * The request does not hit the cache. In this case, the CDN requests the file from the origin server. Upon receiving the file, the CDN serves it to the user and caches it according to the matched caching rule.


<span id="51c607c2"></span>
### When caching files

Upon receiving files from the origin server, the CDN processes them based on the instructions in the matched caching rule. You can configure the following caching behaviors in caching rules:


|**Caching policy** |**Caching behavior** |**Description** |**Cache TTL** |
|---|---|---|---|
|Use CDN Setting |Always Cache (On) |Ignore origin server response headers' no\-cache directive and always cache files. |Follow the configured **Cache TTL** in the rule. |
||Always Cache (Off) |Do not ignore the origin server's response header indicating not to cache. When caching behavior is not specified, do not cache the file. ||
|Use Origin Setting |Override Cache TTL (On) |Follow the instructions in the origin server's response header. When caching behavior is not specified, cache the file. |Follow the cache TTL indicated in the response header. When caching behavior is not specified, follow the configured **Cache TTL** in the rule. |
||Override Cache TTL (Off) |Follow the instructions in origin server's response header. When caching behavior is not specified, do not cache the file. |Follow the cache TTL indicated in the response header. |


<span id="e43257e0"></span>
### Default caching rule

When you add a domain name, CDN will automatically add a caching rule with the following configuration for you. You can modify its configuration.


* Caching Priority: Use CDN Setting

* Caching option: Always Cache (On)

* Cache TTL: 30 days

* Effective for all files.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cce0632b39c8451a83cd44861f1a0be5~tplv-goo7wpa0wc-image.image) </span>

After creating the domain, you will find an additional rule in the caching rule list. This rule always has the lowest priority and cannot be adjusted. Therefore, this rule applies to files that do not match any other rules. You cannot modify or delete this rule. This rule ensures that any file can match a rule.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67db020a429441a6b5086f9079bfb9b3~tplv-goo7wpa0wc-image.image) </span>

<span id="b06d3745"></span>
## Creating caching rule

If you have customized caching requirements for specific files on your site, you can create caching rules.


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Click the **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Caching configuration** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **Cache rule**, switch the **Status** toggle and click **Add rule**.

   
   |**Configuration** |**Description** |
   |---|---|
   |Priority |Indicates the priority of the rule. Rule with priority 1 has the highest priority. When a request is received, the CDN attempts to match rules in descending order of priority. If a rule is matched, the CDN stops matching other rules. You can adjust the rule's priority by dragging it. |
   |Rule type |Indicates the type of matching condition for the rule. The configuration has the following options:<br><br><br>* **File suffix**: The caching rule applies to all files with specified extensions.<br><br>* **File directory**: The caching rule applies to all files under specified paths.<br><br>* **File full path**: The caching rule applies to specific files. |
   |Rule |Specifies the value to match, such as a file extension or path. You need to enter one or more matching objects, separated by semicolons (;).<br><br><br>* If **Rule type** is **File suffix**, you need to enter one or more file extensions. For example: `xlsx` or `png;txt`.<br><br>* If **Rule type** is **File directory**, you need to enter one or more directory paths. Directory paths must start and end with a slash (/). For example: `/www/img/test/;/www/doc/`. If specifying all directories under the domain name, enter `/`.<br><br>* If **Rule type** is **File full path**, you need to enter one or more file paths. File paths must start with a slash (/) and support using asterisk (\*) in the path to represent one or more consecutive characters. For example: `/www/img/my*image.png`. |
   |Ignore case |Indicates whether the objects specified in **Rule** are case\-sensitive. The default setting is **Enabled**, which means case\-insensitive. For example: If you create a rule with matching objects `png;txt`, and **Ignore Case** is **Disabled**, the rule can match requests with URL `HTTPS://www.EXAMPLE.com/image.png` but not requests with URL `https://www.example.com/image.PNG`. |
   |Caching policy |Represents the caching policy. This configuration has the following options:<br><br><br>* **Use CDN Setting:**  Indicates that the CDN's caching behavior for specified files is based on the settings configured in this rule.<br><br>* **Use Origin Setting**: Indicates that the CDN's caching behavior for specified files is based on origin server response headers.<br><br><br>The actual caching behavior is specified in the **Caching behavior** configuration. |
   |Caching behavior |Indicates CDN's behavior when caching files. |
   

8. After configuration, click **Submit Changes** in the upper right corner.


<span id="18deb0f5"></span>
## Detailed description of caching behaviors


|**Caching policy** |**Caching behavior** |**Description** |**Cache TTL** |
|---|---|---|---|
|Use CDN Setting |Always Cache (On) |Indicates that the CDN always caches files. |Follows the Cache TTL configured in the rule. |
||Always Cache (Off) |* The CDN does not cache files under the following conditions:<br><br>   * The origin server response contains `Cache-Control: no-store` or `Cache-Control: private` headers.<br><br>   * The origin server response does not contain `Cache-Control` or `Expires` headers.<br><br>* In other cases, CDN will cache files. ||
|Use Origin Setting |Override Cache TTL (On) |The CDN caches files under the following conditions:<br><br><br>* The origin server response contains `Cache-Control: max-age` or `Expires` headers.<br><br>* The origin server response does not contain `Cache-Control` or `Expires` headers.<br><br>* In other cases, CDN will not cache files. |If `Cache-Control: max-age` or `Expires` headers are included, CDN follows the cache TTL indicated in the response headers.<br><br>If `Cache-Control` and `Expires` headers are not included, CDN follows the **Cache TTL** configured in the caching rules. |
||Override Cache TTL (Off) |* The CDN caches files under the following conditions:<br><br>   * The origin server response contains `Cache-Control: max-age` or `Expires` headers.<br><br>* In other cases, CDN will not cache files. |Follows the cache TTL indicated in the response headers. |


<span id="46117ced"></span>
## Additional information

<span id="f7fb5f07"></span>
### Cases where files are not cached

The CDN will not cache files from the origin server in the following cases, regardless of how caching rules are configured:


* The Content\-Length header in the origin server response has a value of 0.

* The HTTP method used for the user request is neither GET nor HEAD.

* The origin server response status code is not 2xx, and you haven't configured [Negative caching](https://docs.byteplus.com/docs/byteplus-vod/docs-configuring-negative-caching).

* For HEAD requests, the origin server response contains the `Transfer-Encoding: chunked` response header.


<span id="f8d3f8ef"></span>
### How to determine if cached files are expired

When a request is received, assuming the request matches a rule indicating that the requested file should be cached and the request hits the cache, the CDN follows these steps to determine if the cached file has expired:


1. Calculate the duration the file has been cached, in seconds, where the calculation is: Cached duration = Request timestamp \- Timestamp when the file was cached.

2. Obtain the cache TTL for the file based on the settings in the matched rule.


If Cached duration \> TTL, it means the cached file has expired. If Cached duration <= TTL, it means the cached file has not expired.

<span id="02f8f4bc"></span>
### Force cache updates

Assuming a file in the CDN cache has not expired, but the file on the origin server has been updated. You need users to get the latest version of that file.

In this case, you can perform a cache purge operation in CDN for that file. The cache purge operation forcefully marks that file as expired. Subsequently, if a user requests that file, CDN performs [Origin verification](https://docs.byteplus.com/docs/byteplus-vod/docs-setting-cache-time-to-live-ttl#aa303756). After obtaining the updated file, CDN responds to the user's request with the updated file and caches it.

<span id="7baa8cfd"></span>
### Origin verification

When a cached file expires, if a request is received for that file, the CDN will verify with the origin server whether the file has been updated. The origin verification process is as follows:


* If the origin server response for the file contains the Last\-Modified or ETag header, the CDN includes a special header in the origin verification request. ETag takes precedence over Last\-Modified.

   * If `ETag` exists, the origin verification request includes the `If-None-Match` header. The value of this header is the `ETag` value.

   * If `ETag` does not exist but `Last-Modified` does, the origin verification request includes the `If-Modified-Since` header. The value of this header is the `Last-Modified` value.

   * If neither `Last-Modified` nor `ETag` exist, CDN will directly request the file from the origin server. Upon receiving the file, CDN will respond to the user's request and caches the file.

* Regarding the origin server response status code:

   * If the status code is 304, it means the file is up\-to\-date. In this case, the CDN serves the cached file to the user. If the same file is requested again later, the CDN repeats the origin verification process.

   * If the status code is 200, it means the file has been updated on the origin server, and the response body contains the latest file. In this case, the CDN will serve the updated file to the user and replace the existing file in the cache.
