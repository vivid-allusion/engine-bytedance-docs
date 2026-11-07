---
title: "Multi-topic log query"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Multi-topic_log_query"
---

After successfully collecting log data and correctly configuring the index, you can view the collected log data in real time in the Log Service console and query log data within a specified time range using query conditions.

This article introduces the operation steps for multi\-topic log query.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Invitation\-only feature; contact your account manager to whitelist based on business needs</div>


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The storage time of log data in Log Service depends on the **log retention time** of the log project; logs that have expired and been deleted cannot be queried.

* Multi\-topic queries occupy the concurrency quota of single\-topic queries.

* Supports selecting log topics across regions, with up to 50 topics added per query.

* Multi\-topic joint log analysis is not supported.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A project and a log topic have been created.

* Log data has been collected via LogCollector or other methods.

* You must enable indexing before searching logs. To enable indexing, refer to [configure index](https://docs.byteplus.com/docs/tls/Configure-indexes-2).


<span id=".5pON5L2c5q2l6aqk"></span>
## Steps


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, select **common functions** \> **query and analysis**.

4. On the **query and analysis** page, click **+** icon.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3250a889e20e461d34d5f27f98f102f0.png) </span>

5. On the **multi\-topic search** tab, select multiple log topics and click **Confirm**.

6. Specify the time range on the log topic query and analysis page.

   The default is the last 5 minutes, supporting custom search time ranges. If the log data's storage time is outside the specified search time range, this data will not be retrieved.

7. Enter search criteria and click **Search**.

   * For supported search methods, refer to [search overview](https://docs.byteplus.com/docs/tls/Query-overview-2). For supported search syntax, refer to [search syntax](https://docs.byteplus.com/docs/tls/Log-query-syntax-2).

   * Leaving the search criteria empty means querying all logs within the specified time range.

   * For details on search results, refer to [viewing search results](https://docs.byteplus.com/docs/tls/Query-logs-2#.5p-l55yL5qOA57Si57uT5p6c).
