---
title: "Use LiveTail to stream logs in real time"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Use_the_LiveTail_feature_to_scroll_through_logs_in_real_time"
---

The LiveTail feature of the log service is mainly used in online operation and maintenance scenarios. It supports real\-time log stream display and highlights key information, helping operation staff quickly identify anomalies and improve efficiency. This article introduces the basic features and operation of LiveTail.

<span id="863a3be5"></span>
## Prerequisites


* Logs have been collected.

   Only logs collected by LogCollector version 1.0.6 and later support LiveTail. Logs uploaded through other methods, such as calling the PutLogs interface via SDK, do not support contextual queries. For operation steps, please refer to [collect text logs](https://docs.byteplus.com/docs/tls/single_line_full_text_mode) and [write logs using Go SDK](https://docs.byteplus.com/docs/tls/use_tls_sdk_for_go_to_write_logs).

* Indexes have been configured for the logs. For operation steps, please refer to [configure indexes](https://docs.byteplus.com/docs/tls/Configure-indexes-2).


<span id="6b77eb13"></span>
## Background information

In operation and maintenance scenarios, real\-time monitoring of log queues and extracting key information for quick anomaly analysis is a critical task. Traditional operation and maintenance methods usually require executing the `tail -f` command on the server to monitor log files in real time. For further filtering, the `grep` or `grep -v` commands are used for keyword filtering, which is cumbersome and inefficient. To simplify this process, the log service provides the LiveTail feature. LiveTail primarily includes the following functions:


* Supports real\-time capture and display of the latest content in log files to help you quickly locate anomalies.

* Supports setting keywords to filter logs, showing only the logs you care about.

* Supports monitoring related log files by tracing individual logs without logging into the server.


<span id="8357e6b8"></span>
## Limits

The LiveTail log list supports displaying up to 1,000 logs within the scrollable range. Once reaching the 1,000 logs limit, the system automatically refreshes the list and fills in new logs.

<span id="45b44fe2"></span>
## Steps


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, select **Common Features** \> **Query and Analysis**.

4. On the **Query and Analysis** page, choose the specified project and log topic from the left list.

5. On the query and analysis page for the specified log topic, enter a query statement and set the time range.

6. On the **Raw Logs** tab, find the specified log and click the **LiveTail** icon.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3b98110677d93df1954ba9af3f3ddea8.png) </span>

7. View the results in the **LiveTail** panel.

   After enabling LiveTail, the system automatically identifies logs belonging to the same log file as the specified logs and displays them in real\-time as a log stream in the list. Each newly written log is promptly appended to the bottom of the list. The scrollbar stays at the bottom by default to help you track log updates quickly.

   You can also perform the following actions.

   * Highlight: enter one or more strings in the **highlight** text box to highlight them in the logs.

   * Filter string: enter one or more strings in the **filter string** text box to show only logs containing those strings in the list.

   * Stop LiveTail: click the pause button to stop log analysis when you no longer need to use LiveTail.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_93287ee3eacfbf8e134e8e7b2d418ef8.png) </span>


&nbsp;
