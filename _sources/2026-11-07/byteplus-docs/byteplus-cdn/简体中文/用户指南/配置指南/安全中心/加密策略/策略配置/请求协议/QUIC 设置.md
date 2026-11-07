---
title: "QUIC 设置"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-quic_1-cn"
---

本文档介绍 BytePlus CDN 对 HTTP/3 和 QUIC 协议支持。

<span id="概述"></span>
## 概述

CDN 支持的 QUIC 协议包括以下这些：


* Google QUIC (gQUIC)：支持的 gQUIC 版本是 Q043、Q046、Q050。

* IETF QUIC：IETF QUIC 是 HTTP/3 使用的传输层协议。


综上所述，CDN 支持 HTTP/3 以及特定版本的 gQUIC。

在 CDN 中，您可以启用 "HTTP/3 (QUIC)" 特性。该特性启用后，CDN 可以处理使用上述协议的用户请求。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">CDN 支持 QUIC 请求的连接复用。当 CDN 节点收到一个 QUIC 请求，且请求的域名启用了 HTTPS，则该请求就可以复用节点上其他 QUIC 请求的连接，只要这些 QUIC 请求使用相同的证书。</div>


<span id="http-3-介绍"></span>
## HTTP/3 介绍

HTTP/3 基于 IETF QUIC，是 HTTP 协议的最新版本，具备以下优势：


* **低延迟**：QUIC 使密钥交换和支持的协议成为初始握手过程的一部分。在服务器响应客户端连接时，响应数据包包含了数据加密所需要的数据。客户端可以使用该数据生成密钥用来加密需要发送的数据包。在建立 HTTPS 连接时，客户端和服务器端首先需要进行 TCP 握手，然后再进行 TLS 握手以建立安全连接。

* **网络切换性能较优**：QUIC 包含一个连接标识符。该标识符唯一地标识客户端与服务器之间的连接。即使客户端的 IP 地址发生了变化，客户端只需要发送一个包含此 ID 的数据包即可与服务端建立连接。对于 TCP 来说，如果客户端的 IP 地址发生了变化，已有的 TCP 连接会超时。之后，客户端不得不进行冗长的过程与服务器重新建立连接。

* **弱网情况下的性能良好**：QUIC 基于 UDP。在丢包和网络延迟严重的情况下，QUIC 仍可保障服务的可用性。


<span id="前提条件"></span>
## 前提条件

要启用该配置，您的域名必须已经启用了 HTTPS 加密服务。

<span id="操作步骤"></span>
## 操作步骤


1. 打开 **QUIC 设置** 配置页面。操作步骤参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 设置 **状态** 为启用。

3. 配置完成后，点击 **保存**。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d579ad7bab734ca2bbe7cc6cf1a32ccd~tplv-goo7wpa0wc-topic.webp) </span>
