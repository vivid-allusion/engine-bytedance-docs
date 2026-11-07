---
title: "Range Origin Fetch"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-range-get"
---

Range Origin Fetch is a CDN feature that allows the CDN to fetch content from the origin server in fragments (ranges) instead of as a whole file. For large file downloads and media streaming, this improves distribution efficiency, reduces origin\-fetch traffic, and alleviates pressure on the origin. This document explains its mechanism, notes, and configuration steps.

<span id="656448bc"></span>
## About Range Requests

A Range request is an HTTP request that includes the Range request header. This header specifies the requested file range, indicating a request for a file fragment instead of the complete file. For example, `Range:bytes=0-149` indicates a request for the first 150 bytes of the file. If a Range request is successful, the server's response status code is 206.

<span id="1c7040cd"></span>
## Notes


* If the requested file cannot be cached, the CDN passes the user's Range request to the origin, regardless of whether Range Origin Fetch is enabled.

* If the origin does not support Range requests, origin requests may fail after Range Origin Fetch is enabled.

* After enabling Range Origin Fetch, the cache expiration time for all fragments of a file is determined by its first cached fragment.


<span id="7fcd1280"></span>
## CDN behavior when Range Origin Fetch is disabled

When Range Origin Fetch is disabled, the CDN requests the complete file from the origin if the file is not fully cached, regardless of whether the user sends a Range request.

<span id="ff4d7338"></span>
## CDN behavior after Range Origin Fetch is enabled

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When Range Origin Fetch is enabled for domain names added after September 10, 2025, the CDN uses a detection mechanism during origin fetch. This mechanism prevents an increase in origin server egress traffic when a file is not cacheable or has been updated.</div>


<span id="a183c3b9"></span>
### Range Origin Fetch mechanism for new domain names starting September 10, 2025

For client Range requests, the CDN first sends a probing Range request (Range: 0\-0) to the origin. Based on the origin's response, the CDN determines whether the requested file can be cached.


* If the file is not cacheable, the CDN forwards the user's Range request to the origin.

* If the file is cacheable, the CDN checks for updates on the origin based on the cached fragments.

   * If the file has not been updated, the CDN sends origin requests sequentially based on the fragment size you specify (default is 1 MB). After receiving the required number of fragments, the CDN returns the requested fragments to the client.

   * If the file has been updated, the CDN fetches the range specified in the user's request from the origin.


<span id="750b9b8c"></span>
### CDN Range Origin Fetch mechanism for domain names created before 2025\-09\-10

When fetching from the origin, the CDN determines the start position for the first Range Origin Fetch request by rounding down the start position of the user's Range request to the nearest multiple of your specified fragment size (default is 1 MB). When a response is received from the origin,


* If the response status code is 200, the CDN serves the complete file.

* If the status code is 206, the CDN determines if the requested file is cacheable.

   * If the file is not cacheable, the CDN forwards the user's Range request to the origin.

   * If the file is cacheable, the CDN checks for updates on the origin based on the cached fragments.

      * If there are no updates, the CDN sends the **subsequent** Range Origin Fetch requests in sequence.

      * If there is an update, the CDN first clears the fragment cache and then sends the **subsequent** Range Origin Fetch requests in sequence.

         After receiving the corresponding number of fragments, the CDN returns the requested fragments to the client.

* If the response status code is 416, the CDN checks if the requested file is cacheable.

   * If the file is not cacheable, the CDN forwards the user's Range request to the origin.

   * If the file is cacheable, the CDN responds with a 416 status code.

* For other status codes, the CDN forwards the user's Range request to the origin.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Range Origin Fetch can result in requests for out\-of\-bounds fragments. For example, the size of the complete file is 1.5 MB, and the user requests the file range 14,000,000\-15,000,000. In this case, the first Range Origin Fetch request sent by the CDN is for the file range 14,000,000\-15,048,576, which exceeds the file size.</div>


<div data-tips="true" data-tips-type="tip">If the origin is Alibaba Cloud Object Storage (OSS), OSS may return an unexpected response when the requested range is out of bounds. See the solution in the OSS compatibility configuration below.</div>


<span id="9d2e5f24"></span>
### Alibaba Cloud OSS compatibility configuration

Consider the following scenario:


* Your origin is an OSS bucket.

* The range of an Range Origin Fetch request exceeds the complete file size.


In this scenario, OSS responds with a 200 status code and returns the complete file. This increases OSS egress traffic, which may trigger OSS throttling and affect the data transfer rate of origin requests.

Therefore, if your origin is an OSS bucket, we recommend setting the [Origin Request Headers](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-request-headers) for your domain name to `x-oss-range-behavior:standard`. For details, see the documentation on [how this header affects OSS behavior](https://www.alibabacloud.com/help/zh/oss/how-to-obtain-oss-resources-by-segmenting-http-range-requests).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63c37f21d7f4415ca888910d38ef1601~tplv-goo7wpa0wc-image.image) </span>

<span id="926a384d"></span>
## Steps


1. Open the **Range Origin Fetch** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to **Enabled**.

3. Set the fragment size, with a default of 1 MB. Larger fragments reduce the number of origin requests but may increase retransmission costs on unstable networks. The opposite is true for smaller fragments.

   * If the unit is MB, the valid range is 1–40 MB, and the value must be an integer.

   * If the unit is KB, you can only specify 512 KB.

4. Click **Submit Changes**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/655e81d391384ef6a11563d135939274~tplv-goo7wpa0wc-image.image) </span>
