---
title: "PROXY Protocol"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/proxy-protocol_zh-cn"
---

**背景**

PROXY 协议（PROXY protocol）是一种网络协议，旨在解决代理环境中服务器无法获取客户端真实信息的问题。这些信息包括客户端的 IP 地址和端口，以及客户端需要访问的目标 IP 地址和端口。在与服务器建立 TCP/UDP 连接时，代理服务器会发送 PROXY 协议头来传输客户端的真实信息。

**特性介绍**

BytePlus CDN 支持 PROXY 协议，涵盖版本 1 和版本 2。当您在 CDN 中启用了 PROXY 协议，CDN 就可以对收到的 PROXY 协议头进行解析，以获取客户端的真实 IP 地址。

**使用场景**

在您的业务架构中，CDN 前部署了代理，譬如 BytePlus Global Accelerator（GA），并且该代理会发送 PROXY 协议头。您还配置了 IP 黑白名单，希望根据客户端的真实 IP 地址控制对 CDN 的访问。

**操作步骤**


1. 打开 **PROXY Protocol** 配置页面。操作步骤参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 设置 **状态** 为启用。

3. 设置完成后，点击 **保存**。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_7921e3114ec98fcfe067001899384b08.png) </span>
