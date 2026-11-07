---
title: "Log download"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-logs"
---

To analyze traffic patterns or troubleshoot access issues, you can download hourly CDN access logs for your domain names. This guide provides instructions on how to download logs for a specific timeframe within the past 62 days, explains the log file format, and details each field within the logs.

For differences between "Log Download" and the other two methods for retrieving CDN logs, see [Logs Overview](https://docs.byteplus.com/en/docs/byteplus-cdn/logs-overview_en-us).

<span id="instructions-for-downloading-logs"></span>
## Instructions for Downloading Logs


* Data Timeliness: By default, CDN packages logs collected in the past hour at an hourly granularity, generating log packages at the top of each hour. Log packages are available for download approximately 3 hours after generation. Due to factors such as network latency, logs collected by CDN may have a delay of up to 24 hours. For these delayed logs, CDN appends them to their corresponding log packages. Therefore, log packages may have logs appended within 24 hours after their generation.

* Naming Format for Log Packages: `<domain_name>_<log start time>_<log end time>_<service region>.gz`. The timezone of `<log start time>` and `<log end time>` is UTC+08:00.For example: `www.example.com_20220111050000_20220111060000_outsideChineseMainland.gz`. This log package contains the access logs for the domain `www.example.com` during the time period of [05:00:00, 06:00:00) on 2022/01/11.

* Time Zone: The time recorded in the logs corresponds to the UTC+08:00 time zone.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If your domain name has not been accessed during the specified time period, the query result will be empty.</div>


<span id="explanation-of-log-fields"></span>
## Explanation of Log Fields

An example log entry is as follows:


* `[20/Feb/2022:23:00:00 +0800] 192.0.2.1 2.932 GET HTTPS www.test.com /f/202201/10/a/5b6c70f6da8d1e0bae3e1a21eb02d5b3 HTTP/1.1 200 3610495 HIT - "-" "Dalvik/2.1.0 (Linux; U; Android 5.1.1; TAS-AN00 Build/LMY47I)" "application/vnd.android.package-archive"`


The following table explains each field in a log entry.


|**Field Number** |**Field Name** |**Field Explanation** |
|---|---|---|
|1 |Request Time |Indicates the timestamp when the CDN received the user request. |
|2 |Client IP |Indicates the client IP address from which the user request was initiated. |
|3 |Response Time |Indicates the time, in seconds, for the CDN to respond to the user request. The response time is calculated from the moment the CDN receives the request to when the CDN sends the complete response to the user. |
|4 |HTTP Method |Indicates the HTTP method used for the user request, e.g., `GET`, `POST`. |
|5 |HTTP Scheme |Indicates the scheme used for the user request, e.g., `HTTP`, `HTTPS`. |
|6 |Requested Domain |Indicates the domain name being requested. |
|7 |Request Path |Indicates the requested path, starting with a slash (/). |
|8 |HTTP Protocol Identifier |Indicates the version of the HTTP protocol used for the request, e.g., `HTTP/1.1`. |
|9 |HTTP Status Code |Indicates the status code with which the CDN responded to the request, e.g., `200`, `404`. |
|10 |Response Byte Count |Indicates the size of the CDN response payload in bytes. |
|11 |Cache Hit/Miss |Indicates whether the user request hit the CDN's cache. |
|12 |Request Range Parameter |Indicates the value of the Range header in the user request. The default is "\-", indicating the header does not exist or is empty. |
|13 |Request Referer |Indicates the value of the Referer header in the user request. The default is "\-", indicating the header does not exist or is empty. |
|14 |Request User\-Agent |Indicates the value of the User\-Agent header in the user request. The default is "\-", indicating the header does not exist or is empty. |
|15 |Response Content\-Type |Indicates the value of the Content\-Type header in the CDN response. The default is "\-", indicating the header does not exist or is empty. |


<span id="steps"></span>
## Steps


1. Log in to the [BytePlus CDN Management Console](https://console.byteplus.com/cdn).

2. In the left\-hand navigation bar, click **Tool Center** \> **Logs**.

3. Click the **Log Download** tab.

4. On the **Log Download** tab, specify the time period and domain name for the query, and then click **Query**.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_742e8b8453859de41ae0820d891e9c81.png) </span>
