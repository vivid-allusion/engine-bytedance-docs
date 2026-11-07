---
title: "AI 流量管理"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ai-crawler-traffic-monitoring_zh-cn"
---

当您想了解 AI Crawler 是否正在访问您的域名、产生了多少请求、消耗了多少 CDN 响应流量时，可以使用 **AI Crawler 流量监控**。该功能以 AI Crawler 流量监控为主，同时统计常见搜索引擎爬虫，帮助您判断爬虫对网站内容和 CDN 资源的访问情况。

查看 AI Crawler 流量的操作步骤如下：


1. 进入 AI Crawler 流量详情页。

2. 选择项目、域名、时间范围、时间粒度和时区。

3. 查看爬虫请求总数、爬虫请求占比、成功请求数和失败请求数。

4. 在请求数统计和爬虫流量统计图中，按爬虫名称、类别或状态码查看趋势。

5. 结合支持统计的爬虫列表，确认哪些爬虫被纳入统计。


CDN 基于请求中的 User\-Agent 头部识别 AI Crawler 和常见搜索引擎爬虫。页面展示近实时统计数据。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">监控数据的延迟最长约为 5 分钟。</div>


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260730114529-911553832750.png) </span>

<span id="统计范围"></span>
## 统计范围

AI Crawler 通常指用于训练 AI 模型、构建知识库或驱动 AI 应用的自动化访问程序。搜索引擎爬虫指用于抓取和索引网页内容的传统搜索引擎程序，例如 Googlebot。

该页面以 AI Crawler 流量统计为主，同时统计常见搜索引擎爬虫。您可以在趋势图中按爬虫名称、类别或状态码查看数据。

<span id="查看详情页"></span>
## 查看详情页

在 [AI Crawler 流量监控介绍页](https://console.byteplus.com/cdn/cdn-bp/ai-crawl-management)，点击 **开始探索**，进入 **AI Crawler 流量详情** 页面。进入详情页后，您可以先查看总览数据，再通过筛选条件缩小查询范围。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf997bace9e14480814179d52f3a9dc7~tplv-goo7wpa0wc-topic.webp) </span>

<span id="筛选数据"></span>
## 筛选数据

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260730112751-1363240935729.png) </span>

在查看数据前，先确认筛选条件是否符合您的分析目标。页面顶部支持按项目、域名、时间范围、时间粒度和时区筛选数据。


|筛选项 |说明 |
|---|---|
|项目 |默认是 `default`。域名归属于项目，一个域名只能属于一个项目。 |
|域名 |默认展示当前项目下所有域名的数据。手动选择域名时，最多可选择 50 个。 |
|时间范围 |支持快捷选择 **过去 24 小时**、**过去 7 天**、**过去 30 天**，也支持指定任意时间段，精确到秒。 |
|时间粒度 |决定趋势图中每个数据点的时间间隔。可选项与时间范围有关。 |
|时区 |影响数据聚合边界和总览数据。例如时间粒度为 1 天时，时区会影响自然日的统计边界。 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">时区不会影响时间范围选择器中展示的时间，也不会影响趋势图横轴展示的时间。</div>


<span id="时间范围和时间粒度"></span>
### 时间范围和时间粒度

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260730113132-1154319407918.png) </span>

如果您只想排查近期异常，可以选择 **过去 24 小时** 或 **过去 7 天**。如果您需要观察一段较长时间内的趋势，可以自定义时间范围。

可选时间范围最长为 31 天。


|时间范围 |可选时间粒度 |
|---|---|
|不超过 1 小时 |1 分钟、5 分钟 |
|大于 1 小时且不超过 24 小时 |5 分钟、1 小时 |
|大于 1 天且不超过 31 天 |1 小时、1 天 |


<span id="查看总览数据"></span>
## 查看总览数据

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260730112613-901797249007.png) </span>

设置筛选条件后，先查看总览区域。总览数据可以帮助您快速判断当前范围内的爬虫访问规模、爬虫请求占比，以及源站响应情况。


|指标 |说明 |
|---|---|
|爬虫请求总数 |当前筛选条件下，识别到的爬虫请求总数。 |
|爬虫请求占比 |爬虫请求数占当前筛选条件下所有 CDN 请求数的比例。 |
|成功请求数 |源站响应状态码为 2xx 或 3xx 的爬虫请求数。 |
|失败请求数 |源站响应状态码为 4xx 或 5xx 的爬虫请求数。 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">成功请求数和失败请求数仅统计源站响应状态码为 2xx 到 5xx 的请求。因此，成功请求数与失败请求数之和可能小于爬虫请求总数。</div>


如果爬虫请求占比较高，您可以继续查看趋势图，定位请求量集中的时间段、爬虫名称或状态码类别。

<span id="查看趋势图"></span>
## 查看趋势图

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260730112526-951565527110.png) </span>

总览数据用于判断整体情况，趋势图用于查看数据在不同时间点的变化。页面提供两个趋势图：


|图表 |说明 |
|---|---|
|请求数统计 |展示爬虫请求数随时间变化的趋势。 |
|爬虫流量统计 |展示 CDN 响应爬虫请求而产生的响应流量趋势。 |


您可以通过图例或筛选列表控制图表中展示的数据。图例支持点击隐藏或显示对应数据。


|维度 |展示方式 |
|---|---|
|爬虫名称 |支持点击图例，也支持在下拉列表中勾选。列表按当前筛选条件下的请求数从高到低排序，最多选择 5 个。 |
|类别 |支持点击图例。类别包括 AI Crawler 和 Search Engine。 |
|状态码 |支持点击图例，也支持在下拉列表中勾选。状态码按 2xx、3xx、4xx、5xx 展示。 |


<span id="图表展示方式"></span>
### 图表展示方式

趋势图可以按柱形图或曲线图展示。数据点较少时，柱形图更容易比较单个时间点的数据；数据点较多时，曲线图更适合观察整体变化。

您可以设置柱形数量阈值：当柱形数量大于设置值时，图表展示为曲线图。

<span id="支持统计的爬虫"></span>
## 支持统计的爬虫

如果您需要确认某个访问来源是否会被统计，可以查看以下列表。表格中的类别用于趋势图的类别筛选。


|爬虫名称 |类别 |
|---|---|
|PerplexityBot |AI Crawler |
|Perplexity\-User |AI Crawler |
|panguBOT |AI Crawler |
|PetalBot |AI Crawler |
|Diffbot |AI Crawler |
|GPTbot |AI Crawler |
|OAI\-SearchBot |AI Crawler |
|ChatGPT\-User |AI Crawler |
|Meta\-externalagent |AI Crawler |
|Meta\-ExternalFetcher |AI Crawler |
|Facebot |AI Crawler |
|CCBot |AI Crawler |
|cohere\-ai |AI Crawler |
|anthropic\-ai |AI Crawler |
|ClaudeBot |AI Crawler |
|Claude\-User |AI Crawler |
|Claude\-SearchBot |AI Crawler |
|Claude\-Web |AI Crawler |
|Google\-Extended |AI Crawler |
|Google\-NotebookLM |AI Crawler |
|DuckDuckBot |AI Crawler |
|Bytespider |AI Crawler |
|TikTok Spider |AI Crawler |
|ToutiaoSpider |AI Crawler |
|HuaweiCrawler |Search Engine |
|omgili |Search Engine |
|facebookexternalhit |Search Engine |
|FacebookBot |Search Engine |
|facebookcatalog |Search Engine |
|facebookplatform |Search Engine |
|Googlebot |Search Engine |
|Bingbot |Search Engine |
|Yandexbot |Search Engine |
|Baiduspider |Search Engine |
|Yahoo! Slurp |Search Engine |
|Y!J\-ASR |Search Engine |
|Y!J\-BRZ |Search Engine |
|Bravebot |Search Engine |
|Yeti |Search Engine |
|coccocbot |Search Engine |


<span id="使用限制"></span>
## 使用限制

在使用 AI Crawler 流量监控时，请留意以下限制。它们会影响您能查询的数据范围、图表展示方式和统计结果理解。


|限制项 |说明 |
|---|---|
|识别方式 |CDN 基于请求中的 User\-Agent 头部识别爬虫。 |
|数据延时 |页面展示近实时统计数据，延迟最长约为 5 分钟。 |
|时间范围 |单次查询的时间范围不能超过 31 天，开始时间不能早于当前时间前 92 天。 |
|域名选择 |默认展示当前项目下所有域名的数据。手动选择域名时，最多可选择 50 个。 |
|爬虫名称 |在趋势图中按爬虫名称展示数据时，最多选择 5 个爬虫。 |
