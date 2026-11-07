---
title: "Smart compression"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-smart-compression"
---

To reduce file sizes for faster content delivery and lower bandwidth usage, you can configure the smart compression feature for your **custom\-origin domain name** in the BytePlus VOD console. This article describes how to configure the smart compression feature based on file types, directory, or other criteria.

<span id="1585373f"></span>
## Introduction

Smart compression means that the CDN intelligently determines whether a static file is suitable for compression and which algorithm should be used based on the requested information and the enabled compression algorithm. For files suitable for compression, the cache server compresses them before transferring.

After the smart compression feature is enabled, certain files that are already compressed, such as GIF, JPEG, and PNG images and MP4, AVI, and WMV files, will not be compressed, since compressing such files causes additional overhead without providing any compression benefit. The smart compression feature compresses files that are transmitted with the header `content_encoding`, which specifies the compression algorithm used. Before you enable the smart compression feature, read through the compression guidelines listed in the table.


|**Setting** |**Guideline** |
|---|---|
|Rules applied to |HTTP GET request only.<br><br>Note that the cache server will ignore the Range GET header in a request and return entire compressed files in the response. |
|Request headers |If you make a request containing the `Accept-Encoding: gzip, br` header, the CDN uses Brotli compression.<br><br>If the request does not contain this header, the CDN does not compress the content, as this indicates the client does not support it. |
|Compatible browsers |Gzip compression is compatible with all browsers, while Brotli compression is not compatible with some older versions of browsers. You can check browser compatibility [here](https://caniuse.com/?search=Brotli). |
|Content\-Type response header |The following values can be compressed:<br><br><br>* text/html<br><br>* text/xml<br><br>* text/plain<br><br>* text/css<br><br>* text/plain; charset=utf\-8<br><br>* text/javascript<br><br>* application/javascript<br><br>* application/x\-javascript<br><br>* application/rss+xml<br><br>* application/json<br><br>* application/xml<br><br>* image/tiff<br><br>* image/svg+xml |
|MD5 file validation |If your source files are not configured with MD5 file validation, do not enable smart compression. |
|The `Vary` header in a response |Ensure the `Vary` header in a response returned from the origin server complies with [RFC standards](https://datatracker.ietf.org/doc/html/rfc7231#section-7.1.4). Otherwise, smart compression may fail. |


<span id="eebcaae6"></span>
## Configuring smart compression rules


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Click the **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Advanced configuration** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **Smart compression**, switch the **Status** toggle and click **Add rule**.

   
   |**Configuration** |**Description** |
   |---|---|
   |Priority |Indicates the priority of the rule. The rule with priority 1 has the highest priority. When a request is received, the CDN tries to match the request with rules in descending order of priority. If a request matches a rule, the CDN stops matching other rules. You can adjust the priority of rules by dragging them. |
   |Rule type |The available options are:<br><br><br>* **File suffix**: The rule applies to all files with specific file suffixes.<br><br>* **File directory**: The rule applies to all files within specific directories.<br><br>* **File full path**: The rule applies to specific files.<br><br>* **Content\-Type**: The rule applies to files with specific Content\-Type. |
   |Rule |Specifies the items to match. You need to enter one or more values to match, and the total length cannot exceed 1,024 characters. Multiple values are separated by semicolons (;). The requirements for the values are as follows:<br><br><br>* If **Rule type** is **File suffix**, you need to enter one or more file extensions. For example, `xlsx` or `png;txt`.<br><br>* If **Rule type** is **File directory**, you need to enter one or more directory paths. The requirements for directory paths are as follows:<br><br>   * The directory path must start and end with a forward slash (/). For example, `/www/img/test/;/www/doc/`. To specify all directories under the domain, enter `/`.<br><br>   * The directory path can include printable ASCII characters, except for:<br><br>      * Consecutive slashes (//)<br><br>      * Percent signs (%)<br><br>      * Spaces<br><br>      * Dollar signs ($)<br><br>      * Question marks (?)<br><br>      * Delete (ASCII code 127)<br><br>* If **Rule type** is **File full path**, you need to enter one or more file paths. The requirements for file paths are as follows:<br><br>   * The file path must start with a forward slash (/). For example, `/www/img/image.png;/doc/study.docx`.<br><br>   * File paths can use a wildcard character (\*) to represent one or more consecutive characters.<br><br>   * File paths can include printable ASCII characters, except for:<br><br>      * Consecutive slashes (//)<br><br>      * Percent signs (%)<br><br>      * Spaces<br><br>      * Dollar signs ($)<br><br>      * Question marks (?)<br><br>      * Delete (ASCII code 127)<br><br>* If **Rule type** is **Content\-Type**, you need to enter one or more content types. The available options are:<br><br>   * **Default**: text/html<br><br>   * **Custom**: You can select one or more content types. |
   |Compression algorithm |The available options are:<br><br><br>* Gzip: A widely used data compression format which can compress plain text files to about 40% of their original size.<br><br>* Brotli: A compression algorithm introduced by Google which offers significant improvements in compression ratio and performance compared to Gzip. |
   

8. Click **Save**.
