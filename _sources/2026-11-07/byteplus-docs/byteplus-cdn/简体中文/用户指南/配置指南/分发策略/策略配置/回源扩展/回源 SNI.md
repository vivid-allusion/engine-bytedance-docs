---
title: "回源 SNI"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-origin-sni_1-cn"
---

<span id="什么是-sni"></span>
## 什么是 SNI

SNI 的英文全称是 Server Name Indication。SNI 是 TLS 协议的扩展。在同一台服务器上部署了多个站点的场景下，SNI 解决了以下问题：


* 在客户端使用 HTTPS 协议与服务器建立连接时，服务端无法知道该发送给客户端哪个站点的证书。


如果客户端使用不安全的 HTTP 协议与服务端通信，在数据传输时，服务端通过客户端请求中的 Host 头部判断客户端需要访问的站点。但是如果客户端使用 HTTPS 协议连接服务器，在数据传输开始前有一个 TLS 握手的过程。在该过程中，客户端还未传递 Host 头部给服务器。因此服务器无法获得 Host 字段信息来判断需要发送给客户端的站点证书。此时，客户端可以使用 SNI 头部告知服务端需要的目标站点。这样服务端就能在 TLS 握手阶段发送相应的证书给客户端了。

<span id="回源-sni"></span>
## 回源 SNI

本文讨论的 SNI 是 BytePlus CDN 的 "回源 SNI" 配置。 "回源 SNI" 指定了 CDN 在使用 HTTPS 协议向源站请求内容时需要访问的源站域名。如果您的域名启用了 HTTPS，系统有默认的 "回源 SNI" 设置。默认的 "回源 SNI" 设置如下：


* 如果您没有指定 "回源 Host"，"回源 SNI" 与域名相同。

* 如果您指定了 ”回源 Host“，"回源 SNI" 与 "回源 Host" 相同。


但是在某些场景下，"回源 SNI" 与 "回源 Host" 不相同。如果您有这样的场景，可以在 CDN 控制台配置 "回源 SNI"。

<span id="操作步骤"></span>
## 操作步骤


1. 打开 **回源 SNI** 配置页面。操作步骤参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 设置 **状态** 为 **开启**。

3. 设置 **SNI 域名** 为目标站点的域名，长度不能超过 1024 个字符。

4. 配置完成后，点击 **保存**。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/048653b23b544ed8a70a085e7ed7c2cb~tplv-goo7wpa0wc-image.image) </span>
