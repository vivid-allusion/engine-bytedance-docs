---
title: "Viewing pre-configured dashboards"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/View_preset_dashboard"
---

Products integrated with Cloud Monitor provide pre\-configured dashboards. This topic describes how to view the pre\-configured dashboard of a cloud product and how to configure data in the pre\-configured dashboard.


1. Log in to the [Cloud Monitor](http://console.volcengine.com/cloud-monitor/overview) console. 

2. In the left navigation tree, click **Cloud Service Monitor**. On the page that appears, select the target cloud product.

3. In the top navigation bar, select the target region.

4. In the cloud product instance list, click the name of the target instance to go to the monitoring details page, where you can view the pre\-configured dashboard for the specified instance.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5849f65fafc98dc06313835d25136696.png) </span>

   You can configure and select the data aggregation method and aggregation interval for the data in the pre\-configured dashboard. The following table describes the details.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To ensure the performance of the pre\-configured dashboard, you cannot specify the <strong>aggregation interval</strong> and <strong>aggregation method</strong> if you select a large query time range for monitoring data.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Currently, you can specify the <strong>aggregation interval</strong> and <strong>aggregation method</strong> only if you set the time range to <strong>3 days</strong> or less.   </div>
   

   
   |No. |Section |Descriptions |
   |---|---|---|
   |1 |Monitoring time range |You can view monitoring data within the last day by default. You can also specify a custom query time range, which is accurate to the minute.<br><br><br>* For most products, you can query data from the last 30 days at most by default, which is related to data storage duration. For details, see [Supported cloud products](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics).<br><br>* The query time range can be up to 15 days each time. |
   |2 |Chart linkage |After you select Chart linkage, you can quickly view the metrics and values at the same time point of all charts. |
   |3 |Aggregation interval |Specify the aggregation interval for data in the pre\-configured dashboard.<br><br>The available aggregation intervals slightly vary based on the selected monitoring time range. When the query time range is large, you may be unable to select a smaller aggregation interval. To view results for a smaller aggregation interval, narrow down the selected query time range. |
   ||Aggregation method |Configure the aggregation method for data in the pre\-configured dashboard within the aggregation interval, including:<br><br><br>* **Default value**: The value directly returned by the query expression of the metric.<br><br>* **Average**: The value calculated by averaging the raw values within the statistical period.<br><br>* **Maximum value**: The maximum value among the raw values within the statistical period.<br><br>* **Minimum value**: The minimum value among the raw values within the statistical period.<br><br>* **Sum value**: The sum of the raw values within the statistical period.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The supported aggregation methods may vary based on the pre\-configured dashboards of different products. Refer to the console for details.</div><br> |
