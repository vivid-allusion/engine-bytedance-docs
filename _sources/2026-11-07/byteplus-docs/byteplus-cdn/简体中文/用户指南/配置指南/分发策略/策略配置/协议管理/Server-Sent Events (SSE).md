---
title: "Server-Sent Events (SSE)"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/sse-zh-cn"
---

本文档介绍 BytePlus CDN 对 Server\-Sent Events（SSE）的支持方式、识别条件、传输行为及配置步骤。

<span id="e5eee699"></span>
## SSE 概述

Server\-Sent Events（SSE）是基于 HTTP 协议的服务器向客户端**单向**实时推送技术，通过持久化长连接传输文本数据流，适配单向实时通信场景。

<span id="de85d6a9"></span>
### 核心优势


* 轻量易用：基于现有 HTTP 协议栈，客户端通过原生 `EventSource` API 快速接入，开发成本低且兼容主流浏览器。

* 自动重连：客户端 `EventSource` 支持自动重连，并可在重连时通过 `Last-Event-ID` 携带最后接收的事件 ID，为断点续传提供机制基础。


<span id="121d7c22"></span>
### 使用场景


* 实时通知（包括社交消息、订单更新、运维告警）、实时数据监控（包括金融行情、传感器数据）等单向数据传输场景。

* LLM 流式输出：将大语言模型生成的回答分段推送给客户端，实现 “打字机” 式实时反馈，降低首字等待时间，改善实时交互体验。


<span id="febd2412"></span>
## CDN 对 SSE 的支持

启用 SSE 后，CDN 会将符合识别条件的 SSE 请求作为长连接请求处理，通过边缘节点建立连接并透传源站数据流。

<span id="f4d2c8a1"></span>
### 请求识别

当前版本中，客户端请求头携带 `Accept: text/event-stream` 时，CDN 会将该请求识别为 SSE 请求。要形成 SSE 流式响应，源站响应头必须包含 `Content-Type: text/event-stream`，并持续输出符合 SSE 格式的数据流。

如果客户端请求未携带 `Accept: text/event-stream`，即使源站响应头中包含 `Content-Type: text/event-stream`，客户端与边缘节点之间的 HTTP 通信也会按普通 HTTP 请求处理，可能无法获得流式即时转发能力。

<span id="6b9c6511"></span>
### 长连接桥接

客户端请求被路由至就近 CDN 边缘节点后，客户端与边缘节点之间会保持长连接，边缘节点也会将请求透传到源站并与源站保持连接，形成 “客户端 \- 边缘节点 \- 源站” 的持续传输链路。通过该链路，客户端可以就近接入 CDN，由边缘节点回源并转发源站输出的事件流。

<span id="84f98c37"></span>
### 数据流透传

符合 SSE 格式的数据流到达节点后，CDN 采用 “不篡改、不缓存、即时转发” 策略，将数据流推送至客户端。

<span id="275ec1c5"></span>
### 连接复用

如果您启用了 SSE，也建议您启用 HTTP/2。在支持 HTTP/2 回源的场景下，HTTP/2 的多路复用特性允许边缘节点与源站之间在同一条 TCP 连接上复用多个 “流”，同时承载多个客户端的 SSE 数据流，从而减少源站连接数。

<span id="连接中断与恢复"></span>
### 连接中断与恢复

CDN 不保存 SSE 历史事件，也不会在客户端重连后补发已经错过的事件。客户端断线重连后的续传与补发仍依赖客户端重连机制，以及源站基于 `Last-Event-ID` 返回后续事件的能力。

源站长时间无数据输出时，连接可能因回源 HTTP 请求超时中断。BytePlus CDN 的回源 HTTP 请求超时时间默认是 60 秒，可配置范围是 5–60 秒；建议源站的心跳间隔小于该超时时间，并由客户端处理断线重连。

<span id="71503458"></span>
## 操作步骤


1. 进入目标加速域名的配置页面，打开 **Server\-Sent Events** 配置项。操作步骤参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 设置 **状态** 为启用。

3. 设置完成后，点击 **保存**。

4. 配置生效后，使用客户端程序或命令行工具访问 SSE 测试 URL，确认请求头已携带 `Accept: text/event-stream`，源站响应头包含 `Content-Type: text/event-stream`，且客户端可以持续接收事件流。示例命令如下：


```shell
curl -N -H "Accept: text/event-stream" "https://example.com/sse"
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61c794688b33485a92f58dfe243ad55c~tplv-goo7wpa0wc-topic.webp) </span>
