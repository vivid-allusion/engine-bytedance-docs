---
title: "Suspend pay-as-you-go instance"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Suspend_pay-as-you-go_instance"
---

You can switch a running pay\-as\-you\-go Dedicated instance to suspend status. During suspension, compute resources stop running while all instance data and network configurations are fully retained, reducing usage costs when the instance is not in use. This article explains how to suspend a pay\-as\-you\-go instance.

## Prerequisites

Pay\-as\-you\-go Dedicated instance created. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance).

## Precautions

* Only instances in **Running** status can be suspended.

* If the instance exists with unfinished tasks or maintenance events, it cannot be suspended and requires waiting until completion before proceeding.

* Instances are inaccessible after suspension. It is recommended to notify the business side in advance to stop read and write requests to avoid errors or data write failures caused by connection interruptions.

* Resource fees stop during suspension; only backup and storage charges apply. Details are available in [Product billing](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Product_billing).

## Procedure

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. in the top menu bar, select the project and region for the instance.

   > **tip**

   > If the instance is not configured with a project, select **All resources**.

3. Click **Instance list** in the left navigation pane.

4. In **Instances**, select the **Dedicated** tab, then click  **... \> Suspend** instance next to the target pay\-as\-you\-go instance.

5. In the suspend instance dialog, confirm the target instance information, check **I acknowledge the rules and limitations and confirm that I want to suspend the instance**, then click **OK**.

## Subsequent operations

If you need to restore an instance, select  **... \> Restore Instance** on the right side of the target instance, and then click **OK** in the dialog box that pops up.
