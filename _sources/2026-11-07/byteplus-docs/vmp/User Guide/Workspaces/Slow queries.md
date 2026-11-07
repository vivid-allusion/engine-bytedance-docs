---
title: "Slow queries"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Slow_queries"
---

A slow query refers to a PromQL query statement whose execution duration exceeds the preset threshold (5 seconds). Such queries are usually inefficient, consume a large amount of resources, and may even affect the writing of monitoring data.

You can use the slow query feature to identify high\-risk queries with durations exceeding 5 seconds, optimize PromQL statements to improve query efficiency, and configure blocking policies for fine\-grained management of resource\-intensive queries.

<span id="D43jgQEg"></span>
## Limits


|Limit |Description |
|---|---|
|Time range |You can query slow PromQL query data generated within the last 30 days at most. |
|Display limit |Up to 50 slow PromQL query data entries are displayed for each query. |


<span id="yWbiGu9m"></span>
## Procedure


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the project and region where your business is located.

3. In the left navigation bar, click **VMP \> Workspace**.

4. After you click the name of the target workspace, click **Slow query** in the left navigation bar.

5. Set the data time range and refresh interval (optional): By default, **slow PromQL query data in the last 30 minutes** is displayed, and the refresh interval is **Manual refresh**. You can set the data time range and refresh interval for slow PromQL query data based on your business requirements.

   
   |Serial number |Feature |Description |
   |---|---|---|
   |1 |Time range |The time range of slow PromQL query data. Click the current time range, such as **Last 30 minutes,**  and select the target time range. You can query slow PromQL query data in the last 30 days at most. |
   |2 |Refresh frequency |The refresh interval of slow PromQL query data. You can select manual refresh or automatic refresh at a specified interval.<br><br><br>* Manual refresh (default): Click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f2a9afc1bdac005a726c7baca5a28a42.png) </span>icon to refresh data.<br><br>* Automatic refresh: Click the current refresh interval, such as **Manual refresh**, and select the target automatic refresh interval. Supported automatic refresh intervals include **Refresh every 1 min**, **Refresh every 5 min, Refresh every 15 min, Refresh every 30 min**, and **Refresh every 1 hour.** <br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The configured automatic refresh interval takes effect temporarily. After you exit the current page, the refresh interval automatically reverts to manual refresh.   </div><br>    |
   

6. View slow PromQL query data, including **Slow PromQL Quantity** and **Slow PromQL List.** 

   * **Slow PromQL Quantity**

      * Displays a trend chart of the number of slow PromQL queries within a specified statistical period, such as **the last 30 minutes**.

      * In the trend chart, click the target time point to view the number of slow PromQL queries generated from the previous minute to the time point.

   * **Slow PromQL List**

      * Displays up to 50 recent data entries. By default, the data entries are sorted by **average time**. You can click the **sort by** drop\-down list to change the default sorting method to **maximum time** or **execution time**.

      * You can also perform the following operation on the target data:

         
         |Feature |Description |
         |---|---|
         |Copy PromQL |Click **Copy PromQL** to reuse the query logic of the target data and apply it in other scenarios, such as the PromQL match rules in PromQL blocking policies. |
         |View details |Click **View details** to view the details of the target data. |
         |ban |Click **ban** to configure the PromQL blocking policy to prohibit the target account from using this PromQL query capability. For specific operations, see [Creating PromQL blocking policies](https://docs.byteplus.com/en/docs/vmp/Managing_PromQL_blocking_policies). |
