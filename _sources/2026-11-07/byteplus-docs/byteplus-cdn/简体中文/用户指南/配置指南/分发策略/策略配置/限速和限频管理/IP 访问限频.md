---
title: "IP 访问限频"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/qps_throttling_cn"
---

本文档介绍 BytePlus CDN 中的 "IP 访问限频" 功能。您可以使用该功能对限制客户端 IP 地址的 QPS。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">要使用该功能，请 <a href="https://console.byteplus.com/workorder/create">提交工单</a>。</div>


<span id="功能概述"></span>
## 功能概述

一个客户端 IP 地址的 QPS 指的是该 IP 地址每秒向域名发送的请求数。QPS 是在边缘节点统计的。

如果您的域名遭受了 CC 攻击，该域名可能会在短时间内消耗大量的流量，导致高额账单。为了降低 CC 攻击带来的风险，您可以启用 "IP 访问限频"。

启用 "IP 访问限频" 后，如果来自某个 IP 地址的请求 QPS 超过了您设置的 QPS 阈值，在收到来自该 IP 地址的新请求时，CDN 会拒绝处理新请求并响应 403 状态码。

<span id="设置合理的-qps-阈值"></span>
## 设置合理的 QPS 阈值

QPS 阈值如果设置得太小，用户可能无法正常访问您的站点。但是如果 QPS 阈值设置得太大，也失去了设置 QPS 阈值的意义。

您可以使用 CDN 控制台的 [边缘监控页面](https://docs.byteplus.com/en/docs/byteplus-cdn/nqffUP) 查看域名的历史 QPS，然后估算一个适合您域名的 QPS 阈值。建议您可以特别留意 QPS 峰值，判断这些峰值是否符合您的预期。

<span id="操作步骤"></span>
## 操作步骤


1. 打开 **IP 访问限频** 配置页面。操作步骤参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 设置 **状态** 为 **开启**。

3. 设置 **阈值** 为一个合理的 QPS 值。您可以设置的值的范围是 1\-1,000,000。

4. 在页面右下方，点击 **保存**。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69f36e8b9c0644f4aad9c4d4eca2256c~tplv-goo7wpa0wc-topic.webp) </span>
