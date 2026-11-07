---
title: "Querying metrics"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/explore-metrics"
---

You can quickly query and display metrics by using the Explore feature. This topic describes how to use Explore to query data in a workspace.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A workspace is created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. Click **Explore** in the left navigation bar to go to the Explore page.

4. In the upper\-right corner of the page, configure the **workspace**, **query time range**, and **data refresh method** for metric queries.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b18a4e6ef2ed4127940574878b1b760e.png) </span>

   
   |Parameter |Description |
   |---|---|
   |Workspace |From the Workspace drop\-down list, select a workspace for which you want to query metrics. |
   |Min step |Minimum step size, that is, the minimum time interval between data points returned in a range query. The default setting is auto. You can specify a step size based on the sampling interval. For example, 10s means that the minimum time interval between returned data points is 10 seconds.<br><br>The following units are supported for the minimum step:<br><br><br>* s (second)<br><br>* m (minute)<br><br>* h (hour)<br><br>* d (day)<br><br>* w (week) |
   |Query time range |The default is the **last 30 minutes**.<br><br>After you click the drop\-down list, you can select the metric query time range. |
   |Data refresh method |**Manual refresh** and **automatic refresh** are supported.  <br><br><br>* **Manual refresh**: Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0a5e23a41e13edf9d9477678186f9d5b.png) </span> icon to refresh the data and page.<br><br>* **Automatic refresh**: The system will automatically refresh metrics and previews according to the refresh interval. |
   

5. Specify the metric that you want to query. You can manually enter a metric or select a metric from the metric list. Metric queries are based on Prometheus Query Language (PromQL) statements. For more information about PromQL, see [PromQL basics](https://docs.byteplus.com/en/docs/vmp/Basic-PromQL-methods?lang=en).

   * **Manual metric input**: If you are familiar with PromQL statements for queries, you can enter a query statement in the field. When you enter the statement, the system will automatically suggest related statements for you to choose from.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4b9b1d89816a5bb85931662814064298.png) </span>

   * **Metric search list**: Click **Metric search** to display the metric search list. You can select the metric that you want to search from the metric list or use the **search** feature to filter the metric.

      * Click a metric name in the **metric list** to select the metric.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cd41dd1da6d68bb0897585bf0caa08e0.png) </span>

      * In the **Filter labels & values** section, filter the metric based on its **label** and **values** for more granular filtering.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_932878dfeb6990c0e9e7dd14c9a4edba.png) </span>

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Click <strong>Add label & values</strong> to add multiple metric labels and corresponding values.         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Click <strong>Reset</strong> to reset the filter conditions.         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">You can filter metric labels by metric name. You can also filter metric names by metric label.         </div>
         

      * Click **Apply** to combine the selected **metric name** and **label\-value pair** into a PromQL metric query statement.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_40d84c90b25e0da369a38f1eb7816a9d.png) </span>

6. After the configuration is complete, click **Query** to query data and get a metric preview. Data can be presented in time series diagrams and tables. You can select a unit as needed.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3aca02029ce735fda9e66d95239e444a.png) </span>


&nbsp;
