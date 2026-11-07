---
title: "Caching status code"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-caching-by-status-code"
---

To reduce the load on your origin servers from repeated error requests, you can configure status code caching. This guide provides step\-by\-step instructions on how to set up rules in the BytePlus VOD console to cache negative responses, such as 4xx and 5xx errors, for your custom\-origin domain names.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Cache key configuration applies to <strong>Custom\-origin domain</strong> <strong>name</strong>.</div>


<span id="8a706a6f"></span>
## Introduction

Normally, when a cache server successfully pulls requested content from the origin server, the origin server will return a 2XX status code. The cache server will process the content based on the configured cache validity. However, when negative responses are returned from the origin, like `404 Not Found` or `500 Internal Server Error`, and you do not want origin servers to receive the same requests to the object in a given period, you can use negative caching to reduce the load on your origin servers and decrease response latency.

Negative caching means caching negative responses for a very short period in order to prevent overwhelming your origin server. For example, if you configure to cache `404 Not Found` for a short period, this allows BytePlus VOD to shield origin servers from requests that generate errors like `404 Not Found`.

Currently, BytePlus VOD only supports negative caching of 4XX and 5XX status codes.

<span id="cdad3f4d"></span>
## Adding status code caching rules


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Click the **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Caching configuration** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **Status code caching**, switch the **Status** toggle and click **Add rule**.

   
   |**Configuration** |**Description** |
   |---|---|
   |Priority |Indicates the priority of the rule. The rule with priority 1 has the highest priority. When a request is received, CDN tries to match the request with rules in descending order of priority. If a request matches a rule, CDN stops matching other rules. You can adjust the priority of rules by dragging them.<br><br>Note that you cannot adjust the priority of the default rule. |
   |Rule type |The available options are:<br><br><br>* **File suffix**: The rule applies to all files with specific file suffixes.<br><br>* **File directory**: The rule applies to all files in specific directories.<br><br>* **File full path**: The rule applies to specific files. |
   |Rule |Represents the matching objects. You need to enter one or more matching objects, and the total length cannot exceed 1,024 characters. Multiple objects are separated by semicolons (;). The description of matching objects is as follows:<br><br><br>* If **Rule type** is **File suffix**, you need to enter one or more file extensions. For example, `xlsx` or `png;txt`.<br><br>* If **Rule type** is **File directory**, you need to enter one or more directory paths. The requirements for directory paths are as follows:<br><br>   * The directory path must start and end with a forward slash (/). For example, `/www/img/test/;/www/doc/`. To specify all directories under the domain, enter `/`.<br><br>   * The directory path can include printable ASCII characters, except for:<br><br>      * Consecutive slashes (//)<br><br>      * Percent signs (%)<br><br>      * Spaces<br><br>      * Dollar signs ($)<br><br>      * Question marks (?)<br><br>      * Delete (ASCII code 127)<br><br>* If **Rule type** is **File full path**, you need to enter one or more file paths. The requirements for file paths are as follows:<br><br>   * The file path must start with a forward slash (/). For example, `/www/img/image.png;/doc/study.docx`.<br><br>   * File paths support the use of wildcard (\*) to represent one or more consecutive characters.<br><br>   * File paths can include printable ASCII characters, except for:<br><br>      * Consecutive slashes (//)<br><br>      * Percent signs (%)<br><br>      * Spaces<br><br>      * Dollar signs ($)<br><br>      * Question marks (?)<br><br>      * Delete (ASCII code 127) |
   |Status code |Enter the status code. |
   |Ignore case |Indicates whether the specified parameter is case\-sensitive. This parameter is only effective when **Query parameters** is **Include all except** or **Include specified**.<br><br>For example, if you specify that the parameter to keep is `size` and **Ignore case** is **Enabled**. Then CDN receives a request with the parameter `SIZE` in the URI. In this case, the CDN will keep the `SIZE` parameter in the generated cache key.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the CDN tries to match the request with a cached file, the cache key used is case\-sensitive.</div><br> |
   

8. Click **Save**.
