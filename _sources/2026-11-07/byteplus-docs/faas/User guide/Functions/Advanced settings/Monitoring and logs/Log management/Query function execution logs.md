---
title: "Query function execution logs"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Query_function_execution_logs"
---

This article explains how to query function execution logs. The function log search box automatically carries the filter condition `function_id: {function_id}`, facilitating the viewing of targeted function execution logs. You can also enter keywords in the log search box or use query syntax to combine keywords for retrieving desired execution logs.

<span id="prerequisites"></span>
## Prerequisites

Log delivery has been enabled. For detailed operations, refer to [Enable log delivery](https://docs.byteplus.com/en/docs/faas/Enable_log_delivery).

<span id="procedures"></span>
## Procedures


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. On the **Function** page, select the target function, click on the function name to enter its details page.

4. Click **Logs** to switch to the **Logs** tab.

5. Enter the query in the log search box, set the query time range on the right side of the box, and click **Search Analysis** on the right to view the operation logs of the function on the **Original Logs** tab. For details on the query syntax, refer to [Log query syntax](https://docs.byteplus.com/en/docs/tls/Log-query-syntax-2).

   Example: The image below shows the operation logs of the version 2 Hello\-World\-Demo function over the past 30 minutes.

6. (Optional) Click **Log Download** on the right to download the logs to your local machine.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more advanced features about querying logs, please refer to the <a href="https://docs.byteplus.com/en/docs/tls/Query-logs-2">Query logs</a> in Torch Log Service.   </div>
