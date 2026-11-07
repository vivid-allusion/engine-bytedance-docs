---
title: "View slow logs"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/View_slow_logs"
---

Slow logs record queries and write requests with execution time exceeding the threshold. They help analyze request duration, identify performance bottlenecks, and provide data for query optimization and capacity planning. Milvus for VectorDB offers slow log query functionality for Dedicated instances and supports delivery to Torch Log Service (TLS) on BytePlus, enabling convenient log search, visualization, and alert monitoring. This topic describes how to view slow logs.

## Prerequisites

* A dedicated instance has been created and is in Running status. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance).

* Torch Log Service (TLS) on BytePlus is enabled. For detailed steps, see [TLS](https://www.byteplus.com/en/product/tls).

## Precautions

* Milvus for VectorDB does not charge for slow log delivery. Torch Log Service TLS charges for slow log storage and traffic. For detailed billing methods, see [Billing overview](https://docs.byteplus.com/en/docs/tls/billable_items).

* Turning on slow log delivery triggers a Proxy rolling restart; perform this during off\-peak hours.

## Procedure

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. in the top menu bar, select the project and region for the instance.

   > **tip**

   > If the instance is not configured with a project, select **All resources**.

3. Click **Instance list** in the left navigation pane.

4. In the **Instance list**, select the **Dedicated** tab, then click the target instance name.

5. Select the **Logs** tab, then the **Slow logs** subtab, and click **Configure**.

6. In the **Enable slow logs** dialog, configure the following parameters and click **OK**.

   |Parameter |Description |
   |---|---|
   |Slow query threshold (seconds) |Set the request time consumed threshold for recording slow logs. Value range: integer not less than 1. |
   |Associated IAM project |Select the associated project from the dropdown list. For details, see [Project overview](https://docs.byteplus.com/en/docs/6649/189152). |
   |TLS Project (optional) |Select the log project of Torch Log Service. For details, see the [Log project](https://docs.byteplus.com/en/docs/tls/Managing_projects). |
   |TLS Topic (optional) |Select the log topic of Torch Log Service. For details, see the [Log topic](https://docs.byteplus.com/en/docs/tls/Managing_topics). |

7. In the popup dialog, click **OK**.

## View slow logs

After enabling slow log delivery, you can view and search slow logs in the **Slow logs** subtab and perform clustering and chart analysis on the logs. For detailed steps, see [Query and analysis workflow](https://docs.byteplus.com/en/docs/tls/Query-and-analysis-process), [Analyze data using log clustering](https://docs.byteplus.com/en/docs/6470/2131418), and [Query and analysis charts](https://docs.byteplus.com/en/docs/tls/Query_and_analysis_chart).

## More operations

You can also edit slow log delivery settings, turn off slow log delivery, and view slow logs in the TLS console on the slow **Logs** tab.
