---
title: "IP 黑白名单"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-ip-restrictions-cn"
---

本文档介绍如何在 BytePlus CDN 中配置 IP 黑白名单。

您可以配置 IP 黑名单或者白名单，基于客户端 IP 对请求进行过滤。

<span id="功能优先级"></span>
## 功能优先级

CDN 提供的一系列访问控制功能有不同的优先级。在 CDN 处理用户请求时，这些功能按优先级对请求生效。参见 [访问控制功能的优先级](https://docs.byteplus.com/en/docs/byteplus-cdn/access-restrictions-priority_cn)。

<span id="操作步骤"></span>
## 操作步骤


1. 打开 **IP 黑白名单** 配置页面。操作步骤参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 设置 **状态** 为开启。

3. 参照以下 [配置说明](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-ip-restrictions-cn#%E9%85%8D%E7%BD%AE%E8%AF%B4%E6%98%8E)。

4. 配置完成后，点击 **保存**。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/442b27e542ac416ea437d4b65957c3bf~tplv-goo7wpa0wc-topic.webp) </span>

<span id="配置说明"></span>
## 配置说明


|配置 |说明 |
|---|---|
|类型 |该配置的可选值如下：<br><br><br>* **白名单**：指定来自哪些 IP 地址的请求允许访问您的域名。当您只想 CDN 允许来自某些 IP 的请求时，可以配置白名单。<br><br>* **黑名单**：指定来自哪些 IP 地址的请求不允许访问您的域名。当您只想 CDN 阻止来自某些 IP 的请求时，可以配置黑名单。<br><br><br>如果一个请求的来源 IP 匹配了黑名单或者没有匹配白名单，CDN 会拒绝该请求并返回 403 响应状态码。 |
|配置方式 |表示名单中条目的来源。该配置有以下选项：<br><br><br>* 策略配置：表示名单中的条目是在 **规则内容** 中配置的。<br><br>* 全局配置：表示名单中的条目来自一个 [全局配置](https://docs.byteplus.com/en/docs/byteplus-cdn/universal-catalog_cn)。全局配置用来定义大量条目的。一个全局配置最多可以包含 30,000 个条目。 |
|规则内容 |表示 **类型** 对应的 IP 地址条目，最多包含 1,000 个条目，总长度不超过 30,000 个字符。当 **配置方式** 是 **策略配置** 时，该配置会出现。<br><br>每个条目可以是一个 IP 地址、一个 CIDR 网段或者一个 IP 地址范围。IP 地址的格式只能是 IPv4。每个条目需要分行输入。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">如果您需要输入的 IP 地址数量超过 1,000，参考 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/universal-catalog_cn">全局配置</a>。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">不支持输入 <code>0.0.0.0/0</code>。要表示所有 IP 地址，请输入以下组合：</div><br><br><br>   <div data-tips="true" data-tips-type="tip"><code>0.0.0.0/1</code>   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip"><code>128.0.0.0/1</code>   </div><br>    |
|IP 判断来源 |指定 CDN 判断客户端 IP 地址时使用的来源。<br><br>&nbsp;<br><br>支持以下选项：<br><br><br>* **默认逻辑**：CDN 使用真实建连 IP 判断客户端 IP 地址。真实建连 IP 是与 CDN 节点直接建立网络连接的对端 IP 地址。<br><br>* **自定义**：从真实建连 IP、`X-Forwarded-For` 请求头和 `X-Real-IP` 请求头中选择一个或多个来源，以判断客户端 IP 地址。无法从已选请求头获取 IP 地址时，CDN 使用真实建连 IP。<br><br>   * 对于黑名单，只要任一指定来源中获取的 IP 地址在黑名单中，CDN 就拒绝请求。<br><br>   * 对于白名单，只有所有指定来源中获取的 IP 地址均在白名单中，CDN 才允许请求。 |
|响应状态码 |表示 CDN 在拒绝请求时响应的状态码，范围是 200 \- 999。如果不指定该配置，则 CDN 默认响应 403 状态码。 |


<span id="配置示例"></span>
## 配置示例

**白名单**

规则：

> 192.0.2.0/24

> 203.0.113.8\-203.0.113.15


作用：仅允许满足以下任一条件的 IP 地址向您的域名发送请求：


* IP 地址在 192.0.2.1\-192.0.2.254、203.0.113.8\-203.0.113.15 范围内。


**黑名单**

规则

> 198.51.100.25


作用：如果 IP 地址满足以下任一条件，则不允许来自该 IP 地址的请求。


* IP 地址是 198.51.100.25。
