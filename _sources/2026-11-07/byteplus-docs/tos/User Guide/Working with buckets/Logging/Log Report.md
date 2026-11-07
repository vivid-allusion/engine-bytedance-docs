---
title: "Log Report"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Log-report"
---

TOS has preset some log reports for your review. This article describes the built\-in report types and how to view them.

<span id="6d8ae456"></span>
## Log report description

The preset report descriptions in TOS are as follows.


|**Chart Name** |**Description** |
|---|---|
|bucket\-pv |Total effective request count for GetObject in the entire Bucket. |
|bucket\-uv |Total effective request IP count for GetObject in the entire Bucket. |
|mirror\-status |Bucket mirror back\-source status code trend. |
|pv\-uv\-trend |Bucket PV and UV trend changes. |
|get\-put\-trend |Number and trend of effective GET and PUT requests. |
|client\-top\-access |Information about the accessing client, including client IP address, PV, and traffic information. Sort by number of visits from highest to lowest, supporting up to TOP 1000. |
|object\-top\-access |The accessed file information includes the file name, page views, and traffic information. Sort by number of visits from highest to lowest, supporting up to TOP 1000. |
|referer\-top\-access |Visited Refer information, including Referer URL and total Referer count. Sort by number of visits from highest to lowest, supporting up to TOP 1000. |


<span id="1c4a240a"></span>
## **Procedure**


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane, click **Logging**, on the **Logging** page, click the **log report** tab.

4. In the **log report** tab, view the required report.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can select or customize the statistics time in the upper right corner of the page.   </div>
