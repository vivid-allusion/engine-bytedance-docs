---
title: "Origin 防盗链"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-origin-restrictions-cn"
---

本文档介绍如何在 BytePlus CDN 中配置 Origin 防盗链。

Origin 是一个 HTTP 请求头，用于指示请求的来源域名。Origin 头包含协议，域名和端口，不包含路径与查询字符串。端口号是可选的。

<span id="origin-防盗链"></span>
## Origin 防盗链

Origin 头的作用之一是防盗链。您可以为您的站点配置一个 Origin 黑名单以拒绝来自指定域名的请求。或者您可以为您的站点配置一个 Origin 白名单只允许接受来自指定域名的请求。

<span id="关于空-origin"></span>
## **空 Origin**

"空 Origin" 的定义是 Origin 头没有值或者请求中不包含 Origin 头。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>Origin: null</code> 不被视为是 "空 Origin" 情况。</div>


<span id="操作步骤"></span>
## 操作步骤


1. 打开 **Origin 防盗链** 配置页面。操作步骤参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 设置 **状态** 为 **开启**。

3. 参照以下配置说明。

4. 配置完成后，点击 **保存**。



|**配置** |**说明** |
|---|---|
|类型 |该配置有以下选项：<br><br><br>* **白名单**：当您只想允许来自某些域名的请求时，可以配置一个白名单。如果用户的请求不匹配白名单，CDN 拒绝请求并且响应 403 状态码<br><br>* **黑名单**：当您只想阻止来自某些域名的请求时，可以配置一个黑名单。如果用户的请求匹配了黑名单，CDN 拒绝请求并且响应 403 状态码。 |
|源站 |输入一个或者多个 Origin 条目。名单的长度不能超过 30,000 个字符。您可以输入一个或者多个域名（支持子域名和泛域名）和 IP 地址（ 支持 IPv4 地址、IPv6 地址、CIDR 网段）。多个条目使用分号（;）或换行符分隔。您最多可以输入 100 个条目。需要注意的是，二级域名被认为是单个域名，不是泛域名。泛域名不包含二级域名本身。例如：`*.test.com` 不包含二级域名 `test.com`，但是包含 `www.test.com`、`a.a.test.com` 等。<br><br>子域名的级别数量没有限制。 关于 Origin 名单的匹配逻辑，参见 [Origin 匹配逻辑](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-origin-restrictions-cn#origin-%E5%8C%B9%E9%85%8D%E9%80%BB%E8%BE%91)。 |
|空 Origin 访问 CDN 资源 |表示在 [空 Origin](https://docs.byteplus.com/en/docs/18/6934#%E7%A9%BA-origin) 场景下，CDN 处理请求的方式。<br><br><br>* 如果 **类型** 是 **黑名单**，该选项是 **允许空 Origin 访问 CDN 资源**。<br><br>* 如果 **类型** 是 **白名单**，该选项是 **不允许空 Origin 访问 CDN 资源**。 |
|忽略大小写 |表示 Origin 在用于过滤请求时是否区分大小写。 |


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07835504991d44c283bc9d8b54caf3b7~tplv-goo7wpa0wc-image.image) </span>

<span id="origin-匹配逻辑"></span>
## Origin 匹配逻辑

我们通过以下名单配置为例，阐述 Origin 头的匹配逻辑。如果一个请求未匹配白名单或者匹配了黑名单，CDN 会拒绝请求并返回 403 响应状态码。


|**名单配置** |**用户请求中 Origin 头** |**匹配？**  |**匹配逻辑说明** |
|---|---|---|---|
|* www.test.com<br><br>* 1.1.1.1<br><br>* 2001:0db8:3c4d:0015:0000:0000:1a2f:1a2b<br><br>* \*.test.com |http://www.test.com |是 |Origin 头中的域名匹配名单。 |
||http://www.test.com:80 |是 ||
||www.test.com |否 |Origin 头不符合 HTTP 协议规范。规范要求 Origin 头部值必须是以下格式之一：<br><br><br>* scheme://host:port<br><br>* scheme://host |
||2001:0db8:3c4d:0015:0000:0000:1a2f:1a2b |否 ||
||http://2001:0db8:3c4d:0015:0000:0000:1a2f:1a2b |否 |Origin 头不符合 HTTP 协议规范。规范要求当 host 是一个 IPv6 地址时，该地址必须包裹在 `[]` 中。 |
||http://[2001:0db8:3c4d:0015:0000:0000:1a2f:1a2b] |是 |Origin 头中的 IP 地址匹配名单。 |
||http://aaa.test.com |是 |Origin 头中的多级域名匹配名单中的泛域名条目。 |
||http://ss.aaa.test.com |是 ||
||http://test.com |否 |Origin 头中的二级域名不匹配名单中的泛域名条目。原因是泛域名不包含二级域名本身。 |
