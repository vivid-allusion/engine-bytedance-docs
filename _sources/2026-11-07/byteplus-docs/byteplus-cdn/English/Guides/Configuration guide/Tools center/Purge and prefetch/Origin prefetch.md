---
title: "Origin prefetch"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-prefetch"
---

<span id="prefetch-overview"></span>
## Prefetch Overview

Prefetch is a BytePlus CDN feature that allows you to proactively cache files from your origin server to CDN edge nodes. This ensures that even the first user request for a file results in a cache hit, significantly improving access speed for content like new software packages or promotional event pages.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">There is no charge for prefetch.</div>


<span id="usage-scenarios"></span>
## Usage Scenarios

"Prefetch" is suitable for the following scenarios:


* Files expected to receive high traffic, such as installation packages for software. After you publish the installation package on your site, you can submit a prefetch task for it. This way, the download of the package can be accelerated immediately.

* Promotional pages for large events. Before the event starts, you can submit a prefetch task for those promotional pages. When the event begins, users will be able to quickly open these pages.


<span id="precautions"></span>
## Precautions


* After you submit a prefetch task, the origin node will request the file specified in the prefetch task from your origin server. If the prefetch task includes many files, your site may experience increased load in the short term, especially when some files are large. For this reason, CDN provides a "concurrency limit" configuration. This configuration specifies the maximum number of files that the origin node can request from the origin server at a time when processing a prefetch task. See [Configuration Instructions](https://docs.byteplus.com/en/docs/18/6626#configuration-instructions).

* The completion time of a prefetch task will vary depending on the actual size of the files being prefetched.

* When submitting a prefetch task for a file, if the file has already been cached by the CDN and the cache is not expired, the CDN will not prefetch that file. We recommend one of the following approaches:

   * Regardless of whether the file is cached, submit a [Cache purge](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-purge) task for the file before submitting the prefetch task. Note that with this approach, if the file is not cached, the purge operation will still consume one purge quota.

   * [Determine if the file is cached](https://docs.byteplus.com/en/docs/18/6626#how-to-determine-if-a-request-hits-the-cdn-cache). If the file is already cached, then submit a [Cache purge](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-purge) task.


<span id="prefetch-quota"></span>
## Prefetch Quota

Your account can prefetch up to 1,000 files per day.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The prefetch quota is shared between the primary account and IAM users.</div>


<span id="operational-steps"></span>
## Operational Steps


1. Log in to the [BytePlus CDN Management Console](https://console.byteplus.com/cdn).

2. In the left sidebar, click **Tools Center** \> **Purge and Prefetch**.

3. On the **Purge and Prefetch** page, click the **Origin Prefetch** tab.

4. Follow the configuration instructions below.

5. After configuring the settings, click **Submit**.


<span id="configuration-instructions"></span>
### Configuration Instructions


|**Configuration** |**Description** |
|---|---|
|URLs |The URLs of the files to prefetch. This configuration has the following options:<br><br><br>* **Enter URLs**: Manually enter the URLs of the files to prefetch. You can submit up to 100 URLs at a time.<br><br>* **Import from File**: Upload a .txt text file. The URLs of the files to prefetch are contained in this text file.<br><br><br>The file URLs must meet the following conditions:<br><br><br>* The file URL must start with `https://` or `http://`.<br><br>* Multiple file URLs should be separated by a newline.<br><br><br>The number of URLs you can prefetch per day under your account is limited. See [Prefetch Quota](https://docs.byteplus.com/en/docs/18/6626#prefetch-quota). |
|Concurrency |Represents the maximum number of simultaneous requests that CDN sends to the origin server for a file prefetch task. The default value for this configuration is 10. You can set the range from 1 to 1,000.<br><br>&nbsp;<br><br>You can set a reasonable number of concurrent requests based on the request handling capacity of the origin server. |


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_8fc4008ca3e8c0834386db73dba4e1f0.png) </span>

<span id="how-to-determine-if-a-request-hits-the-cdn-cache"></span>
## How to determine if a request hits the CDN cache

In the CDN's response to user requests, the `X-Response-Cache` header indicates whether the request hit the cache.


* `edge_hit`: Indicates a cache hit.

* `miss`: Indicates a cache miss.


You can also obtain the value of the `cdn_cache_status` variable by configuring [CDN response headers](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cdn-response-headers). This variable indicates whether the request hit the cache.
