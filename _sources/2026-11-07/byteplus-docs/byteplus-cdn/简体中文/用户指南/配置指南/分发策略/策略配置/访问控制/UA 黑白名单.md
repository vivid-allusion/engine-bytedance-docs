---
title: "UA 黑白名单"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-ua-restrictions-cn"
---

本文档介绍如何在 BytePlus CDN 中通过 User\-Agent 请求头来对访问您域名的请求进行限制。

<span id="什么是-user-agent"></span>
## 什么是 User\-Agent

User\-Agent 请求头包含了发起请求的客户端的操作系统版本、CPU 类型、浏览器版本等信息。网站服务器可以针对不同的 User\-Agent 头部的值，返回不同的页面。

在 CDN 中，您可以通过 User\-Agent 字段的值来允许或者阻止特定用户访问您的域名。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您可以在搜索引擎中搜索 “User Agent大全” 来查找常见的 User\-Agent 值。</div>


<span id="fbd97c05"></span>
### **空** User\-Agent

"空 User\-Agent" 的定义是 User\-Agent 头没有值或者请求中不包含 User\-Agent 头。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>User-Agent: null</code> 不被视为是 "空 User\-Agent" 情况。</div>


<span id="操作步骤"></span>
## 操作步骤


1. 打开 **UA 黑白名单** 配置页面。操作步骤参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 设置 **状态** 为 **开启**。

3. 参照以下配置说明。

4. 配置完成后，点击 **保存**。


<span id="配置说明"></span>
### 配置说明


|**配置** |**说明** |
|---|---|
|类型 |该配置有以下选项：<br><br><br>* **白名单**：指定设置的名单类型为白名单。只有用户请求的 User\-Agent 请求头在白名单中，该请求才能访问您的域名。<br><br>* **黑名单**：指定设置的名单类型为黑名单名单。如果用户请求的 User\-Agent 请求头在黑名单中，CDN 会拒绝该请求。<br><br><br>如果一个请求的 User\-Agent 请求头匹配了黑名单或者没有匹配白名单，CDN 会拒绝该请求并返回 403 响应状态码。 |
|User\-Agent 字符串 |输入一个或者多个 User\-Agent。该配置的长度不能超过 30,000 个字符。您最多可以输入 1,000 个 User\-Agent。您输入的 User\-Agent 有以下要求：<br><br><br>* 您可以使用通配符（\*）表示任意数量的字符。但是 `*` 仅可以出现在一个 User\-Agent 的开头和末尾。<br><br>* User\-Agent 不能包含 `**`。<br><br>* User\-Agent 只能包含可打印 ASCII 字符，除了 Delete（ASCII code 127）。<br><br>* 多个 User\-Agent 使用分隔符（`\|`）分隔，或者每行一个 User\-Agent。比如: `*curl*\|*Mozilla*`。<br><br>* User\-Agent 不能只包含空格。 |
|空 User\-Agent 访问 CDN 资源 |表示在 [空 User-Agent](https://docs.byteplus.com/en/docs/18/6932#%E7%A9%BA-user-agent) 场景下，CDN 处理请求的方式。<br><br><br>* 当 **类型** 是 **黑名单** 时，该选项为 **允许空 User\-Agent 访问 CDN 资源**。<br><br>* 当 **类型** 是 **白名单** 时，该选项为 **不允许空 User\-Agent 访问 CDN 资源**。 |
|忽略大小写 |表示 User\-Agent 名单在用于过滤请求时是否区分大小写。 |


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f1823d550374227a0fbb52531b8bc85~tplv-goo7wpa0wc-image.image) </span>
