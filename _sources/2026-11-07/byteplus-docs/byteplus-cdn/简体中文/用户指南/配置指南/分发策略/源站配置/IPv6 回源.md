---
title: "IPv6 回源"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/origin_ip_preference_cn"
---

本文档介绍 BytePlus CDN 中的 "IPv6 回源" 特性。

<span id="概述"></span>
## 概述

IPv6 是网络层中 IP 协议的最新版本，具有比 IPv4 大得多的地址空间，以及一些其他优势。

对于域名类型的源站，当 CDN 向源站请求内容时，会首先通过 DNS 解析获取源站域名的 IP 地址。 默认情况下，CDN 会尝试获取与用户请求相同类型的 IP 地址。也就是说：


* 假设用户请求使用的是 IPv6 地址。在这个情况下，CDN 会尝试获取源站域名的 IPv6 地址。如果无法获取该 IP 地址，CDN 才尝试获取源站域名的 IPv4 地址。


如果您希望 CDN 在 DNS 解析时优先获取指定类型的 IP 地址，可以配置 “IPv6 回源” 功能。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">该功能不适用于 IP 地址类型的源站。</div>


* <div data-tips="true" data-tips-type="tip">要使用户请求访问 CDN 的 IPv6 地址，您需要先在域名的配置中 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-ipv6-cn">启用 IPv6</a>。</div>



<span id="操作步骤"></span>
## 操作步骤


1. 打开 **IPv6 回源** 配置页面。操作步骤参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 根据以下 **回源方式** 的配置描述，选择一个配置选项。

   * **协议跟随**：表示 CDN 尝试获取与用户请求相同类型的 IP 地址。这是默认设置。

   * **IPv6 优先**：表示 CDN 始终尝试获取源站域名的 IPv6 地址。如果无法获取该 IP 地址，CDN 才尝试获取源站域名的 IPv4 地址。

   * **IPv4 优先**：表示 CDN 始终尝试获取源站域名的 IPv4 地址。如果无法获取该 IP 地址，CDN 才尝试获取源站域名的 IPv6 地址。

3. 修改完成后，在页面右下方，点击 **保存**。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_271d5fc27ee7e53e19a3b63e93f36ab7.png) </span>
