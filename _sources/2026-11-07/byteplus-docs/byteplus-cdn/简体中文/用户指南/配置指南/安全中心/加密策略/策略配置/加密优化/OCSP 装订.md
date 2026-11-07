---
title: "OCSP 装订"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-ocsp-stapling-1-cn"
---

本文档介绍 BytePlus CDN 提供的 "OCSP 装订" 功能。

<span id="什么是-ocsp-装订"></span>
## 什么是 OCSP 装订

OCSP 是在线证书状态协议，英文全称是 Online Certificate Status Protocol。在 TLS 握手阶段，客户端获取证书后会向该证书的 CA 机构查询该证书的状态。CA 机构会向客户端发送 OCSP 响应。

由于客户端在获得证书时就会向 CA 机构查询证书的状态，容易造成 CA 机构收到大量的查询请求。如果 CA 机构响应慢，会增加 TLS 握手的时间。为了避免这个问题，OCSP 装订就产生了。OCSP 装订允许服务器定期向 CA 机构查询证书状态并在服务器缓存该状态。当服务器向客户端发送证书时，会一起发送该证书的 OCSP 响应。OCSP 响应是经过 CA 机构签名的，不易被伪造。

<span id="ocsp-装订的优缺点"></span>
## OCSP 装订的优缺点

OCSP 装订极大降低了客户端向 CA 机构发送的查询请求，也降低了 TLS 的握手时间。缺点就是客户端获取到的证书状态不一定是最新的。但是可以通过配置服务器向 CA 机构查询证书的时间间隔来降低该缺点带来的影响。

<span id="启用-ocsp-装订"></span>
## 启用 OCSP 装订

BytePlus CDN 提供 "OCSP 装订" 功能，可以提高 TLS 握手效率，提升用户体验。

<span id="前提条件"></span>
### 前提条件

要开启该配置，域名必须已经开启了 HTTPS 加密服务。

<span id="操作步骤"></span>
## 操作步骤


1. 打开 **OCSP 装订** 配置页面。操作步骤参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 设置 **状态** 为 **开启**。

3. 配置完成后，点击 **保存**。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b6d9e2105854f6cb30919a6230bc099~tplv-goo7wpa0wc-image.image) </span>
