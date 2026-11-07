---
title: "Metric management"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Metric_management"
---

Metric management is a visual metric search page provided by Observability Platform. It allows you to quickly search metrics by product, time, metric type, attribute category, and more.​ This topic describes how to quickly find metrics and view their details.

<span id="qubPY5gO"></span>
## Limits

The following products currently support metric management: Server\-side Monitoring.

<span id="3E42nVvz"></span>
## Procedure


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, select **Metric center \-\> Metric management**.

3. Filter metrics based on your needs. The list of filtered metrics is displayed after you apply the filters.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Multiple filters follow "AND" logic, meaning only metrics that meet all filters are displayed.   </div>
   

   
   |Serial number |Filter item |Description |
   |---|---|---|
   |1 |Product scope |Filter metrics by product and region.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Supported regions vary by product. Refer to the console for the actual supported regions.</div><br> |
   |2 |Time range |Filter metrics that have data points reported within the specified time range, using relative time or custom time. |
   |3 |Fuzzy search |Perform a fuzzy search for metrics by metric name. |
   |4 |Quick filter |Quickly filter metrics by various attributes attached to the metric, such as metric type, attribute category, and source.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Two attribute categories are supported: default metrics and custom metrics, classified by the following rules.</div><br><br><br><br>* <div data-tips="true" data-tips-type="default"><strong>Default metrics</strong>: Metrics reported by language probes, metrics reported by basic resources such as hosts and containers, and automatically generated trace performance metrics are all classified as default metrics.</div><br><br><br>* <div data-tips="true" data-tips-type="default"><strong>Custom metrics</strong>: Raw metrics reported via SDK and metrics generated through <a href="https://docs.volcengine.com/docs/6431/2122010">production metrics</a> are all classified as custom metrics.</div><br> |
   

4. Click **View** in the "Actions" column to the right of the target metric to view its details and tag information.

   * **Metric ** **details**: Detailed information about the metric, including metric type, attribute category, associated product, source, unit, and description.

   * **Tag**: Tags attached to the metric. You can perform a fuzzy search by tag `VALUE`.
