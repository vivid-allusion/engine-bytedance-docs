---
title: "Cache Sharing"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cache-sharing_en-us"
---

Cache Sharing is a BytePlus CDN feature that allows multiple domains to share the same CDN cache. This is ideal for scenarios where you have identical files across different domains, as it reduces requests to your origin server and improves cache efficiency. This document introduces the feature's benefits, limitations, and provides step\-by\-step instructions for configuration.

To use this feature, please [submit a ticket](https://console.byteplus.com/workorder/create).

<span id="what-is-cache-sharing"></span>
## What is Cache Sharing

Cache Sharing allows multiple domains to share the same CDN cache. In CDN, you can create one or more Cache Sharing configurations. In a Cache Sharing configuration, you specify one caching domain and one or more sharing domains. The sharing domains will share the CDN cache of the caching domain.

<span id="usage-scenarios"></span>
## Usage Scenarios

Cache Sharing is suitable for the following scenarios:


* You have multiple domains with identical files. To reduce the number of requests from CDN to the origin server, you can configure Cache Sharing for these domains.

* Your site has multiple domains for different distribution channels targeting different users. These domains distribute the same content.


After you add, modify, or delete a Cache Sharing configuration, the hit ratio of requests to the sharing domains may decrease. For specific reasons, see [How Cache Sharing Works](https://docs.byteplus.com/en/docs/18/47603#how-cache-sharing-works). Please proceed with caution.

<span id="how-cache-sharing-works"></span>
## How Cache Sharing Works

After you create a Cache Sharing configuration, when CDN receives a request for a sharing domain, it processes the request as follows:


1. Based on the caching behavior of the sharing domain, CDN determines whether the requested file needs to be cached and the cache TTL. If the file does not need to be cached, CDN requests the file from the origin server of the sharing domain, and then responds to the request with this file. The process ends.

2. If the file needs to be cached, CDN replaces the domain in the requested file URL with the caching domain, and then searches for the requested file in the cache. If the file is not found in the cache, proceed to step 4.

3. If the file is found in the cache, CDN uses the cache TTL obtained in step 1 to determine whether the cached file has expired. If the file has not expired, CDN responds to the request with this file. The process ends.

4. If the file has expired or CDN cannot find the file in the cache, CDN requests the file from the origin server of the sharing domain.

5. After retrieving the file from the origin server, CDN caches it under the caching domain. The process ends.


Cache sharing configuration affects the cache of edge nodes. Please be cautious when creating, deleting, and modifying operations. Before operating, make sure to read the [Notes](https://docs.byteplus.com/en/docs/18/47603#notes).

<span id="limitations"></span>
## Limitations


* If a domain has been set as the caching domain for other domains, you cannot set this domain as a sharing domain in any Cache Sharing configuration.

* The sharing domains and caching domain must be under the same primary account.

* The caching domain cannot be a wildcard domain.


<span id="operation-steps"></span>
## Operation Steps


1. Log in to the [BytePlus CDN Console](https://console.byteplus.com/cdn).

2. In the left navigation bar, click **Pro Settings** \> **Cache Sharing**.

3. On the **Cache Sharing** page, click **Create Configuration**.

4. On the **Create Configuration** page, specify a caching domain, specify one or more sharing domains, and then click **Submit**.


The specified sharing domains will share the CDN cache of the caching domain. After you click **Submit**, the Cache Sharing configuration you created appears in the list.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_51d3fa0cbfbb9dbfd9241d46a72825e8.png) </span>

<span id="notes"></span>
## Notes


* Before you create or modify a Cache Sharing configuration, it is recommended to set the sharing domains and caching domain to use the same origin server configuration and cache key configuration. After the Cache Sharing configuration takes effect, the hit ratio can be improved, and incorrect cached files can be avoided.

   * For requests to the sharing domains, CDN searches for files in the cache under the caching domain, not under the sharing domains. In the short term, the hit ratio for requests to the sharing domains may decrease.

   * After you create a Cache Sharing configuration, the sharing domains no longer use their own caches, but instead use the cache of the caching domain. After you delete a Cache Sharing configuration, the sharing domains will continue to use their own cache.

   * It is recommended that domains in the Cache Sharing configuration use the same origin server configuration. If they are not the same, the following situations may occur:

      * There are files with the same path and filename but different update times or content under different origin servers. Based on [How Cache Sharing Works](https://docs.byteplus.com/en/docs/18/47603#how-cache-sharing-works), the actually cached file may come from any origin server, resulting in users getting incorrect files.

      * It is recommended that the cache key configurations of the sharing domains are the same as those of the caching domain to improve the hit ratio.
