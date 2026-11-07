---
title: "Referer 防盗链"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-referer-restrictions-cn"
---

在 BytePlus CDN 中，您可以配置 "Referer 防盗链"，阻止包含特定 Referer 的请求访问 CDN，从而防止您网站的内容被盗链。

如果用户请求由于满足您的 "Referer 防盗链" 配置而被 CDN 拒绝，CDN 响应 403 状态码。

<span id="注意事项"></span>
## 注意事项

当一个用户请求被 CDN 拒绝时，以下用量依然会被统计。


* CDN 对该请求的响应会被计入 CDN 向用户传输的数据量，虽然该数据量很小。

* 如果该请求是一个 HTTPS 请求，该请求会被计入 HTTPS 请求数。


<span id="referer-介绍"></span>
## Referer 介绍

Referer 是 HTTP 请求中的一个头部，用来记录请求的来源页面。一般来说，Referer 是一个完整 URL，包含 scheme、域名、路径和查询字符串。

当您点击网页 A 中的一个链接时，浏览器会向链接所指向目标页面发送 HTTP 请求。请求中包含 Referer 头部，头部值就是网页 A 的 URL。

<span id="空-referer"></span>
### 空 Referer

空 Referer 指的是 HTTP 请求中不包含 Referer 头部。在 "Referer 防盗链" 中，您可以配置 CDN 如何处理不包含 Referer 头部的用户请求。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>Referer: null</code> 不被视为是 "空 Referer" 情况。</div>


**空 Referer 场景**

通常，空 Referer 出现在以下任意场景中：


* 您通过浏览器中的书签访问目标页面。

* 您在浏览器地址栏中输入 URL 访问目标页面。

* 您在一个 HTTPS 页面中点击链接访问一个 HTTP 页面。

* 您使用浏览器提供的隐私浏览模式。

* 如果您访问的页面满足以下任意条件，您在该页面中点击任何链接时，HTTP 请求中不包含 Referer 头部。

   * 页面的 `<meta>` 标签中声明了 `Referrer-Policy: no-referrer`。

   * 包含该页面的服务器响应中存在 `Referrer-Policy: no-referrer` 头部。


<span id="功能优先级"></span>
## 功能优先级

CDN 提供的一系列访问控制功能有不同的优先级。在 CDN 处理用户请求时，这些功能按优先级对请求生效。参见 [访问控制功能的优先级](https://docs.byteplus.com/en/docs/byteplus-cdn/access-restrictions-priority_cn)。

<span id="操作步骤"></span>
## 操作步骤


1. 打开 **Referer 防盗链** 配置页面。操作步骤参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 设置 **状态** 为开启。

3. 参照以下 [配置说明](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-referer-restrictions-cn#%E9%85%8D%E7%BD%AE%E8%AF%B4%E6%98%8E)。

4. 配置完成后，点击 **保存**。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1099707bc98e2254ca820fe84a03a16c.png) </span>

<span id="配置说明"></span>
## 配置说明


|配置 |说明 |
|---|---|
|类型 |表示名单的类型。该配置有以下选项：<br><br><br>* **白名单**：指定一个白名单。如果用户请求中的 Referer 不匹配该清单，CDN 会拒绝请求。<br><br>* **黑名单**：指定一个黑名单。如果用户请求中的 Referer 匹配该清单，CDN 会拒绝请求。 |
|配置方式 |表示清单中条目的来源。该配置有以下选项：<br><br><br>* 策略配置：表示名单中的条目在 **常规名单** 和 **正则名单** 中配置。<br><br>* 全局配置：表示名单中的条目来自一个 [全局配置](https://docs.byteplus.com/en/docs/byteplus-cdn/universal-catalog_cn)。全局配置用来定义大量条目。一个全局配置最多可以包含 4,000 个条目。 |
|规则内容 |表示名单的配置选项，包含：<br><br><br>* 常规名单：名单中的每个条目是一个 IP 地址或者域名，用来对 Referer 中的 hostname 进行匹配校验。<br><br>* 正则名单：名单中的每个条目是一个正则表达式，用来对 Referer 中的完整 URL 进行匹配校验。<br><br>* 空 Referer：表示在 [空 Referer](https://docs.byteplus.com/en/docs/18/6933#%E7%A9%BA-referer) 场景下，CDN 处理请求的方式。<br><br>   * 勾选：表示如果请求不包含 Referer 头部，则该请求被认为**匹配**您配置的名单。<br><br>   * 不勾选：表示如果请求不包含 Referer 头部，则该请求被认为**不匹配**您配置的名单。 |
|常规名单（输入框） |表示一个常规名单。如果您在 **规则内容** 下勾选了 **常规名单**，该输入框会出现。<br><br>**输入要求**<br><br>名单最多可以包含 1,000 个条目，总长度不能超过 30,000 个字符。您可以输入一个或者多个域名和 IP 地址。域名可以是泛域名。IP 地址只能是 IPv4 地址或者 IPv4 CIDR 地址。多个条目之间使用分号（;）分隔或者每个条目一行。<br><br>如果您需要输入的条目数量超过 1,000，参考 [全局配置](https://docs.byteplus.com/en/docs/byteplus-cdn/universal-catalog_cn)。<br><br>**关于泛域名和子域名**<br><br><br>* 泛域名不匹配域名本身。例如：`*.example.com` 不匹配 `example.com`，但是匹配 `www.example.com`、`a.a.example.com` 等。<br><br>* 子域名的级别数量没有限制。例如，您可以在名单中指定 `aaa.bbb.ccc.ddd.eee.fff.ggg.eee.example.com`。 |
|忽略大小写 |表示常规名单中的条目是否是大小写敏感的。 |
|忽略 Scheme 校验 |表示 CDN 是否对 Referer 中的 scheme 进行校验，也就是校验 Referer 是否包含 `http://` 或者 `https://`。该配置有以下选项：<br><br><br>* 勾选：表示 CDN 不校验 Referer 是否包含 scheme。在这个情况下，无论 Referer 是否包含 scheme，CDN 都会将 Referer 与您配置的名单进行匹配校验。<br><br>* 不勾选：表示 CDN 会先校验 Referer 是否包含 scheme。只有 Referer 包含 scheme，CDN 才会将 Referer 与您配置的名单进行匹配校验。否则，CDN 判定请求与您配置的名单不匹配。<br><br><br>该配置对**正则名单**不生效，因为 CDN 依赖正则表达式来判断 Referer 是否匹配正则名单。 |
|正则名单（输入框） |表示一个正则表达式名单，用于对 Referer 中的完整 URL 进行匹配校验。您最多可以指定 100 个正则表达式，每个正则表达式一行。如果您在 **规则内容** 下勾选了 **正则名单**，该输入框会出现。 正则名单中的条目不区分大小写。 |


<span id="配置示例"></span>
## 配置示例

假设您配置的名单中包含以下条目：


* www.example.com

* \*.example.com


相关设置及匹配结果如下表所示：


|**名单类型** |**用户请求中的 Referer** |**忽略大小写** |**忽略 Scheme 校验** |**空 Referer** |**匹配结果** |
|---|---|---|---|---|---|
|黑名单 |https://www.eXampLe.com/file?p=v |勾选 |N/A ||拒绝请求 |
|||不勾选 |||接受请求 |
||www.example.com/file?p=v |N/A |勾选 |N/A |拒绝请求 |
||||不勾选 ||接受请求 |
||不包含 Referer 头部 |N/A ||勾选 |拒绝请求 |
|||||不勾选 |接受请求 |
||https://www.example.com |N/A |||拒绝请求 |
||https://docs.www.example.com ||||拒绝请求 |
||https://example.com ||||接受请求 |
|白名单 |https://www.eXampLe.com/file?p=v |勾选 |N/A ||接受请求 |
|||不勾选 |||拒绝请求 |
||www.example.com/file?p=v |N/A |勾选 |N/A |接受请求 |
||||不勾选 ||拒绝请求 |
||不包含 Referer 头部 |N/A ||勾选 |接受请求 |
|||||不勾选 |拒绝请求 |
||https://www.example.com |N/A |||接受请求 |
||https://docs.www.example.com ||||接受请求 |
||https://example.com ||||拒绝请求 |
