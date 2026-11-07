---
title: "HTML 转 Markdown"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/html-to-md_zh-cn"
---

本文档介绍如何在 BytePlus CDN 中开启 HTML 转 Markdown 特性，使边缘节点能够将 HTML 响应内容转换为 Markdown 格式返回，以更好地服务 AI Agent、爬虫等场景下的内容消费需求。

<span id="3a499196"></span>
## 特性概述

HTML 转 Markdown 是 CDN 提供的一项 AI 流量管理能力。开启后，对于携带 `Accept: text/markdown` 请求头、访问 HTML 资源的请求，CDN 边缘节点会自动将源站返回的 HTML 内容转换为 Markdown 格式并响应返回。

转换在边缘节点完成，无需客户改造源站，即可让 AI Agent 与爬虫直接获取结构化的 Markdown 内容。其价值在于：


* **降低 Token 消耗：** 原始 HTML 包含大量格式排版、脚本、样式等与正文无关的信息，转换为 Markdown 后内容更精简，可减少 AI 处理时的无效 Token 开销。

* **提升内容可用性：** 结构化的 Markdown 更利于大模型在下游任务中的解析与理解，有助于提升网站内容在 AI 搜索场景下被采纳的可能性。

* **降低源站成本：** 无需在源站自行部署 HTML 转换逻辑，在边缘侧即可完成处理。


<span id="6ccd4d4d"></span>
## 转换说明


|项目 |说明 |
|---|---|
|**触发方式** |基于请求头的内容协商触发。仅当请求头携带 `Accept: text/markdown` 时，CDN 才执行转换。 |
|**支持的源内容类型** |源站响应 Content\-Type 为 text/html 的资源。 |
|**转换结果** |Markdown 正文。 |
|**响应头** |转换完成后，CDN 在响应头中返回 `content-type: text/markdown; charset=utf-8`。 |
|**转换逻辑** |当前版本不对源站内容做正文抽取或降噪处理，源站返回什么内容，即对其原样转换为 Markdown。转换结果包含哪些内容，完全由源站返回的 HTML 内容决定。 |
|**缓存说明** |开启本特性后，CDN 始终不会缓存转换后的 Markdown 文件。 |


<span id="78e6c29e"></span>
## 使用限制

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>不建议对面向浏览器访问的客户端渲染（CSR/SPA）页面开启此特性。</strong></div>


<div data-tips="true" data-tips-type="tip">对于客户端渲染（如 React、Vue 等单页应用）的页面，源站返回的 HTML 仅为不含正文的空壳，真正的内容需由浏览器执行 JavaScript 后在客户端动态渲染生成。此类页面开启本特性后，转换流程仍会正常执行（特性本身生效），但存在两个问题：</div>



* <div data-tips="true" data-tips-type="tip">转换得到的 Markdown 内容基本为空（因源站 HTML 中本就不含正文）；</div>


* <div data-tips="true" data-tips-type="tip">转换后的响应为 Markdown 格式，浏览器无法再将其渲染为正常页面。</div>



<div data-tips="true" data-tips-type="tip">因此，本特性更适合源站 HTML 自身即包含完整正文的页面，例如服务端渲染（SSR）、静态站点生成（SSG），以及通过服务端模板渲染（如 PHP、JSP 等）生成完整 HTML 的页面。</div>


其他说明：


* 当前版本不提供转义配置项（如转换程度、内容摘要等）。

* 请求文件的后缀必须为 `.html` 或 `.htm`，其他后缀的文件不会触发 HTML 转 Markdown。

* 转换仅在请求头明确携带 `Accept: text/markdown` 时触发，不影响浏览器访问（浏览器访问仍返回原始 HTML）。


<span id="956a5ccc"></span>
## 操作步骤


1. 打开 **HTML 转 Markdown** 配置页面。操作步骤参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 设置 **状态** 为启用。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8dab09032199464c99a2a9a9d508d75e~tplv-goo7wpa0wc-topic.webp) </span>

<span id="7483eee6"></span>
## 效果验证

配置生效后，可通过携带 `Accept: text/markdown` 请求头的方式访问 HTML 资源，验证返回内容是否为 Markdown 格式。示例命令如下：

```Bash
curl -i -H "Accept: text/markdown" "https://<YOUR-DOMAIN>/example.html"
```


若特性正常生效，响应头中 `content-type` 应为 `text/markdown; charset=utf-8`，响应体为转换后的 Markdown 内容。作为对比，不携带该请求头访问同一 URL 时，应返回原始 HTML。
