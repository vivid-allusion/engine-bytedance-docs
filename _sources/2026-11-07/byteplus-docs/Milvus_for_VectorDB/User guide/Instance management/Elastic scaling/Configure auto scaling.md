---
title: "Configure auto scaling"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Configure_auto_scaling"
---

Milvus for VectorDB supports configuring automatic scaling policies for instances. The system automatically expands computing or storage resources when the instance load increases and scales down when resource usage decreases to release idle capacity, ensuring business stability while optimizing resource costs. This topic describes how to configure auto scaling for an instance.

## Prerequisites

A Dedicated instance with the resource model set to CPU has been created. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance).

## Precautions

* Auto scaling cannot be enabled together with scheduled scaling.

* Subscription instances do not support auto scaling; instances with auto scaling enabled cannot switch to subscription and cannot manually change configurations.

* Each expansion or reduction follows the complete order process and generates a separate bill.

* Mix Coordinator resource consumption is low, but frequent scaling may affect cluster stability. Therefore, auto scaling is not supported.

* Auto scaling evaluates based on the overall average load of instances and cannot detect hotspot distribution or single\-node exceptions (such as OOM). Please plan load balancing strategies accordingly.

* Vertical scaling may cause frequent node restarts, affecting cluster stability. Proceed with caution.

* Expansion trigger condition: average CPU usage \> 60% for 10 consecutive minutes, or average memory usage \> 80% for 10 consecutive minutes (meeting either condition).

* Reduction trigger condition: average CPU usage < 30% for 30 consecutive minutes and average memory usage < 50% for 30 consecutive minutes (both conditions must be met).

* Scaling priority: execute horizontal scaling first, then vertical scaling.

* Auto scaling in may reduce cluster performance; enable cautiously.

* To ensure availability, automatic scaling does not support single\-node instances; expand first, then configure.

* The initial node count cannot be set to 1, and the minimum node count for automatic scaling must not be less than 2.

* Different node types have minimum memory specification requirements. Nodes below these specifications cannot be configured:

   * Milvus 2.5: Proxy and Data nodes require memory ≥ 4 GB; Index and Query nodes require memory ≥ 8 GB.

   * Milvus 2.6 and 3.0: Proxy and Streaming nodes require memory ≥ 4 GB; Data and Query nodes require memory ≥ 8 GB.

      > **tip**

      > Milvus 3.0 version instances currently require whitelist access. To use it, [submit a ticket](https://console.byteplus.com/workorder/create/?step=2&SubProductID=P00000255) for approval.</a\>

## Procedure

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. in the top menu bar, select the project and region for the instance.

   > **tip**

   > If the instance is not configured with a project, select **All resources**.

3. Click **Instance list** in the left navigation pane.

4. In the **Instance list**, select the **Dedicated** tab, then click the target instance name.

5. Select the **Elastic scaling** tab, then click **Edit configuration** under the **Auto scaling configuration** sub\-tab.

6. In the **Edit auto scaling configuration** window, set the following parameters, then click **Save** or **Save and enable** as needed.

   |Node |Parameter |Description |
   |---|---|---|
   |* Proxy<br><br>* Data node<br><br>* Index node<br><br>* Query node |Specification range |set the upper and lower limits for node scaling specifications. |
   ||Ccount range |set the upper and lower limits for node scaling quantity. |
   ||Auto scaling in |Select whether to enable auto scaling in. Turned off by default. |

## Subsequent operations

After enabling auto scaling, click the **Scaling events** tab to view the instance's scaling records.
