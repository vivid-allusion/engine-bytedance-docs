---
title: "View access logs"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/View_access_logs"
---

Milvus for VectorDB provides access log query capabilities for Dedicated instances and supports forwarding logs to Torch Log Service (TLS) of BytePlus, facilitating log search and analysis, visualization, and alert monitoring. This topic explains how to view access logs.

## Prerequisites

* A dedicated instance has been created and is in Running status. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance).

* Torch Log Service (TLS) on BytePlus is enabled. For detailed steps, see [TLS](https://www.byteplus.com/en/product/tls).

* Enabling access log forwarding triggers a Proxy rolling restart. Perform this operation during business off\-peak hours.

## Precautions

* Milvus for VectorDB does not charge for access log delivery. Torch Log Service TLS charges for access log storage and traffic. See [Billing overview](https://docs.byteplus.com/en/docs/tls/billable_items) for detailed billing methods.

* The instance kernel version is too low and does not support custom collection scope; a kernel version upgrade is required. For specific operations, see [Upgrade kernel version](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Upgrade_kernel_version).

## Enable access log delivery

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. Select the project and region of the instance in the top menu bar.

   > **tip**

   > If the instance is not configured with a project, select **All resources**.

3. Click **Instance list** in the left navigation pane.

4. In the **Instance list**, select the **Dedicated** tab, then click the target instance name.

5. Select the **Logs** tab, then the **Access logs** sub\-tab, and click **Configure**.

6. In the **Enable access logs** dialog, set the following parameters, then click **OK**.

   |Parameter |Description |
   |---|---|
   |Sampling rate |Set the collection rate for access logs. Value range: 0–1. |
   |Collection scope |Configure the APIs and fields for access log collection. By default, **base** is selected, which means collecting all APIs. After unchecking **base**, you can manually select the API. |
   |Associated IAM project |Select the associated project from the dropdown list. For details, see [Project overview](https://docs.byteplus.com/en/docs/6649/189152). |
   |TLS Project (optional) |Select the log project of Torch Log Service. For details, see the [Log project](https://docs.byteplus.com/en/docs/tls/Managing_projects). |
   |TLS Topic (optional) |Select the log topic of Torch Log Service. For details, see the [Log topic](https://docs.byteplus.com/en/docs/tls/Managing_topics). |

## View access logs

After enabling access log delivery, you can view and search access logs on the **Access logs** sub\-tab, and perform clustering and chart analysis on the logs. For detailed steps, see [Query and analysis workflow](https://docs.byteplus.com/en/docs/tls/Query-and-analysis-process), [Analyze data using log clustering](https://docs.byteplus.com/en/docs/6470/2131418), and [Query and analysis charts](https://docs.byteplus.com/en/docs/tls/Query_and_analysis_chart).

## More operations

You can also edit access log delivery settings, disable access log delivery, or go to the TLS console to view access logs on the **Access logs** sub\-tab.
