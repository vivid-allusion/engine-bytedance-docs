---
title: "Restart an instance or component"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/restart-instance-or-component"
---

when the instance encounters an exception, you can restore its running state by restarting it. you can restart the entire Milvus instance or only specific components according to your needs. this article explains how to restart the Milvus instance or components.

## Precautions

* only Dedicated instances support restart.

* During instance restart, some services will be unavailable. It is recommended to perform the restart during off\-peak hours.

## Procedure

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. in the top menu bar, select the project and region for the instance.

   > **tip**

   > If the instance is not configured with a project, select **All resources**.

3. Click **Instance list** in the left navigation pane.

4. In the **Instance list**, select the **Dedicated** tab, then click the target instance name.

   * Restart instance

      1. At the top right of the instance detail page, select  **... \> Restart**.

      2. In the pop\-up dialog, click **OK**.

   * Restart component

      1. In the **Component level** area of the architecture diagram, click **Restart** to restart the component in all availability zones, or hover over the component to restart in a specific availability zone, then click restart.

      2. In the pop\-up dialog, click **OK**.

5. View restart status.

   After restarting the instance or component, refresh the page to check the instance status. During the restart, the instance running state is **Restarting**. If the status changes to **Running**, the instance has restarted successfully.
