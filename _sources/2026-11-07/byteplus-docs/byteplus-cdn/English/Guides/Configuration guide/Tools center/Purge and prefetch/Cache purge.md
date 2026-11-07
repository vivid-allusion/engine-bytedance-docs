---
title: "Cache purge"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-purge"
---

<span id="cache-purge-overview"></span>
## Cache Purge Overview

Cache Purge is a feature that allows you to manually remove specified files or directories from BytePlus CDN edge nodes before their set expiration time. This guide explains how to use this feature to ensure that your users can immediately access the latest content after you have updated it on your origin server.

<span id="how-it-works"></span>
## How It Works

You use "Cache Purge" to submit purge tasks for specific files or directories.


* For a file purge, CDN will remove the specified files from the cache. Afterward, when requests for these files are received, the CDN fetches them from the origin server.

* For a directory purge, CDN marks the files under the specified directory as expired. When these files are requested, the CDN will send a file validation request to the origin server. See [origin validation](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-caching-rules#origin-validation) for a description of the file validation process.


<span id="usage-scenarios"></span>
## Usage Scenarios

"Cache Purge" is suitable for the following scenarios:


* Key files have been updated on your site, and you need users to access the latest files.

* Specific files on the origin server need to be deleted for certain reasons. However, these files may already be cached by the CDN. You want to prevent users from accessing these files.


<span id="precautions"></span>
## Precautions


* "Cache Purge" ensures that users get the latest version of a file. However, after a file is purged, the first access to that file will not be accelerated. If you need the first access to the file to be accelerated, after the purge task is successfully executed, you can use the [Origin prefetch](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-prefetch) feature.

* After you submit a purge task, it takes about 5 minutes to take effect.

* Submitting purge tasks for many files at once triggers a large number of requests to your origin server. As a result, your origin server may face a surge in traffic, especially with larger files.

* You cannot directly purge files and directories under a wildcard domain. Instead, you need to perform these operations for each subdomain.


<span id="purge-quota"></span>
## Purge Quota

Your primary account has the following daily limits for purging files and directories:


* If you are purging files, you can purge up to 10,000 files per day. Each purge task can include up to 100 URLs.

* If you are purging directories, you can purge up to 50 directories per day.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The purge quota is shared between the primary account and IAM accounts.</div>


<span id="steps"></span>
## Steps


1. Log in to the [BytePlus CDN Management Console](https://console.byteplus.com/cdn).

2. In the left sidebar, click **Tools Center** \> **Purge and Prefetch**.

3. On the **Purge and Prefetch** page, click the **Cache Purge** tab.

4. Follow the configuration instructions below.

5. After completing configuration, click **Submit**.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260410072736-109724106610.png) </span>

<span id="configuration-instructions"></span>
## Configuration Instructions


|**Configuration** |**Description** |
|---|---|
|Task Type |Indicates the type of task. This configuration has the following values:<br><br><br>* **URL Purge**: Indicates that the purge target is one or more files.<br><br>* **Directory Purge**: Indicates that the purge target is one or more directories.<br><br><br>Your account has a limited number of files and directories that can be purged daily. See [Purge Quota](https://docs.byteplus.com/en/docs/18/6625#purge-quota) for details. |
|Purge by Prefix |Indicates whether to enable "Purge by Prefix". This configuration only appears when **Task Type** is **Directory Purge**, and it is disabled by default. |
|URLs |Indicates the URLs that need to be purged. This configuration has the following values:<br><br><br>* **Enter URLs**: Indicates manually entering the URLs that need to be purged.<br><br>* **Import from File**: Indicates that you can upload a .txt file containing the URLs to be purged.<br><br><br>The URLs must meet the following conditions:<br><br><br>* If **Task Type** is **URL Purge**, you can specify up to 100 file URLs. File URLs must meet the following conditions:<br><br>   * File URLs must start with `https://` or `http://`.<br><br>   * Multiple file URLs must be separated by new lines.<br><br>* If **Task Type** is **Directory Purge**, the following conditions apply:<br><br>   * If **Purge by Prefix** is not enabled, you can specify up to 100 directory URLs. The directory URLs must meet the following conditions:<br><br>      * The directory URLs must start with `https://` or `http://` and end with `/`.<br><br>      * Multiple directory URLs must be separated by new lines.<br><br>   * If **Purge by Prefix** is enabled, you can specify up to 100 prefixes to match directory URLs. For example, the prefix `http://example.com/images/` matches all paths that start with it, such as `http://example.com/images/pic1.jpg` and `http://example.com/images/2024/`. |
|Purge by Request Header |Specifies the request headers that must be included in the cache key of the files to be purged. The file will only be matched and purged if its cache key contains all the headers specified here.<br><br>&nbsp;<br><br>The request headers must meet the following requirements:<br><br><br>* You can specify up to 10 request headers.<br><br>* The header name cannot be `User-Agent`, nor can it start with `x-bdcdn-` or `Volc-Cdn`.<br><br>* Both the header name and value cannot exceed 1,024 characters.<br><br><br>A common use case for this configuration is as follows:<br><br><br>* You have configured a list of request headers to be included in the cache key using the Rules Engine. When performing a purge, you only want to precisely purge files whose cache keys contain the specified request headers. |


<span id="additional-features"></span>
## Additional Features

You need to [submit a ticket](https://console.byteplus.com/workorder/create) to enable the following features:


* Force Delete

* RegEx Purge


<span id="force-delete"></span>
### Force Delete

When **Task Type** is **Directory Purge**, this configuration appears to specify whether to delete cached files.


* By default, when you submit a cache purge task, CDN marks the corresponding files in the cache as expired instead of deleting them. When receiving requests for these files, CDN sends file validation requests to the origin server instead of directly requesting files. See [Origin Validation](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-caching-rules#origin-validation).

* When **Force Delete** is enabled, the purge task deletes the corresponding files in the cache. When receiving requests for these files, CDN directly requests files from the origin server.


<span id="regex-purge"></span>
### RegEx Purge

When specifying file URLs, you can use regular expressions in the URLs to match files that need to be purged. You can enter one or multiple URLs, with multiple URLs separated by line breaks. Each URL cannot exceed 256 characters. Regular expression matching is case\-sensitive.

Your account can purge 20 URLs containing regular expressions per day. You can submit up to 10 URLs at a time.

In URLs, the regular expressions you can specify have the following restrictions:


* Regular expressions match file paths and query strings but do not include the leading `/` in the path. This means the URL format can only be `http://host/regex` or `https://host/regex`. `host` represents the domain, and `regex` represents the regular expression.

* Regular expressions can only contain the following metacharacters:

   * [0\-9]

   * [a\-z]

   * [A\-Z]

   * [a\-zA\-Z]

   * [^/]\*

   * .\*

   * +

   * [,?]

   * ?


<span id="notes"></span>
#### Notes

In file URLs containing regular expressions that you construct, except for the leading `/` in the path, the entire path is considered a regular expression. Therefore, as long as the regular expression matches part of the path in an actual file's URL, that file will be considered a match and will be purged by CDN.

For example, `https://www.example.com/dir2/.*\.js` can match the following file URLs:


* http://www.example.com/dir2/img1.js

* http://www.example.com/dir2/img1.js?size=small

* http://www.example.com/dir1/dir2/img1.js

* http://www.example.com/dir1/dir2/img1.jsp


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_63d4586b2c1e80245fcb35b10aea9fe2.png) </span>
