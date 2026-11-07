---
title: "Range 回源设置"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-range-get-cn"
---

本文档介绍 CDN 中的 Range 回源特性。在大文件下载、流媒体播放等场景中，启用该特性能有效提升文件的分发效率，降低 CDN 的回源流量、减轻源站的压力。

<span id="656448bc"></span>
## 关于 Range 请求

Range 请求指的是那些包含了 Range 请求头的 HTTP 请求。该请求头指定了请求的文件范围，表示请求的是文件的一个分片，而非整个文件。例如，`Range:bytes=0-149` 表示请求的是文件前 150 字节。如果 Range 请求成功，服务器的响应状态码是 206。

<span id="1c7040cd"></span>
## 注意事项


* 如果请求文件不可缓存，无论 Range 回源是否启用，CDN 都会向源站透传用户 Range 请求。

* 如果源站不支持 Range 请求，启用 Range 回源后，回源请求可能会失败。

* 启用 Range 回源后，针对同一个文件，其所有分片的缓存过期时间均以该文件第一个被缓存的分片为准。


<span id="7fcd1280"></span>
## 未启用 Range 回源时 CDN 的行为

未启用 Range 回源时，无论用户请求是否为 Range 请求，只要 CDN 没有缓存过完整文件，CDN 就会向源站请求完整文件。

<span id="ff4d7338"></span>
## 启用 Range 回源后的 CDN 行为

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">对于 2025\-09\-10 后添加的域名，如果您对这些域名启用了 Range 回源，CDN 在回源时会增加探测机制。该机制可避免当文件不可缓存或者源站文件有更新时源站下行流量增大的问题。</div>


<span id="a183c3b9"></span>
### 2025\-09\-10 起 CDN 对新增域名的 Range 回源机制

对于客户端 Range 请求，在回源时，CDN 会先发送一个探测 Range 请求（Range: 0\-0）。基于源站响应，CDN 判断请求文件是否可缓存。


* 如果文件不可缓存，CDN 向源站透传用户 Range 请求。

* 如果文件可缓存，CDN 基于已缓存分片检查文件在源站上是否有更新。

   * 如果文件无更新，CDN 按照您指定的分片大小（默认 1 MB）依次发送回源请求。在获得相应数量的分片后，CDN 返回客户端所请求的分片。

   * 如果文件有更新，CDN 按照用户 Range 请求中指定的分片大小回源。


<span id="750b9b8c"></span>
### CDN 对 2025\-09\-10 前创建域名的 Range 回源机制

回源时，CDN 将用户 Range 请求的分片起始位置按照您指定的分片大小（默认 1 MB）向下取整，作为**第一个**回源 Range 请求的分片起始位置。收到源站响应时，


* 如果响应状态码是 200，CDN 响应完整文件。

* 如果状态码是 206，CDN 判断请求文件是否可缓存。

   * 如果文件不可缓存，CDN 向源站透传用户 Range 请求。

   * 如果文件可缓存，CDN 基于已缓存分片检查文件在源站上是否有更新。

      * 如果文件无更新，CDN 依次发送**后续**回源 Range 请求。

      * 如果文件有更新，CDN 先清理分片缓存，再依次发送**后续**回源 Range 请求。

         在获得相应数量的分片后，CDN 返回客户端所请求的分片。

* 如果响应状态码是 416，则 CDN 判断请求文件是否可缓存。

   * 如果文件不可缓存，CDN 向源站透传用户 Range 请求。

   * 如果文件可缓存，CDN 响应 416 状态码。

* 如果是其他状态码，CDN 向源站透传用户 Range 请求。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">回源 Range 请求可能会发生分片越界行为。可能发生分片越界行为。例如：完整文件的大小是 1.5 MB，用户请求的文件范围是 14,000,000\-15,000,000。在这个情况下，对于 CDN 发送的第一个回源 Range 请求，文件范围是 14,000,000\-15,048,576，超出了文件的大小。</div>


<div data-tips="true" data-tips-type="tip">如果源站是阿里云对象存储（OSS），越界发生时 OSS 可能会有非预期响应。参见下方 OSS 兼容配置中描述的解决方法。</div>


<span id="9d2e5f24"></span>
### AlibabaCloud OSS 兼容配置

假设以下场景：


* 您的源站是 OSS 存储桶。

* 回源 Range 请求的文件范围超过了完整文件的大小。


在这个场景中，OSS 会响应 200 状态码并返回完整文件。这会导致 OSS 的下行流量增大，可能会触发 OSS 限流，影响回源请求的数据传输速度。

因此，如果您的源站是 OSS 中的存储桶，推荐您为您的域名设置 [回源 HTTP 请求头](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-origin-request-headers-cn)：`x-oss-range-behavior:standard`。参见 [该头部对于 OSS 行为的影响](https://www.alibabacloud.com/help/zh/oss/how-to-obtain-oss-resources-by-segmenting-http-range-requests)。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a86aef98bffa4d69a2ab728aea02da53~tplv-goo7wpa0wc-image.image) </span>

<span id="926a384d"></span>
## 操作步骤


1. 打开 **Range 回源设置** 配置页面。操作步骤参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 设置 **状态** 为 **开启**。

3. 设置分片大小，默认是 1 MB。较大的分片可以减少回源请求次数，但可能在网络不稳定时增加失败重传的成本；较小的分片则相反。

   * 如果单位是 MB，您可以指定的范围是 1~40 MB，且必须是整数。

   * 如果单位是 KB，您只能指定 512 KB。

4. 点击 **提交编辑**。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f8f31b2ccb8404e940dae4a84dac867~tplv-goo7wpa0wc-topic.webp) </span>
