---
title: "Cache key"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-cache-key"
---

To improve your CDN cache hit rate and reduce origin requests, you can customize how cache keys are generated.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Cache key configuration applies to <strong>Custom\-origin domain</strong> <strong>name</strong>.</div>


<span id="0dc99a11"></span>
## Introduction

<span id="547d43ac"></span>
### Cache key

A cache key is a unique identifier for each file in the cache. When a user request is received, the CDN generates a cache key for the request. Typically, the cache key includes the host, path, and query parameters. For example, `www.example.com/image.png?version=1`. Then, the CDN tries to match this cache key with the cache keys of cached files. The cache key is case\-sensitive when matching.


* If a match is found, it means a cache hit. In this case, the CDN sends the cached file to the user.

* If no match is found, it means a cache miss. In this case, the CDN requests the file from the origin server. After receiving the file, the CDN caches it using the cache key.


<span id="d2bc3ccf"></span>
## Cache key configuration

You can create cache key rules in the console. The purpose of this feature is to indicate which query parameters in the request URI should be included in the cache key when the CDN generates it. Since the generated cache key is used by the CDN to match cached files, cache key rules directly affect the cache hit rate.

<span id="35c6097d"></span>
### Usage scenario

If the query parameters in the file URI on your site are not used to differentiate files, you can create cache key rules to specify which query parameters need to be discarded in the generated cache key by the CDN. This can improve the cache hit rate and reduce origin requests. For example, if the URI contains an `auth` parameter, which is used to verify the user's identity rather than to differentiate files, this parameter does not need to be included in the generated cache key.

<span id="bdf8614d"></span>
### Default cache key rule

When you add a domain name, BytePlus VOD will automatically add a cache key rule for you. This rule applies to all file requests. You can modify the configuration of this rule, but you cannot delete it. When you add other cache key rules, this rule always has the lowest priority, ensuring that any request can match a rule.

<span id="afe624cc"></span>
## Adding cache key rules


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Click the **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Caching configuration** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **Cache key**, switch the **Status** toggle and click **Add rule**.

   
   |**Configuration** |**Description** |
   |---|---|
   |Priority |Indicates the priority of the rule. The rule with priority 1 has the highest priority. When a request is received, the CDN tries to match the request with rules in descending order of priority. If a request matches a rule, the CDN stops matching other rules. You can adjust the priority of rules by dragging them.<br><br>Note that you cannot adjust the priority of the default rule. |
   |Rule type |The available options are:<br><br><br>* **File suffix**: The rule applies to all files with specific file suffixes.<br><br>* **File directory**: The rule applies to all files within specific directories.<br><br>* **File full path**: The rule applies to specific files. |
   |Rule |Specifies the objects to match. You need to enter one or more matching objects, and the total length cannot exceed 1,024 characters. Multiple objects are separated by semicolons (;). The description of matching objects is as follows:<br><br><br>* If **Rule type** is **File suffix**, you need to enter one or more file extensions. For example, `xlsx` or `png;txt`.<br><br>* If **Rule type** is **File directory**, you need to enter one or more directory paths. The requirements for directory paths are as follows:<br><br>   * The directory path must start and end with a forward slash (/). For example, `/www/img/test/;/www/doc/`. To specify all directories under the domain, enter `/`.<br><br>   * The directory path can include printable ASCII characters, except for:<br><br>      * Consecutive slashes (//)<br><br>      * Percent signs (%)<br><br>      * Spaces<br><br>      * Dollar signs ($)<br><br>      * Question marks (?)<br><br>      * Delete (ASCII code 127)<br><br>* If **Rule type** is **File full path**, you need to enter one or more file paths. The requirements for file paths are as follows:<br><br>   * The file path must start with a forward slash (/). For example, `/www/img/image.png;/doc/study.docx`.<br><br>   * File paths support the use of wildcard (\*) to represent one or more consecutive characters.<br><br>   * File paths can include printable ASCII characters, except for:<br><br>      * Consecutive slashes (//)<br><br>      * Percent signs (%)<br><br>      * Spaces<br><br>      * Dollar signs ($)<br><br>      * Question marks (?)<br><br>      * Delete (ASCII code 127) |
   |Query parameters |Specifies how the CDN handles query parameters in the request URL when caching files and matching cached files. The available options are:<br><br><br>* **Include all**: Includes all query parameters in the request URI.<br><br>* **Include none**: Does not include any query parameters.<br><br>* **Include all except**: Include all query parameters except for the specified ones.<br><br>* **Include specified**: Include the specified query parameters. |
   |Specified parameters |Specifies the query parameters to keep or discard. Multiple query parameters are separated by semicolons (;). For example, `version;size`.<br><br><br>* If **Query parameters** is **Include all** or **Include none**, the value of this configuration must be `*`. `*` represents all query parameters.<br><br>* If **Query parameters** is **Include all except** or **Include specified**, you need to specify one or more query parameters, but you cannot specify `*`. Also, the query parameters you specify cannot include consecutive slashes (//), percent signs (%), or spaces.<br><br><br>The default value of this configuration is `*`. |
   |Ignore case |Indicates whether the specified parameter is case\-sensitive. This parameter is only effective when **Query parameters** is **Include all except** or **Include specified**.<br><br>For example, if you specify that the parameter to keep is `size` and **Ignore case** is **Enabled**. Then CDN receives a request with the parameter `SIZE` in the URI. In this case, the CDN will keep the `SIZE` parameter in the generated cache key.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the CDN tries to match the request with a cached file, the cache key used is case\-sensitive.</div><br> |
   

8. Click **Save**.


<span id="dca3a35e"></span>
## Configuration example

<span id="8eaa8488"></span>
### Scenario


* The URIs of files in the root directory of your site contain two query parameters, `version` and `token`.

* Among these two parameters, only `version` is used to differentiate files. For example, `/image.png?version=1` and `/image.png?version=2` are two different files. However, `/image.png?version=1&token=abc` and `/image.png?version=1&token=xyz` are the same file.

* The CDN receives two requests for this file. The URIs of the requests are `/image.png?version=1&token=12345` and `/image.png?version=1&token=abcde`.


<span id="8609a610"></span>
### Result without creating cache key rule

When the first request is received, the CDN caches the file. The cache key of the file in the cache is `/image.png?version=1&token=12345`. When the second request is received, the CDN tries to match the file in the cache using `/image.png?version=1&token=abcde`. Since there is no cache hit, the CDN requests the file from the origin.
