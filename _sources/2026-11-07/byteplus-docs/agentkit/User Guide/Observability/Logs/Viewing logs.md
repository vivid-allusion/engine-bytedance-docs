---
title: "Viewing logs"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Viewing_logs"
---

You can view logs, that is, the runtime logs of each resource, to analyze log information and quickly locate anomalies.

In this topic, an agent runtime is used as an example to describe how to view logs. To view logs for other resources, such as tools or MCP services, select the target resource in the left\-side navigation pane in the product console.

<span id="DllTkCGg"></span>
## Procedure


1. Log in to [the AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Agent Runtime".

3. In the agent runtime list, click the name of the target agent runtime to enter the details page.

4. Select the "Log" tab. On the search and analysis page for the log topic, specify a time range.

   The default time range is 5 minutes. You can also specify a custom time range. Log data that falls outside the specified query time range will not be included in query results.

5. Enter the search condition and click the "Search" button.

   * For supported search methods, see [Search overview](https://docs.byteplus.com/en/docs/tls/Query-overview-2). For supported search syntax, see [Search syntax](https://docs.byteplus.com/en/docs/tls/Log-query-syntax-2).

   * To search logs without performing a statistical analysis, simply enter your search condition.

   * If the search condition is empty, the system retrieves all logs within the specified time range.

6. After searching, you can view the results on the "Raw log" tab.

   Log data is reported about every 1 minute. If no real\-time data appears on the "Raw log" tab, wait for one minute and refresh the page. For more information, see the [View search results](https://docs.byteplus.com/en/docs/tls/Query-logs-2?lang=en) section.

7. (Optional) Click the "Download log" button on the right to download logs to your local device.
