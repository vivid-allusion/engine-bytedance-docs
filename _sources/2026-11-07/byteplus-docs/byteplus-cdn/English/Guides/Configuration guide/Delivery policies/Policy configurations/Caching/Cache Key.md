---
title: "Cache Key"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cache-keys"
---

To improve your CDN cache hit rate and reduce origin requests, you can customize how cache keys are generated. This guide explains how to create cache key rules in BytePlus CDN to control which URL query parameters are included or ignored during the caching process.

<span id="cache-key"></span>
## Cache Key

A cache key is a unique identifier for each file in the cache. By default, a cache key includes the hostname, path, and query parameters from the user's request URL. You can configure which query parameters are included in the cache key.

When the CDN receives a user request, it generates a cache key for the requested file and attempts to match this key against the cache keys of cached files. A successful match requires an exact match of the hostname, path, and query parameters in the request URL. Query parameter matching also considers the order in which parameters appear. If the CDN finds a match, the request is considered a cache hit. Note that the cache key matching process is case\-sensitive.

<span id="cache-key-configuration"></span>
## Cache Key Configuration

CDN provides cache key configuration. You can create cache key rules in the console. This feature lets you specify which query parameters from the request URL to include when CDN generates a cache key. Since the generated cache key will be used by CDN to match cached files, cache key rules directly affect the cache hit rate.

At the end of this document, we provide a [configuration example](https://docs.byteplus.com/en/docs/18/6578#configuration-example) to help you better understand the impact of cache key settings on cache hits.

<span id="usage-scenario"></span>
## Usage Scenario

If certain query parameters in your site's URLs do not distinguish between file versions, you can create cache key rules to discard those parameters. This improves the cache hit rate and reduces requests to the origin server. For example, the auth parameter in the URL verifies the user's identity, not to distinguish files. In this case, the parameter does not need to be included in the generated cache key.

<span id="steps"></span>
## Steps


1. Open the **Cache Key** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Click **Add Rule**.

   You can add up to 50 rules.

3. Refer to the following [Configuration Instructions](https://docs.byteplus.com/en/docs/18/6578#configuration-instructions).

4. After you finish configuring, click **Save**.


<span id="about-preset-cache-key-rules"></span>
### About Preset Cache Key Rules

When you add a domain, CDN automatically adds a cache key rule for you. This rule applies to requests for all files. You can modify the configuration of this rule, but you cannot delete it. When you add other cache key rules, the priority of this rule is always the lowest, ensuring that any request can match a rule.

<span id="configuration-instructions"></span>
### Configuration Instructions


|**Configuration** |**Description** |
|---|---|
|Priority |Indicates the priority of the rule. The rule with priority 1 has the highest priority. When a request is received, CDN tries to match the request with the rules in descending order of priority. If a request matches a rule, CDN stops matching the remaining rules. You can adjust the priority of the rules by dragging and dropping them. Note that you cannot adjust the priority of the preset rule. |
|Match Type |This configuration has the following options:<br><br><br>* **Path Extension**: Indicates that the rule is used to match requests for files ending with a specific suffix.<br><br>* **Path Directory**: Indicates that the rule is used to match requests for files under a specific directory path.<br><br>* **Full Path** : Indicates that the rule is used to match requests for specific files. |
|Match Value / Pattern |Specifies the pattern to match. The pattern must not exceed 1,024 characters and cannot include the following characters:<br><br><br>* Double slashes (//), spaces, dollar signs ($), and question marks (?).<br><br><br>Furthermore,<br><br><br>* If **Match Type** is **Path Extension**, the pattern must be one or more file extensions separated by semicolons (;). The file extensions should not start with a period (.). For example: `png;txt`.<br><br>* If **Match Type** is **Path Directory**, the pattern must be one or more directory paths separated by semicolons (;). Directory paths must start and end with a slash (/). For example: `/chs/foods/;/us/birds/`.<br><br>* If **Match Type** is **Full Path**, the pattern must be one or more file paths separated by semicolons (;). The file paths must start with a slash (/) and can include asterisks (\*) to represent one or more characters. For example: `/chs/foods/local*sets;/us/birds/chickadee`. |
|Parameter Handling |Specifies which query parameters from the request URL are included in the generated cache key. The configuration values are as follows:<br><br><br>* **Retain All**: The cache key includes all query parameters from the request URL. The order of query parameters in the cache key is the same as in the request URL.<br><br>* **Retain None**: The cache key does not include any query parameters from the request URL.<br><br>* **Retain Specified**: The cache key includes all query parameters from the request URL except those specified in **Parameter Name**. The CDN sorts the query parameters included in the cache key alphabetically before generating the cache key.<br><br>* **Retain All Except**: If the query parameters specified in **Parameter Name** exist in the user's request URL, the cache key includes these specified parameters. The CDN sorts the query parameters included in the cache key alphabetically before generating the cache key. |
|Parameter Name |Specifies the query parameters to retain or discard. Separate multiple query parameters with a semicolon (;). For example `version;size`.<br><br>&nbsp;<br><br>If **Parameter Handling** is **Retain Specified** or **Retain All Except**, you can specify one or more query parameters. Also, the specified query parameters should not include double slashes (//), percent signs (%), spaces. |
|Case\-Insensitive Parameter Matching |Indicates whether **Parameter Name** is case\-sensitive. This parameter is only valid when **Parameter Handling** is **Retain Specified** or **Retain All Except**.<br><br>&nbsp;<br><br>Example: If you specify to retain the parameter `size`, with **Case\-Insensitive Parameter Matching** enabled, then CDN will retain the `SIZE` parameter in the generated cache key when receiving a URL request that includes the `SIZE` parameter.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When CDN tries to match a request to a cached file, matching is always case\-sensitive.</div><br> |


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260916034300-211204487629.png) </span>

<span id="more-information"></span>
## More Information

<span id="configuration-example"></span>
### **Configuration Example**


* The file URLs in the root directory of your site contain the parameters `version` and `token`.

* Among these parameters, only `version` is used to distinguish files. For example, `/image.png?version=1` and `/image.png?version=2` are two different files. However, `/image.png?version=1&token=abc` and `/image.png?version=1&token=xyz` point to the same file.

* CDN receives two consecutive requests for the file. The URLs of the requests are `https://<domain>/image.png?version=1&token=12345` and `https://<domain>/image.png?version=1&token=abcde`.


<span id="result-without-creating-a-cache-key-rule"></span>
#### Result Without Creating a Cache Key Rule

Upon receiving the first request, CDN caches the file. The cache key for the file in the cache is `/image.png?version=1&token=12345`. Upon receiving the second request, CDN uses `/image.png?version=1&token=abcde` to match the file in the cache. Since this results in a cache miss, CDN requests the file from the origin server.
