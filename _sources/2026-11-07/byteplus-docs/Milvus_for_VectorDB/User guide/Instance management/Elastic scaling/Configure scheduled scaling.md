---
title: "Configure scheduled scaling"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Configure_scheduled_scaling"
---

Milvus for VectorDB supports configuring scheduled scaling policies for instances, allowing users to automatically adjust resource allocation based on preset time windows to match periodic changes in business traffic, ensuring stable performance while improving resource utilization efficiency. This article explains how to configure scheduled scaling for an instance.

## Prerequisites

A Dedicated instance with the resource model set to CPU has been created. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance).

## Precautions

* Auto scaling and scheduled scaling cannot be enabled together.

* Subscription instances do not support enabling auto scaling; instances with auto scaling enabled cannot be changed to subscription.

* Each scaling operation follows the full order process and generates a separate bill.

* The interval between two scheduled scaling tasks must be at least 30 minutes.

* A maximum of 5 scheduled rules are supported.

## Procedure

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. in the top menu bar, select the project and region for the instance.

   > **tip**

   > If the instance is not configured with a project, select **All resources**.

3. Click **Instance list** in the left navigation pane.

4. In the **Instance list**, select the **Dedicated** tab, then click the target instance name.

5. Select the **Elastic scaling** tab, then click **Create scheduled rule** on the **Scheduled scaling settings** sub\-tab.

6. In the **Create scheduled rule** window, configure the following parameters, then click **OK**.

   |Parameter |Description |
   |---|---|
   |Rule name |Set the name of the scheduled rule, such as **Morning rush hour expansion**. |
   |Recurrence cycle |Select the recurrence cycle to execute the scheduled rule.<br><br><br>* Daily: set the time to execute the scheduled rule each day.<br><br>* Weekly: check the days of the week to execute the scheduled rule and set the execution time. |
   |Target configuration |Select the node types to adjust in this scheduled task and set the target node quantity and target specification. Node types not selected will keep the current configuration unchanged. The supported node types for configuration are as follows:<br><br><br>* Proxy<br><br>* Data node<br><br>* Index node (supported only in version 2.5 instances)<br><br>* Streaming node (supported only in version 2.6 and 3.0 instances)<br><br>   > **tip**<br>   <br><br>   > Milvus 3.0 version instances currently require whitelisting. To use this feature, please [submit a ticket](https://console.byteplus.com/workorder/create/?step=2&SubProductID=P00000255) for approval.<br>   <br><br>* Query node |

## Subsequent operations

* After creating a scheduled rule, turn on the **scheduled scaling rule** switch to enable the rule.

* After creating a scheduled rule, you can **Edit** or **Delete** the rule in the **Actions** column of the rule.

* After enabling scheduled scaling, click the **Scaling events** tab to view the instance's scaling records.
