---
title: "Query logs"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Query_logs"
---

Logstash provides log query functionality. When a Logstash instance encounters an exception and you need to identify the cause, you can select filters such as node, log level, log type, start and end time, and keywords to quickly locate the logs of the instance you want to query, assisting in Logstash instance operations and maintenance. By default, Logstash instance logs within the past 7 days are provided and displayed in reverse chronological order. This topic describes how to query logs.

<span id="faOlPaXf"></span>
## Procedure


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the left navigation, select **Data processing** \> **Logstash**.

3. In the Logstash instance list, click the target instance name to enter the **Basic information** tab.

4. On the left, select **Observability** \> **Logs**.

5. On the log query page, select nodes, log levels, log types, start and end times, keywords, and other filter criteria as needed. The system will automatically filter logs that meet the criteria and display them in the log list below.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can click <strong>Log time</strong> in the log list to switch between ascending and descending order of logs.   </div>
