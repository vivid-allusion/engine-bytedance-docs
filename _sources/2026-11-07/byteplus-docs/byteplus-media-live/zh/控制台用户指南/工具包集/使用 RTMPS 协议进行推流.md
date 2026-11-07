---
title: "使用 RTMPS 协议进行推流"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/pushrtmps-zh-CN"
---

本文档介绍如何使用 RTMPS 协议进行推流。

<span id="a7833f99"></span>
## 背景

RTMP（实时消息协议）是一种网络类型协议，用于在 Flash 播放器和服务器之间传输音视频流。RTMP 基于 TCP 协议，默认使用 1935 端口。它是一种标准的、未加密的实时消息协议。

RTMPS 是 RTMP 的一个变体。它是基于 TLS/SSL 的 RTMP。它通过 SSL 在传输层加密网络类型连接。默认端口为 443。RTMPS 很好地解决了 RTMP 的安全问题。

<span id="f8e509fb"></span>
## 操作流程

<span id="b9d50a28"></span>
### **配置 RTMPS 功能**

默认情况下，BytePlus MediaLive 会为推流域名启用 RTMPS 功能。但要使 RTMPS 功能生效，需先为推流域名配置证书和 HTTPS。关于证书配置方法，请参见[Managing SSL certificate](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-managing-certificates)。关于 HTTPS 配置方法，请参见 [HTTPS configuration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-https)。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71d9f2ce91014b28949f804b853d0d89~tplv-goo7wpa0wc-image.image) </span>

<span id="71183a08"></span>
### 使用 RTMPS 协议进行推流

可通过修改 RTMP 地址获取 RTMPS 地址并进行推流。


1. 使用**地址生成器**获取 RTMP 推流地址。

2. 将生成的 RTMP 推流地址协议头更改为**RTMPS**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/963694262ccc4a95b165175e5a43d3fc~tplv-goo7wpa0wc-image.image) </span>

3. 将 RTMPS 推流地址输入到 OBS 软件中即可开始推流。播放器可按照正常拉流回放流程。支持 RTMP、FLV、HLS 和 RTM 协议。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52462e79c96d4196a2ce6aa3a9d8906d~tplv-goo7wpa0wc-image.image) </span>
