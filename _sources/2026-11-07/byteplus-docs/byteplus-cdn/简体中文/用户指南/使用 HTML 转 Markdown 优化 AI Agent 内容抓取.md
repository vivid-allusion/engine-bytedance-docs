---
title: "使用 HTML 转 Markdown 优化 AI Agent 内容抓取"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/html-md-best-practice_zh_cn"
---

HTML 转 Markdown 是将网页 HTML 内容转换为 Markdown 内容的方式。相比原始 HTML，Markdown 更接近正文阅读结构，通常能保留标题、段落、列表和链接等信息，更适合 AI Agent、AI 搜索爬虫和大模型问答系统读取。

在 CDN 中开启 HTML 转 Markdown 后，转换可以在边缘节点完成：AI 客户端通过请求头获取 Markdown，普通浏览器仍访问原始 HTML。这样既能为 AI 客户端提供更轻量的内容入口，又无需在源站单独开发和维护转换服务。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dae933b9a76443f593f05bea4753fd67~tplv-goo7wpa0wc-image.image) </span>

<span id="1c89793d"></span>
# 使用场景

如果您的站点有大量公开内容页，并且这些页面的源站 HTML 中已经包含完整正文，建议优先试用 HTML 转 Markdown。该能力尤其适合希望提升 AI Agent、AI 搜索爬虫、大模型问答系统读取效率的网站。


* 站点已有大量公开内容页，例如帮助中心、文档站、资讯文章、博客、知识库、商品详情页等。

* 希望普通浏览器访问保持不变，同时为 AI 客户端提供更轻量的 Markdown 内容。

* 不希望在源站侧单独开发和维护 HTML 转 Markdown 服务。


<span id="7d9595c9"></span>
# 使用收益

对已有大量公开内容页的网站，HTML 转 Markdown 的核心价值是：在不影响普通浏览器访问的前提下，让同一批内容更容易被 AI Agent 读取和理解。实际收益取决于网页本身的内容结构，建议通过典型页面对比验证。


|收益 |说明 |
|---|---|
|降低无效内容占用 |Markdown 相比原始 HTML 更精简，可减少非正文内容对 AI 读取的干扰。 |
|减少传输内容体积 |将 HTML 转换为 Markdown 后，响应内容通常会减少与正文无关的页面结构信息，从而降低传输内容体积。例如，某个体积为 5 MB、包含较多导航、样式、脚本等非正文内容的 HTML 页面，转换为 Markdown 后约为 3 MB，体积降幅超过 40%。页面中非正文内容占比越高，转换后的体积收益通常越明显 |
|提升内容可读性 |Markdown 保留标题、段落、列表、链接等结构，更适合 AI Agent、搜索爬虫和大模型问答系统读取。 |
|降低源站改造成本 |转换在 CDN 边缘节点完成，源站无需单独建设一套 HTML 转 Markdown 服务。 |
|不影响普通访问 |普通浏览器请求未携带 Markdown 请求头时，仍返回原始 HTML 页面。 |


<span id="250cf4d6"></span>
# 推荐使用方式

建议先选择 3 到 5 个典型内容型页面开启并验证效果，例如帮助中心文章、文档页、资讯详情页或商品详情页。分别使用普通请求和携带 `Accept: text/markdown` 的请求访问同一 URL，对比普通访问是否正常、Markdown 中是否包含完整标题和正文、列表和链接是否保留。

确认效果符合预期后，再逐步扩展到同类页面。对于打开后才显示正文、内容结构复杂或强依赖交互的页面，建议先评估转换结果，再决定是否扩大使用范围。

<span id="1a474c4d"></span>
# 产品形态

HTML 转 Markdown 是 CDN 域名配置中的一项开关能力。开启后，CDN 根据请求头区分访问方：AI 客户端请求 Markdown 时返回 Markdown；普通浏览器访问时仍返回原始 HTML。

<span id="8ed52ccc"></span>
## 处理方式


1. AI Agent、AI 搜索爬虫等客户端请求页面，并在请求头中声明 `Accept: text/markdown`。

2. CDN 边缘节点接收请求，确认目标域名已开启 HTML 转 Markdown，并判断请求头是否命中转换条件。

3. 命中条件时，CDN 回源获取原始 HTML 页面，并在边缘节点将 HTML 转换为 Markdown。

4. CDN 向客户端返回 Markdown 响应；普通浏览器请求未携带该请求头时，仍返回原始 HTML。



|项目 |说明 |
|---|---|
|触发方式 |仅当请求头携带 `Accept: text/markdown` 时触发转换。 |
|源内容类型 |源站响应的 `Content-Type` 需为 `text/html`。 |
|转换结果 |返回 Markdown 正文。 |
|响应头 |转换成功后，响应头返回 `content-type: text/markdown; charset=utf-8`。 |
|缓存策略 |CDN 不缓存转换后的 Markdown 文件，每次请求实时转换。 |


<span id="f3b7516c"></span>
# 使用限制

使用该能力前，请重点确认以下限制。HTML 转 Markdown 解决的是“让 AI 客户端更方便读取已有 HTML 内容”的问题，不会改变原网页内容本身。


* **触发条件限制：** 仅当请求头携带 `Accept: text/markdown` 时触发转换。普通浏览器请求不携带该请求头时，仍返回原始 HTML。

* **源内容类型限制：** 源站响应的 `Content-Type` 需为 `text/html`。

* **文件后缀限制：** 请求文件的后缀必须为 `.html` 或 `.htm`，其他后缀的文件不会触发 HTML 转 Markdown。

* **适用页面：** 适用于源站 HTML 中已经包含完整正文的页面，例如帮助中心、文档站、资讯文章、博客、知识库、商品详情页等内容型页面。

* **不适用页面：** 如果源站 HTML 只包含页面框架、没有完整正文，不建议开启；客户端渲染（CSR/SPA）页面通常属于这种情况。此类页面通常需要打开后才显示正文，转换出的 Markdown 可能基本为空；浏览器也无法将 Markdown 响应渲染为正常页面。

* **内容处理限制：** 当前能力不做正文抽取、摘要生成或降噪处理。源站返回什么 HTML，CDN 就基于该内容进行格式转换。

* **缓存限制：** CDN 不缓存转换后的 Markdown 文件，每次命中转换条件的请求都会实时转换。

* **质量边界：** 该能力不替代内容质量优化。标题层级、正文结构、链接文本和无关内容仍需在源站侧保持清晰。


<span id="0b5b2b2d"></span>
# 查看配置方式

如需查看完整的控制台配置路径和操作步骤，请参见 [HTML 转 Markdown 配置文档](https://docs.byteplus.com/en/docs/byteplus-cdn/html-to-md_zh-cn)。

在 CDN 控制台进入目标加速域名的配置页面，定位到 HTML 转 Markdown 配置项，开启该能力并提交配置。配置生效后，只有携带 `Accept: text/markdown` 请求头的请求会触发转换；未携带该请求头的普通访问不受影响。
