---
title: "View the instance list"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/View_the_instance_list"
---

The instance list in Milvus for VectorDB provides details such as instance name, instance ID, status, availability zone, version, and creation time. This topic describes how to view the instance list and the related operations.

## Procedure

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. in the top menu bar, select the project and region for the instance.

   > **tip**

   > If the instance is not configured with a project, select **All resources**.

3. Click **Instances** in the left navigation pane, select the **Dedicated**, **Serverless**, or **On\-Demand** tab to view the instance list of the specified type.

## What's next

* **Export instances**

   You can export and save the data of the specified instance locally.

   1. In the instance list, click the![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_06364c20b80af45b8393591e049b0e62.png)icon.

   2. In the Export Instances dialog, configure the following parameters, then click **OK**.

      |Parameter |Description |
      |---|---|
      |Export scope |Select the scope of instances to export. Valid values:<br><br><br>* **Export all data**: Export data for all instances under the current account.<br><br>* **Export selected data**: Export data for selected instances.<br><br>* **Export current search results**: Export data filtered by instance name or ID. |
      |Header language |Select the language for exporting instance data field names. Valid values are **English** and **Chinese**. |
      |Export list fields |Select fields to export instance data. |

* **Modify the instance name**

   On the instance list, click the edit icon to the right of the target instance name to modify the instance name. The instance name must meet the following rules:

   * Cannot start with a digit or hyphen (\-).

   * Contain letters, digits, underscores (_), and hyphens (\-).

   * Length must be between 1 and 128 characters.

* **Copy the instance ID**

   On the instance list, click the copy icon to the right of the target instance ID to copy the instance ID.

* **View instance details**

   On the instance list, click the Name of the target instance to enter the **Instance details** page and view the instance information. For more information shown on the instance details page, see [View instance details](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/View_instance_information).

* **View instance monitoring information**

   On the instance list, click the monitoring icon in the **Monitor** column of the target instance. For more information about instance monitoring items, see [Monitoring and alarm metrics](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Monitoring_and_alarm_metrics).

   > **tip**

   > Viewing instance monitoring information is not supported for On\-Demand instances.

* **Delete an instance**

   **Dedicated instance**

In the Instances list, select  **...**  in the **Actions** column of the target instance  **\> Delete**, then click **OK** in the pop\-up dialog to delete the instance. For more information, see [Delete an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Delete_an_instance).

   **Serverless instance**

In the instance list, click **Delete** in the **Actions** column of the target instance, then click **OK** in the pop\-up dialog to delete the instance. For more information, see [Delete an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Delete_an_instance).

   **On-Demand instance**

In the instance list, click **Delete** in the **Actions** column of the target instance, then click **OK** in the pop\-up dialog to delete the instance. For more information, see [Delete an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Delete_an_instance).

   > **tip**

   > If delete protection is enabled for an instance, you cannot delete the instance from the instance list before you disable delete protection for the instance. For more information about delete protection, see [Configure delete protection for an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Configure_delete_protection_for_an_instance).
