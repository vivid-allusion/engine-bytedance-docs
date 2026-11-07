---
title: "回源 URL 改写"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-origin-path-rewrite_1-cn"
---

本文档介绍如何在 BytePlus CDN 中配置回源 URL 改写。该功能允许对 CDN 回源请求 URL 中的路径和查询参数进行改写。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip">要使用该功能，请 <a href="https://console.byteplus.com/workorder/create">提交工单</a>。</div>


<span id="功能概述"></span>
## 功能概述

在源站上，假设某些文件的 URL 或者 URL 发生了变更。此时，有以下几种解决方案：


* 在源站配置 301 或 302 重定向，将内容的原 URL 重定向到新的 URL。同时，在 CDN 中启用 [回源重定向跟随](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-redirect-follow-cn) 功能。

* 不在源站做任何变更，而是在 CDN 中配置 [URL 重定向改写](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-url-redirect-cn)功能。如果用户请求了原 URL，CDN 会响应 301 或者 302 状态码，指示用户浏览器向新的 URL 发送请求。

* 不在源站做任何变更，而是在 CDN 配置 **回源 URL 改写**。如果用户请求了原 URL，CDN 在回源请求中会使用新的 URL。


本文档介绍的是第三种解决方案。

<span id="请求流程"></span>
## **请求流程**

在您对某个文件配置了 "回源 URL 改写" 后，请求的流程如下：


1. 用户请求文件。

2. 如果该文件未被缓存，CDN 根据配置，将用户请求 URL 改写成新的 URL，然后向源站发起请求。

3. CDN 获取文件后，将该文件返回给用户。同时，CDN 缓存该文件。需要留意的是，该文件的缓存键中保存的是用户请求 URL，而非改写后的 URL。关于缓存键的介绍，参见 [配置缓存键值](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-cache-keys-cn)。


<span id="操作步骤"></span>
## 操作步骤


1. 打开 **回源 URL 改写** 配置页面。操作步骤参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 点击 **新增**。

   您最多可以添加 50 条规则。

3. 参照以下配置说明。

4. 配置完成后，点击 **保存**。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f08686ab2ed4d29933f4c846d178cb4~tplv-goo7wpa0wc-topic.webp) </span>

<span id="配置说明"></span>
## 配置说明

&nbsp;


|**配置** |**说明** |
|---|---|
|改写类型 |表示改写类型。该配置有以下取值：<br><br><br>* **路径改写**：表示对回源 URL 中的路径进行改写。<br><br>* **URL 改写**：表示对回源 URL 中的路径和查询字符串进行改写。 |


<span id="路径改写"></span>
### 路径改写

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec9dff63729c4a84b5b0dfadffdf1a33~tplv-goo7wpa0wc-topic.webp) </span>

当 **改写类型** 是 **路径改写** 时，"回源 URL 改写" 的配置说明如下：


|**配置** |**说明** |
|---|---|
|用户请求路径 |表示一个正则表达式，长度不能超过 1,024 个字符，用于匹配用户请求 URL 中路径。 |
|回源路径 |表示改写后，回源请求 URL 中的路径，长度不能超过 1,024 个字符。您可以在路径中使用 `$1`、`$2`、`$3` 等捕获 **用户请求路径** 中定义的组。 |


参见 [路径改写配置示例](https://docs.byteplus.com/en/docs/18/6964#%E8%B7%AF%E5%BE%84%E6%94%B9%E5%86%99%E9%85%8D%E7%BD%AE%E7%A4%BA%E4%BE%8B)。

<span id="url-改写"></span>
### URL 改写

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_013250c321ba724edc691e0013023a91.png) </span>

当 **改写类型** 是 **URL 改写** 时，"回源 URL 改写" 的配置说明如下：


|**配置** |**说明** |
|---|---|
|请求 URL |表示一个正则表达式，长度不能超过 1,024 个字符，用于匹配用户请求 URL 中的路径和查询字符串。 |
|回源 URL |表示改写后的路径和查询字符串，长度不能超过 1,024 个字符。您可以使用 `$1`、`$2`、`$3` 等捕获 **请求 URL** 中定义的组。 |


参见 [URL 改写配置示例](https://docs.byteplus.com/en/docs/18/6964#url-%E6%94%B9%E5%86%99%E9%85%8D%E7%BD%AE%E7%A4%BA%E4%BE%8B)。

<span id="规则优先级"></span>
## 规则优先级

在规则列表中，每条规则都有优先级。优先级为 1 的规则具有最高优先级。当收到一个用户请求时，CDN 按规则的优先级，从高到低尝试将请求与规则匹配。如果请求匹配了一条规则，匹配过程就停止了。您可以拖动规则来调整优先级。

<span id="配置示例"></span>
## 配置示例

<span id="路径改写配置示例"></span>
### 路径改写配置示例


|**请求 URL 中的路径** |**用户请求路径（包含组**  **`(.*)`**  **）**  |**回源路径** |**重定向路径** |**说明** |
|---|---|---|---|---|
|`/a/bbb/image.png` |`^/a{1,2}(.*)g$`<br><br>用于匹配以 `/` 开头和以 `g` 结尾的路径。 |`/food/$1` |`/food//bbb/image.pn` |正则表达式匹配了请求路径。`(.*)` 表示的字符串是 `/bbb/image.pn`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div><br><br><br><div data-tips="true" data-tips-type="tip">重定向路径中出现 <code>//</code>，因此该路径无效。同时，文件扩展名也不正确。</div><br> |
|||`/food$1g` |`/food/bbb/image.png` |正则表达式匹配了请求路径。`(.*)` 表示的字符串是 `/bbb/image.pn`。 |
|`/aaa/bbb/image.png` |`/a{1,2}(.*)g`<br><br>用于匹配请求路径中的特定字符串。 |`/food/$1g` |`/food/a/bbb/image.png` |* 正则表达式匹配了请求路径。<br><br>* `(.*)` 表示的字符串是 `a/bbb/image.pn`。 |
|`/food/aaa/pngs/image.png` ||`/food/$1g` |`/food/a/pngs/image.png` |* 正则表达式匹配了请求路径。<br><br>* `(.*)` 表示的字符串是 `a/pngs/image.pn`。 |
|`/aaa/bbb/image.png` |`aaa(.*)`<br><br>用于匹配请求路径中的特定字符串。 |`/food/$1g` |`/food//bbb/image.pngg` |* 正则表达式匹配了请求路径中的 `aaa/bbb/image.png`。<br><br>* `(.*)` 表示的字符串是 `/bbb/image.png`。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div><br><br><br><div data-tips="true" data-tips-type="tip">重定向路径中出现 <code>//</code>，因此该路径无效。同时，文件扩展名也不正确。</div><br> |
|`/aaa/bbb/image.png` |`aaa/(.*)`<br><br>用于匹配请求路径中的特定字符串。 |`/food/$1` |`/food/bbb/image.png` |* 正则表达式匹配了请求路径中的 `aaa/bbb/image.png`。<br><br>* `(.*)` 表示的字符串是 `bbb/image.png`。 |


<span id="url-改写配置示例"></span>
### URL 改写配置示例

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip">推荐您也参考上方的 "路径改写配置示例"，以了解在使用正则表达式匹配路径时的注意事项。</div>



|**请求 URL 中的路径和查询字符串** |**请求 URL（包含组** **`(.*)`**  **）**  |**回源 URL** |**改写后路径** |**说明** |
|---|---|---|---|---|
|`/a/bbb/image.png?param=val1&param2=val2` |`^/a{1,5}/(.*).png?param=(.*)`<br><br>用于匹配符合以下所有条件的请求 URL：<br><br><br>* 以 1 到 5 个 `a` 组成的目录开头的 `.png` 文件。<br><br>* 第一个查询参数是 `param`。 |`/food/$1.png?param5=$2&size=6` |`/food/bbb/image.png?param5=val1&param2=val2&size=6` |第一个 `(.*)` 表示的字符串是 `bbb/image`。第二个 `(.*)` 表示的字符串是 `val1&param2=val2`。 |
