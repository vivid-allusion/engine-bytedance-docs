---
title: "Viewing monitoring information"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/viewing_monitoring_information"
---

This topic describes how to view monitoring information.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only monitoring information from the past one month can be viewed, and the maximum time range for each query is 15 days.

* RDS for PostgreSQL retrieves data every 30 seconds by default and displays the collected data by averaging or taking the maximum value according to the display granularity of the query results. For example, when querying the QPS data of proxy nodes in the past 3 hours, Cloud Monitor shows results with a 2\-minute granularity, meaning each displayed data point is actually the average of the previous 4 queries. For more information about monitoring metrics, refer to [Monitoring metrics](https://docs.byteplus.com/en/docs/RDS_for_PG/viewing_monitoring_information).

* Based on the selected query time range, the data is aggregated and displayed using different cycles and methods.The specific rules are as shown in the following table.

   
   |**Query time range** |**Monitor data aggregation interval** |**Note** |
   |---|---|---|
   |(0~6] hours |30 seconds |Cloud Monitor retrieves data every 30 seconds and displays the collected data directly. |
   |(6~24] hours |1 minute |Cloud Monitor retrieves data every 30 seconds and displays the data aggregated by a certain method (such as averaging two data points) after every two collections. |
   |(1~7] days |5 minutes |Cloud Monitor acquires data every 30 seconds and displays the data collected every 10 times according to a certain aggregation method (such as finding the average of 10 times of data). |
   |(7~15] days |60 minutes |Cloud Monitor retrieves data every 30 seconds and displays the data aggregated by a certain method (such as averaging 120 data points) after 120 collections. |
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Monitoring data aggregation period The values of the same monitoring item at the same time point slightly differ under different aggregation periods. To view accurate values, select a smaller time range.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL](https://console.byteplus.com/db/rds-pg) console.

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click on the target instance name.

4. Click on the **Monitoring** tab at the top of the page.

5. Click on the **Monitoring** tab to view **Resource monitor**, **Engine monitor**, **Deployment monitor**, and **Proxy monitor** details of the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information about monitoring metrics, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/monitoring_metrics">Monitoring metrics</a>. You can click <strong>View more metrics</strong> on the right side to view <strong>Alarm policy</strong> and <strong>Alarm overview</strong> of the instance.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Resource and engine monitoring information can be viewed by node, and it supports viewing all nodes simultaneously. In the left\-side <strong>resource monitor</strong> or <strong>engine monitor</strong>, select nodes by checking under <strong>select node ID</strong> to view the monitoring information for the respective nodes.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Monitoring data from the last 15 days is supported. You can customize the time range for viewing with precision to the minute. RDS for PostgreSQL also provides quick options for 1 hour, 3 hours, 6 hours, 12 hours, 1 day, 3 days, 7 days, and other time ranges.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">With <strong>Chart linkage</strong> selected, if you hover over a monitoring chart and view the specific value of a metric at a specific time point, the values of other metrics under the same monitoring category at the same time point are displayed in the monitoring charts synchronously.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">No proxy monitor page is provided if read/write splitting is not enabled for the instance.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Click the top right corner of each monitoring item<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aa59a07501f9616178f7eb8d9a126bb0.png" />, you can view the detail information of the monitoring item.   </div>
