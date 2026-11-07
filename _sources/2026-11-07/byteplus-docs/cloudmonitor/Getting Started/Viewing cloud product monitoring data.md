---
title: "Viewing cloud product monitoring data"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-Cloud-Service-Monitor"
---

The Cloud Service Monitor page displays the metrics of various cloud products in a centralized manner. The Cloud Service Monitor page displays the statistics on the status, performance, and alert overview of all instances of each product in different regions, and enables you to quickly create alert policies. This helps you monitor instances and promptly obtain information about exceptions that occur on instances.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

<span id=".5bey5pSv5oyB55qE5LqR5Lqn5ZOB"></span>
### Supported cloud products

Currently, multiple cloud products, such as ECS, VKE, and EIP are supported. For a detailed list, see [Cloud product metrics](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics).

<span id=".5LqR55uR5o6n55qE55uR5o6n5oyH5qCH"></span>
### Cloud Monitor metrics

The metrics vary based on different cloud products. For details, see the metrics displayed on each monitoring page. For example:


* For ECS, the displayed metrics include CPU utilization, memory utilization, and other metrics.

* For EIP, the displayed metrics include inbound bandwidth, outbound bandwidth, and other metrics.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For all metrics of different cloud products, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics">Cloud product metrics</a>.</div>


<span id=".5p-l55yL5LqR5Lqn5ZOB55uR5o6n5pWw5o2u"></span>
## Viewing cloud product monitoring data


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation tree, click **Cloud Service Monitor**. On the page that appears, select the target cloud product.

3. In the top navigation bar, select the target region.

4. View the alert overview, resource distribution, and instance list of the corresponding cloud product in the selected region within the current account.

   * **Alert overview**

      * **Number of current alerts**: the total number of resource instances with **active alerts** and the number of resource instances at different alert levels, which include **Critical, Warning, and Notice**. If you click the number of instances at a specific level, you are redirected to the **Alert history** page, where instances at the specific level will be automatically displayed in the list. For details, see [Viewing alert records](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-alarm-history).

      * **Number of alert policies**: the total number of alert policies associated with resource instances and the number of alert policies in different states, which include **Disabled and In alert**. If you click the number of alert policies in a specific status, you are redirected to the **Alert policy** page, where policies in the specific status will be automatically displayed in the list. For details, see [Viewing alert policies](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-an-alarm-strategy).

   * **Distribution of resources**

      * This section only displays the key metrics for each cloud product. The distribution of resource instances across different performance tiers is displayed in chart form.

   * **Resource instance list**

      * Displays the basic information of all resource instances, such as the name, status, and performance.

      * Click the name of the target resource instance to view all metric data and associated alert policies.

         Cloud Monitor collects data every 30 seconds by default. However, the obtained data will be aggregated and displayed by different intervals and methods based on the selected query time range. The following table describes specific rules.

      
      |**Query time range** |**Monitoring data aggregation interval** |**Descriptions** |
      |---|---|---|
      |(0, 6] hours |30 seconds |Cloud Monitor obtains data every 30 seconds and directly displays the collected data. |
      |(6, 24] hours |1 minute |Cloud Monitor collects data every 30 seconds, aggregates data that is collected every two collection cycles by using a specific aggregation method (such as calculating the average value of the data), and then displays the data. |
      |(1, 7] days |5 minutes |Cloud Monitor collects data every 30 seconds, aggregates data that is collected every 10 collection cycles by using a specific aggregation method (such as calculating the average value of the data), and then displays the data. |
      |(7, 15] days |60 minutes |Cloud Monitor collects data every 30 seconds, aggregates every 120 data points by using a specific aggregation method (such as calculating the average value of the data), and then displays the data. |
      

5. (Optional) Click the name of the current product to directly select another product or perform a fuzzy search to switch between cloud products.


<span id=".5Yib5bu65ZGK6K2m562W55Wl"></span>
## Creating an alert policy


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation tree, click **Cloud Service Monitor**. On the page that appears, select the target cloud product.

3. In the top navigation bar, select the target region.

4. In the upper right corner of the page, click **Create alert policy**.

5. Specify the parameters of the policy. The current cloud product and region are automatically selected for the alert object.

   For detailed configuration, see [Creating alert policies](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy).
