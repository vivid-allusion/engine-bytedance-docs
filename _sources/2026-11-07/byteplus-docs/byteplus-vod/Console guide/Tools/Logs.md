---
title: "Logs"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-logs"
---

BytePlus VOD provides hourly CDN logs to help you analyze access traffic and user behavior. This guide explains the structure of the log fields and provides step\-by\-step instructions on how to query and download logs from the BytePlus VOD console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Only logs from the past 30 days are available.</div>


* <div data-tips="true" data-tips-type="tip">The log packages may experience a delay of up to 3 hours, and during peak periods, this delay may exceed 12 hours.</div>


* <div data-tips="true" data-tips-type="tip">The log packages are named following the convention <code>{DomainName}_{StartTime}_{EndTime}.gz</code>. For example, a log package named <code>domain_20220111050000_20220111060000.gz</code> contains access logs for the domain from January 11, 2022, 05:00:00 to January 11, 2022, 05:59:59. The logs are packaged on an hourly basis.</div>



<span id="baeb7ba2"></span>
## Log fields

Let's take a look at an example log:

```Plain
[21/Apr/2023:08:50:12 +0800] 103.xx4.72.25 0.0 GET HTTP gc-yzj1.xxx-test.com / HTTP/1.1 403 407 HIT - "-" "Mozilla/5.0 (Windows NT 6.2; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.198 Safari/537.36" "application/octet-stream"
```


Here's what each field represents:


|**Field name** |**Description** |
|---|---|
|Request time |The time when the request reaches the CDN node |
|Client IP address |The IP address of the client making the request |
|Response time |The time it takes for the CDN node to process the request, in seconds |
|HTTP method |The HTTP request method, such as GET or POST |
|HTTP scheme |The request scheme, either http or https |
|Request domain |The acceleration domain name |
|Request URI |The path requested by the user, starting with "/" |
|HTTP protocol identifier |The protocol information of the HTTP request, such as HTTP/1.1 |
|HTTP status code |The response status code, such as 200 or 404 |
|Response bytes |The size of the server response in bytes |
|Cache Hit/Miss |Indicates whether the request was served from the CDN node's cache |
|Request Range parameter |The Range header value in the HTTP request. If not present, it will be filled with "\-". |
|Request Referer |The Referer header value in the HTTP request. If not present, it is filled with "\-". |
|Request User\-Agent |The User\-Agent header value in the HTTP request. If not present, it is filled with "\-". |
|Response Content\-Type |The Content\-Type header value in the HTTP response. If not present, it is filled with "\-". |


<span id="389e70d1"></span>
## Querying and downloading logs

Follow these steps to query and download logs:


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Tools** \> **Logs** on the left navigation bar.

3. Select the desired space name, domain name, and time range for the query, and click the **Query** button.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8102b4a2a174b9c9c0993f0d848afa1~tplv-goo7wpa0wc-image.image) </span>

4. You have two options for downloading log files to your local device:

   * To download a single log file, click the **Download** button in the action column.

   * To download multiple or all log files, select them and click the **Batch download** button at the top of the list.
