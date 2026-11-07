---
title: "Viewing monitoring data"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/view-monitoring-data"
---

Cache for Redis adopts a proxy\-server architecture, which supports viewing visualized proxy node and server node performance monitoring data. You can monitor relevant data to keep track of the status of instance operations and promptly detect maintenance\-related issues. This topic describes how to view monitoring data of Redis instances.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click **Monitoring** tab.

5. Under the **Monitoring** tab, you can select different tabs to view the data details of various monitoring metrics within a specified time range (such as the past 1 hour).

   |Tab name |Description |Precautions |
   |---|---|---|
   |Aggregated proxy |Displays the details of various performance monitoring data that support aggregation in the proxy nodes. Among them, the performance monitoring data shown under the **Aggregated proxy** tab is the aggregated value of the corresponding performance monitoring data in all proxy nodes under the current instance. |* You can quickly specify the query time period as **1 hour**, **3 hour**, **6 hour**, **12 hour**, **1 day**, **3 days**, or **7 days** above the monitoring chart, or you can customize the query time period in the query time window.<br><br>* You can also hold down the left mouse button and drag on the line chart of any monitoring metric to quickly select the time period within the range covered by the mouse. The selected query time period will be uniformly applied to all metrics under the current tab.<br><br>* You can view performance metric details for up to the past 15 days.<br><br>* For more information about monitoring metrics, refer to [Monitoring metrics](https://docs.byteplus.com/en/docs/redis/monitoring-metric).<br><br>* In the upper right corner of the **Monitoring** tab, you can click **View more metrics** to jump to the cloud monitoring page, and you can also click **Create an alert policy** to set alarms. For specific procedures, refer to [Setting alerts](https://docs.byteplus.com/en/docs/redis/set-alert). |
   |Aggregated server |Displays the details of various performance monitoring data that support aggregation in the server nodes. Among them, the performance monitoring data shown under the **Aggregated server** tab is the aggregated value of the corresponding performance monitoring data in all server nodes under the current instance. ||
   |Proxy |Under the **Proxy** tab, you can check the target node on the left side to view the details of various performance monitoring data of single proxy node. ||
   |Server |Under the **Server** tab, you can click the target shard on the left side and then check the target node in the shard to view the details of various performance monitoring data of a single server node. ||
   |Top 5 view |Displays the details of the server nodes ranked in the top 5 in terms of monitoring metric data such as peak CPU usage, memory usage, network peak input rate, or network peak output rate among all server nodes of the current instance, including the server node ID and the corresponding monitoring metric values. |* You can quickly specify the query time period as **1 hour**, **3 hour**, **6 hour**, **12 hour**, or **1 day** above the monitoring data ranking table, or you can customize the query time period in the query time window.<br><br>* Only the monitoring metric data of peak CPU usage, memory usage, network peak input rate, or network peak output rate of server nodes will participate in the Top 5 ranking, while the corresponding metric data for proxy nodes will not be ranked.<br><br>* You can view the details of the performance metric data ranking within the past 24 hours at most. |
