---
title: "【通告】Let's Encrypt 证书链变更"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/lets_encrypt_cert_chain_update_cn"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在 BytePlus CDN 中，如果您为域名部署了 Let's Encrypt 证书来启用域名的 HTTPS 访问，请关注本通告。</div>


尊敬的 BytePlus 用户，您好：

在 Let's Encrypt 的证书链中，对中间证书进行交叉签名的 IdenTrust 根证书将于 **2024年9月30日** 到期。同时，自 **2024年6月6日** 起，Let's Encrypt 签发的证书仅以自签根证书 ISRG Root X1 作为唯一授信根证书。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Let's Encrypt 证书的有效期是 90 天。</div>


如果您的域名部署了 Let's Encrypt 证书，只有客户端信任 ISRG Root X1，也就是客户端的信任库包含 ISRG Root X1，客户端才能正常使用 HTTPS 协议访问您的域名。自 9月开始，建议您监控用户反馈渠道，关注与证书相关的 CDN 访问问题反馈。

以下常见系统只有在特定版本才信任 ISRG Root X1：


* Android：Android 7.1.1 及以上版本。

* Windows：Windows XP SP3 及以上版本，Windows Server 2008 及以上版本（关闭了自动根证书更新的系统除外）。

* Java：Java SE 7u151, Java SE 8u141, Java SE 9 及以上版本。

* macOS：macOS 10.12.1 Sierra 及以上版本。

* iOS：iOS 10.0 及以上版本。


关于更多信任 ISRG Root X1 的系统，参见 [Let's Encrypt 文档 - 信任 ISRG Root X1 的平台](https://letsencrypt.org/zh-cn/docs/certificate-compatibility/)。

针对证书相关的 CDN 访问问题，您可以采取以下措施：


*  **（推荐）为域名部署付费证书**：付费证书具有更广泛的兼容性，且效期均为一年，相比于只有 90 天有效期的 Let's Encrypt 证书，大大节省了证书维护成本。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">BytePlus 证书中心提供多种规格的付费证书供您选择，并提供多种采购优惠。<a href="https://www.byteplus.com/zh-CN/product/certificate-center">前往了解</a>。   </div>
   

* 升级客户端信任库：如果客户端的系统版本较老，可能会不信任 ISRG Root X1。要使客户端能正常使用 HTTPS 协议访问您的加速域名，请升级客户端信任库，以包含 ISRG Root X1 证书。


感谢您对 BytePlus 的支持与关注。如果您有任何疑问，欢迎随时与我们沟通。
