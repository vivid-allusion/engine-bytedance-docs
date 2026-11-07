---
title: "WebSocket"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/websocket_cn"
---

本文介绍如何在 BytePlus CDN 中启用 WebSocket，并配置 WebSocket 超时时间。

<span id="功能说明"></span>
## 功能说明

WebSocket 是一种基于单个 TCP 连接的全双工通信协议，适用于实时聊天、在线游戏和实时数据更新等需要双向通信的场景。

CDN 默认关闭 WebSocket。启用后，客户端发起 WebSocket 请求时，CDN 节点会与源站建立 WebSocket 连接，并在客户端、CDN 节点与源站之间转发 WebSocket 消息。

<span id="websocket-超时时间"></span>
## WebSocket 超时时间

WebSocket 超时时间用于控制 CDN 节点与源站之间 WebSocket 连接的空闲时长。默认值为 60 秒。如果连接在设定时长内没有数据收发，CDN 会断开该连接。

您可以根据业务的消息发送间隔设置 WebSocket 超时时间。该参数的单位为秒，取值范围为 1–900，默认值为 60。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">WebSocket 超时时间应大于或等于 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-request-time-out-cn">回源请求超时</a> 中的 <strong>HTTP 读取超时</strong>。否则，源站发送的 WebSocket 消息可能无法正常传递。</div>


<span id="操作步骤"></span>
## 操作步骤


1. 打开 **WebSocket** 配置页面。操作步骤参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 设置 **状态** 为启用。

3. 设置 **WebSocket 超时时间**。

4. 设置完成后，点击 **保存**。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66afa68256624bfcaebc18ecab2eb559~tplv-goo7wpa0wc-topic.webp) </span>
