---
title: "View instance monitoring information"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/View_instance_monitoring_information"
---

This topic describes how to view monitoring information of a Milvus for VectorDB instance.

<span id="IiYTJz6w"></span>
## Precautions

Only Dedicated and Serverless instances support viewing instance monitoring information.

<span id="8yoSinIi"></span>
## Monitoring information description

The monitoring capabilities of Milvus for VectorDB are provided by Cloud Monitor. Cloud Monitor collects data every 30 seconds by default and aggregates the data based on the selected time range when viewing monitoring data. The aggregation follows the rules shown in the table below.


|**Query time range** |**Monitoring data aggregation period** |
|---|---|
|(0~6] hours |30 seconds |
|(6~24] hours |1 minute |
|(1~7] days |10 minutes |
|(7~14] days |60 minutes |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The aggregation periods of monitoring data vary with different time ranges. At different aggregation periods, the values of the same monitoring metric at the same time point may slightly differ. To view precise values, select a smaller time range.</div>


<span id="0bdraKo2"></span>
## View monitoring information about a single instanceinformation


1. Log in to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. On the top navigation bar, select the target project and region.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the instance is not configured with a project, select <strong>All resources</strong>.   </div>
   

3. Click **Instance list** in the left navigation pane.

4. In the **Instances** list, select the **Dedicated** or **Serverless** tab as needed, then click the target instance name.

5. At the top of the page, click the **Monitoring overview** tab.

   Under the **Monitoring overview** tab, you can view the instance’s monitoring information for Performance, Data, Resource, and Collections.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Performance and Data metrics display by instance, Resource metrics display by node, and Collection metrics display by collection.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For detailed information about monitoring metrics, see <a href="https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Monitoring_and_alarm_metrics">Monitoring and alarm metrics</a>.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">By default, monitoring information of the last day is displayed. You can view the monitoring data of the last month. You can use the time window on the page to define a custom time range for viewing, accurate to the minute, with a maximum interval of 14 days. Milvus for VectorDB also provides quick options of 1 hour, 3 hours, 6 hours, 12 hours, 1 day, 3 days, and 7 days.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Monitoring metrics support display by node dimension. You can click the node name to show or hide the node's monitoring data.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you check <strong>chart linkage</strong>, when hovering over any monitoring chart to view the specific value of that item at a certain time, the exact values of other items under the current monitoring category at that time will also display synchronously in their corresponding charts.   </div>
   


<span id="XxxDHfMF"></span>
## View instance monitoring dashboard information

Milvus for VectorDB is connected to the Cloud Monitor dashboard, allowing you to view all instance monitoring information under the current account directly in the [Monitoring Dashboard](https://console.byteplus.com/observe/cloud-monitor/previewDashBoard/detail?namespace=VCM_Milvus&subnamespace=default).
