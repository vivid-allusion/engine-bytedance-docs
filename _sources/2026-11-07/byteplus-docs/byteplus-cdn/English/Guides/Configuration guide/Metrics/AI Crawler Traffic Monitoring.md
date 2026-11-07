---
title: "AI Crawler Traffic Monitoring"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ai-crawler-traffic-monitoring_en-us"
---

Use **AI Crawler Traffic Monitoring** to check whether AI crawlers are accessing your domain names, how many requests they generate, and how much CDN response traffic they consume. This feature focuses on AI crawler traffic and also tracks common search engine crawlers, helping you understand how crawlers access your website content and CDN resources.

To view AI crawler traffic, follow these steps:


1. Go to the AI Crawler Traffic Details page.

2. Select a project, domain name, time range, time granularity, and time zone.

3. View the total number of crawler requests, the percentage of crawler requests, successful requests, and failed requests.

4. View trends in the request count and crawler traffic charts by crawler name, category, or status code.

5. Check the list of supported crawlers to see which crawlers are included in the statistics.


CDN identifies AI crawlers and common search engine crawlers based on the User\-Agent header in requests. The page displays real\-time statistics.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Monitoring data may have a latency of up to about 5 minutes.</div>


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260902082249-1640819219174.png) </span>

<span id="statistical-scope"></span>
## Statistical scope

AI crawlers are typically automated access programs used to train AI models, build knowledge bases, or power AI applications. Search engine crawlers are traditional search engine programs that crawl and index web content, such as Googlebot.

This page focuses on AI crawler traffic statistics and also includes common search engine crawlers. In trend charts, you can view data by crawler name, category, or status code.

<span id="view-the-details-page"></span>
## View the details page

On the [AI Crawler Traffic Monitoring introduction page](https://console.byteplus.com/cdn/cdn-bp/ai-crawl-management), click **Explore Now** to go to the **AI Crawler Traffic Details** page. After you enter the details page, you can view overview data first, and then narrow the query scope by using filters.

<span id="filter-data"></span>
## Filter data

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260902114154-578969195461.png) </span>

Before viewing data, check whether the filters match your analysis goal. The top of the page supports filtering data by project, domain name, time range, time granularity, and time zone.


|Filter |Description |
|---|---|
|Project |The default project is `default`. Domain names belong to projects, and each domain name can belong to only one project. |
|Domain name |By default, data for all domain names in the current project is displayed. If you manually select domain names, you can select up to 50. |
|Time range |Supports quick selection of **Last 24 hours**, **Last 7 days**, and **Last 30 days**. You can also specify a custom time range accurate to the second. |
|Time granularity |Determines the interval between data points in trend charts. Available options depend on the selected time range. |
|Time zone |Affects data aggregation boundaries and overview data. For example, when the time granularity is 1 day, the time zone affects the statistical boundary of each calendar day. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The time zone does not affect the time displayed in the time range selector or on the horizontal axis of trend charts.</div>


<span id="time-range-and-time-granularity"></span>
### Time range and time granularity

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260902114235-315865186051.png) </span>

If you only need to troubleshoot recent anomalies, select **Last 24 hours** or **Last 7 days**. If you need to observe trends over a longer period, specify a custom time range.

The maximum time range for a single query is 31 days.


|Time range |Available time granularity |
|---|---|
|No more than 1 hour |1 minute, 5 minutes |
|More than 1 hour and no more than 24 hours |5 minutes, 1 hour |
|More than 1 day and no more than 31 days |1 hour, 1 day |


<span id="view-overview-data"></span>
## View overview data

&nbsp;

After setting filters, view the overview section first. Overview data helps you quickly understand the scale of crawler access, the percentage of crawler requests, and origin response results within the selected scope.


|Metric |Description |
|---|---|
|Total crawler requests |The total number of crawler requests identified under the current filters. |
|Crawler request percentage |The percentage of crawler requests among all CDN requests under the current filters. |
|Successful requests |The number of crawler requests for which the origin response status code is 2xx or 3xx. |
|Failed requests |The number of crawler requests for which the origin response status code is 4xx or 5xx. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Successful requests and failed requests count only requests whose origin response status codes are from 2xx to 5xx. Therefore, the sum of successful requests and failed requests may be smaller than the total number of crawler requests.</div>


If the percentage of crawler requests is high, continue to view trend charts to identify the time periods, crawler names, or status code categories where requests are concentrated.

<span id="view-trend-charts"></span>
## View trend charts

&nbsp;

Overview data helps you understand the overall situation, while trend charts show how data changes over time. The page provides the following two trend charts:


|Chart |Description |
|---|---|
|Request count statistics |Shows the trend of crawler requests over time. |
|Crawler traffic statistics |Shows the trend of response traffic generated when CDN responds to crawler requests. |


You can use legends or filter lists to control the data displayed in charts. Click a legend to hide or show the corresponding data.


|Dimension |Display method |
|---|---|
|Crawler name |Supports clicking legends and selecting crawlers from the drop\-down list. The list is sorted by request count under the current filters in descending order. You can select up to 5 crawlers. |
|Category |Supports clicking legends. Categories include AI Crawler and Search Engine. |
|Status code |Supports clicking legends and selecting status codes from the drop\-down list. Status codes are displayed as 2xx, 3xx, 4xx, and 5xx. |


<span id="chart-display-mode"></span>
### Chart display mode

Trend charts can be displayed as bar charts or line charts. When there are only a few data points, bar charts make it easier to compare individual time points. When there are many data points, line charts are better for observing overall trends.

You can set a bar count threshold. If the number of bars is greater than the configured value, the chart is displayed as a line chart.

<span id="supported-crawlers"></span>
## Supported crawlers

If you need to check whether a specific access source is included in the statistics, see the following list. The category in the table is used for category filtering in trend charts.


|Crawler name |Category |
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


<span id="limits"></span>
## Limits

When using AI Crawler Traffic Monitoring, note the following limits. They affect the data range you can query, how charts are displayed, and how statistical results should be interpreted.


|Limit |Description |
|---|---|
|Identification method |CDN identifies crawlers based on the User\-Agent header in requests. |
|Data latency |The page displays real\-time statistics, with a latency of up to about 5 minutes. |
|Time range |The time range of a single query cannot exceed 31 days, and the start time cannot be earlier than 92 days before the current time. |
|Domain name selection |By default, data for all domain names in the current project is displayed. If you manually select domain names, you can select up to 50. |
|Crawler name |When data is displayed by crawler name in trend charts, you can select up to 5 crawlers. |
