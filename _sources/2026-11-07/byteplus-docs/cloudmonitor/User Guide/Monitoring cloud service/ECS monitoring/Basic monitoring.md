---
title: "Basic monitoring"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Basic-monitoring"
---

To view the basic metric data of an Elastic Compute Service (ECS) instance, you need to go to the details page of the ECS instance. The ECS instance monitoring page only displays the performance data of ECS instances.

<span id=".5p-l55yL5Z-656GA55uR5o6n"></span>
## View basic metric data


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview).

2. In the left navigation bar, click **Cloud Service Monitor**. On the page that appears, click **ECS**.

3. In the top navigation bar, select the target region.

4. View the alert overview and resource distribution of ECS instances in the selected region within the current account.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f2c0ca11cb9648273e880c05362fd5a8.png) </span>

   
   |No. |Section |Descriptions |
   |---|---|---|
   |① |Alert overview |Displays the alert overview information in the specified region within the current account, including:<br><br><br>* **Number of current alerts**: the total number of resource instances in the Alert state and the number of resource instances at different alert levels, which include Critical, Warning, and Notice.<br><br>   If you click the number of instances at a specific level, you are redirected to the **Alert History** page, where instances at the specific level will be automatically displayed in the list. You can view the detailed information about the instances. For more details, refer to [Viewing alert records](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-alarm-history).<br><br>* **Number of alert policies**: the total number of alert strategies associated with resource instances and the number of alert strategies in different states, which include **Disabled and In alert**.<br><br>   If you click the number of alert policies in a specific state, you are redirected to the **Alert policy** page, where policies in the specific state will be automatically displayed in the list. You can view the detailed information about the policies. |
   |② |Distribution of resources |Displays the performance metric trend charts of ECS instances that are integrated with Cloud Monitor. |
   |③ |Resource instance list |Displays the names, status, and related metric values of ECS instances. |
   |④ |Export data |Allows you to export current data to an Excel file and download the file to your on\-premises computer. |
   

5. Click the name of the target instance in the resource list to go to the monitoring details page. Click the **BaseMonitor** tab to view the basic metric data of the specified instance.

   
   |No. |Section |Descriptions |
   |---|---|---|
   |1 |Monitoring time range |You can view monitoring data within the last day by default. You can also specify a custom query time range, which is accurate to minutes.<br><br><br>* You can query data in the last 30 days at most. The metric storage duration varies based on different cloud services. For more details, refer to [Cloud service metrics](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics).<br><br>* The query time range can be up to 15 days each time. |
   |2 |Chart linkage |After you select Chart linkage, you can quickly view the metrics and values at the same time point of all charts. |
   |3 |Cycle and Method |The data collection interval and method in the chart.<br><br><br>* **Cycle**: The interval at which the data is collected in the chart. The intervals slightly vary based on the selected monitoring time range. Valid values: **30s**, **1m**, **5m**, **10m**, **30m**, and **1h**. When the monitoring time range is greater than 7 days, the interval is fixed at **10m**.<br><br>* **Method**: The method in which the statistics are collected in the chart. Valid values: **Default value**, **Average**, **Maximum value**, **Minimum value**, and **Sum value**. |
