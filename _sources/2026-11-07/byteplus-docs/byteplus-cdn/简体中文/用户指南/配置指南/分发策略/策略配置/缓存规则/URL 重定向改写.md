---
title: "URL 重定向改写"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-url-redirect-cn"
---

本文档介绍如何在 BytePlus CDN 中配置 URL 重定向改写。当用户请求匹配规则时，CDN 会返回指定的 `3xx` 状态码和新的 URL，客户端随后向新 URL 发起请求。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">要使用此特性，请<a href="https://console.byteplus.com/workorder/create">提交工单</a>。</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d38b87e8a9e4b82b88aa9c020f5e837~tplv-goo7wpa0wc-topic.webp) </span>

<span id="使用场景"></span>
## 使用场景

当用户常访问的内容路径发生变更时，您可以选择以下方式之一：


* 在源站配置重定向，并在 CDN 中开启 [回源重定向跟随](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-redirect-follow-cn)。

* 在 CDN 配置 **URL 重定向改写**。CDN 向客户端返回 `3xx` 响应，客户端请求新的 URL。

* 在 CDN 配置 [回源路径改写](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-origin-path-rewrite_1-cn)。CDN 仅使用新路径向源站发起请求，客户端请求的 URL 不会改变。


本文介绍第二种方式。

<span id="注意事项"></span>
## 注意事项


* 请确保重定向后的 URL 不会再次命中当前规则或其他 **URL 重定向改写** 规则。CDN 不会自动阻止重定向循环；发生循环时，客户端会持续收到 `3xx` 响应，直至达到自身的最大重定向次数。

* 如果 **目标 Host** 不是加速域名，客户端对重定向 URL 的请求不会经过 CDN 加速。

* **目标路径** 不能包含连续斜杠（`//`）、百分号（`%`）、空格或问号（`?`）。


<span id="匹配与替换规则"></span>
## 匹配与替换规则

**重写路径** 是用于匹配请求 URL 路径的正则表达式，最长为 1,024 个字符。**目标路径** 是替换字符串，用于替换 **重写路径** 匹配到的内容。


* 未使用 `^` 和 `$` 时，规则可以匹配路径中的一部分。仅匹配到的内容会被替换，未匹配的前缀和后缀会保留。

* 使用 `^` 和 `$` 时，规则仅匹配完整路径。

* 您可以在正则表达式中使用捕获组。`$1`、`$2` 等分别表示第 1 个、第 2 个捕获组匹配到的内容。


例如，请求路径为 `/old/images/logo.png`，**重写路径** 为 `^/old/(.*)$`，**目标路径** 为 `/new/$1` 时，重定向路径为 `/new/images/logo.png`。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>目标路径</strong> 替换的是正则表达式匹配到的内容，而不是必然替换完整路径。这与 <a href="https://docs.byteplus.com/zh-CN/docs/byteplus-cdn/docs_cn-origin-path-rewrite_1-cn">回源路径改写</a> 中的 <strong>CDN 回源路径</strong> 不同：<strong>CDN 回源路径</strong> 会替换完整请求路径。</div>


<span id="操作步骤"></span>
## 操作步骤


1. 打开 **URL 重定向改写** 配置页面。具体操作参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 单击 **添加规则**。

   最多可添加 50 条规则。

3. 按照以下说明完成规则配置。

4. 单击 **保存**。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b13de6d9d02a47d1b08c1cb940469879~tplv-goo7wpa0wc-topic.webp) </span>

<span id="配置说明"></span>
## 配置说明


|配置 |说明 |
|---|---|
|重写路径 |用于匹配请求 URL 路径的正则表达式。支持捕获组，最长为 1,024 个字符。有关匹配和替换的说明，参见[匹配与替换规则](https://docs.byteplus.com/en/docs/18/6951#%E5%8C%B9%E9%85%8D%E4%B8%8E%E6%9B%BF%E6%8D%A2%E8%A7%84%E5%88%99)。 |
|跳转方式 |CDN 返回的重定向状态码。可选 `301`、`302`、`303`、`307` 或 `308`。<br><br>&nbsp;<br><br>`301` 和 `308` 适用于永久变更，`302` 和 `307` 适用于临时跳转。`303` 要求客户端使用 `GET` 方法请求新 URL。对于 `301` 和 `302`，如果原请求不是 `GET`，客户端请求新 URL 时可能改用 `GET`。对于 `307` 和 `308`，客户端请求新 URL 时保留原请求方法。 |
|目标协议 |重定向 URL 使用的协议。<br><br><br>* **跟随请求**：使用原请求的协议。<br><br>* **HTTP**：使用 HTTP 协议。<br><br>* **HTTPS**：使用 HTTPS 协议。 |
|目标 Host |重定向 URL 中的域名或 IPv4 地址。域名最长为 1,024 个字符。 |
|目标路径 |用于替换匹配内容的字符串，最长为 1,024 个字符。不能包含连续斜杠（`//`）、百分号（`%`）、空格或问号（`?`）。 |
|目标参数 |重定向 URL 中查询参数的处理方式。<br><br><br>* **保留全部**：保留原请求中的所有查询参数。<br><br>* **删除全部**：删除原请求中的所有查询参数。<br><br>* **保留部分**：仅保留指定名称的查询参数。<br><br>* **删除部分**：删除指定名称的查询参数，保留其他查询参数。 |
|参数名称 |当 **目标参数** 为 **保留部分** 或 **删除部分** 时，输入要保留或删除的参数名称。多个参数名称之间使用分号（`;`）分隔，最长为 1,024 个字符。参数名称不能包含连续斜杠（`//`）、百分号（`%`）、双引号（`"`）或空格。 |


<span id="规则优先级"></span>
## 规则优先级

CDN 按规则在列表中从上到下的顺序匹配请求。命中第一条规则后，CDN 应用该规则并停止匹配后续规则。

更具体的规则应排在更通用的规则之前。例如，规则 `^/images/logo/(.*)$` 应排在 `^/images/(.*)$` 之前；否则，请求 `/images/logo/a.png` 会先命中通用规则。

您可以拖动规则调整其顺序。

<span id="配置示例"></span>
## 配置示例

<span id="完整路径匹配"></span>
### 完整路径匹配

以下规则将 `/old/images/` 下的请求重定向到 `/new/images/`。


|配置 |值 |
|---|---|
|重写路径 |`^/old/images/(.*)$` |
|目标路径 |`/new/images/$1` |


请求 `https://example.com/old/images/logo.png` 会重定向至 `https://example.com/new/images/logo.png`。

<span id="局部路径替换"></span>
### 局部路径替换

以下规则仅替换路径中匹配到的 `legacy/` 部分，未匹配的路径前缀会保留。


|配置 |值 |
|---|---|
|重写路径 |`legacy/(.*)` |
|目标路径 |`modern/$1` |


请求 `https://example.com/static/legacy/logo.png` 会重定向至 `https://example.com/static/modern/logo.png`。

<span id="查询参数筛选"></span>
### 查询参数筛选

以下规则仅保留名称为 `keep` 的查询参数。


|配置 |值 |
|---|---|
|重写路径 |`^/old$` |
|目标路径 |`/new` |
|目标参数 |**保留部分** |
|参数名称 |`keep` |


请求 `https://example.com/old?keep=1&drop=2` 会重定向至 `https://example.com/new?keep=1`。
