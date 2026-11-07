---
title: "Homepage"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Homepage"
---

The AI Native Database Platform provides a homepage that displays a resource overview for the tenant account. This topic introduces the homepage.

## Overview

The homepage displays a resource overview for the tenant account on the AI Native Database Platform, including workspace overview, resource usage, compute consumption, resource consumption, and global monitoring metrics.

* **Workspace overview**

   On the homepage, workspace statuses are categorized as running, changing, creating, suspended, stopped, and abnormal, with the number of workspaces in six of these categories counted and displayed. The following table describes the running statuses of workspaces for each category.

   |**Category** |**Running status of the workspace** |
   |---|---|
   |Running |Running |
   |Changing |Changing, Network changing |
   |Creating |Creating |
   |Suspended |Suspended |
   |Suspended |Suspended |
   |Abnormal |Creation failed, Abnormal |

   > **tip**

   > Click the count below each category to quickly open the workspace list corresponding to that running status category.

* **Resource usage**

   The table below shows the indicators included in resource usage.

   |**Metric** |**Tip** |
   |---|---|
   |Compute |Total compute used by all workspaces since the account was created.<br><br>> **tip**<br><br><br>> This compute data represents the cumulative usage time of 1 CU compute.<br> |
   |Storage |Total storage space used by all workspaces under the account in the past minute. |
   |Compute<br><br> |Compute used by all workspaces across different engine types.<br><br>> **tip**<br><br><br>> This compute data represents the cumulative usage time of 1 CU compute.<br> |
   |Storage space |Total storage space used by all workspaces across different engine types. |
   |Branches |Total branches of all workspaces under different engine types. |
   |Branch compute |Total compute used by non\-default branches of all workspaces across different engine types. |

   > **tip**

   > Resource usage information is updated every hour on the hour.

* **Resource consumption**

   The homepage shows the five workspaces consuming the most compute and storage resources.

* **global monitoring metrics**

   The homepage displays real\-time compute monitoring metrics. For more information about monitoring metrics, refer to [Viewing monitoring information](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Viewing_monitoring_information).

   > **tip**

   > You can call the [GetMetricData](https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData)API to query monitoring metrics and alarm information. When calling this API, you need to provide the product Namespace, the SubNamespace of the metrics to be queried, and the MetricName. Global monitoring metrics \- the Namespace consuming total compute is VCM_Sinlar_PostgreSQL. The MetricName and SubNamespace for each metric are shown in the table below.

   |**Name** |**Metricname** |**Description** |**Dimension** |
   |---|---|---|---|
   |Total compute consumption |AccountGlobalCU |Real\-time compute consumption of all workspaces under the account. |Global monitoring |
