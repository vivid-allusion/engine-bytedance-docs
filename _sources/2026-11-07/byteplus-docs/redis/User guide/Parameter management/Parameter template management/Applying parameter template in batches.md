---
title: "Applying parameter template in batches"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/batch-apply-parameter-template"
---

This article describes how to batch apply a target parameter template to multiple instances.

## Prerequisite

* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

* A parameter template has been created. For specific procedures, refer to [Creating parameter template](https://docs.byteplus.com/en/docs/redis/create-parameter-template).

## Precautions

* The database version of the target instance should be consistent with the parameter template database version to be applied. For example, if the parameter template supports Redis database version 6.0, then the parameter template only supports instances applied for Redis version 6.0.

* If the parameter template to be applied includes parameters that require restarting, the instance will restart after the parameter template is applied. Restarting the instance typically takes 30 to 60 seconds, and one or two temporary disconnections may occur during this process. Please proceed with caution. We recommend that you perform restarts during off\-peak hours and ensure that applications have an automatic reconnection mechanism.

* Each parameter template can be applied to up to 20 instances at one time.

## Procedure

You can choose any of the following methods to apply a parameter template.

### Method 1: Batch apply on Instances page

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, select the target instances for batch application of the parameter template.

   > **tip**

   * > Each parameter template can be applied to up to 20 instances at one time.

   * > Only instances with **Running** status and the same version can be selected.

4. In the lower\-left corner of the instance list, select  **... \> Apply parameter template**.

5. Perform the following tasks in the **Batch apply parameter template** panel pop\-up:

   1. Select template.

      Confirm the instance information (such as instance name, ID, and version information) that needs to apply this template in the **Selected instances** area, and select the template to be applied in the **Parameter template** area.

   2. Click **Next step** in the lower\-right corner.

   3. Confirm application.

      In the **Confirm information** area, confirm the parameter information that needs to be modified for this application (such as parameter name, parameter value in the template, whether a restart is required for it to take effect, etc.), as well as the current value of the corresponding parameter in the selected instance.

      > **tip**

      > If the parameter template to be applied includes parameters that require restarting, the instance will restart after the parameter template is applied. Restarting the instance typically takes 30 to 60 seconds, and one or two temporary disconnections may occur during this process. Please proceed with caution. We recommend that you perform restarts during off\-peak hours and ensure that applications have an automatic reconnection mechanism.

   4. Click **OK** in the lower right corner.

      > **tip**

      > After clicking **OK**, the **Batch tasks have been initiated** pop\-up window will appear. You can perform the following tasks in the pop\-up window:

      * > View the detailed information of the parameter template application task, including task progress, total number of tasks, and execution results of individual tasks.

      * > For failed tasks, click **Retry** in the **Actions** column on the right side of the corresponding instance to re\-initiate the parameter template application task for that instance.

      * > Click **Batch retry** in the bottom\-right corner to re\-initiate the parameter template application task for all failed instances.

      * > Click **Terminate** in the bottom\-left corner to stop this batch parameter template application operation. All running or pending tasks will be terminated.

      * > Click **OK** in the lower\-right corner to close the dialog box.

### Method 2: Batch apply on Parameter templates page

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. In the left\-side navigation pane, select **NoSQL Database \> Redis \> Parameter templates**.

4. On the **Parameter templates** page, find the parameter template to be applied according to business needs under the **Customized templates** or **System templates** tab.

5. In the **Actions** column on the right side of the target parameter template, click **Apply to instance**.

6. Perform the following tasks in the **Apply parameter template to instance** panel pop\-up:

   1. Select instance.

      In the **Selected parameter template** area, confirm the template information to be applied (such as template name, ID, applicable version, creation and modification time, etc.), and select the instances to which this template needs to be applied in the **Instances** area below.

      > **tip**

      * > Each parameter template can be applied to up to 20 instances at one time.

      * > Only instances with **Running** status and the same applicable version as the target parameter template can be selected.

   2. Click **Next step** in the lower\-right corner.

   3. Confirm application.

      In the **Confirm information** area, confirm the parameter information that needs to be modified for this application (such as parameter name, parameter value in the template, whether a restart is required for it to take effect, etc.), as well as the current value of the corresponding parameter in the selected instance.

      > **tip**

      > If the parameter template to be applied includes parameters that require restarting, the instance will restart after the parameter template is applied. Restarting the instance typically takes 30 to 60 seconds, and one or two temporary disconnections may occur during this process. Please proceed with caution. We recommend that you perform restarts during off\-peak hours and ensure that applications have an automatic reconnection mechanism.

   4. Click **OK** in the lower right corner.

      > **tip**

      > After clicking **OK**, the **Batch tasks have been initiated** pop\-up window will appear. You can perform the following tasks in the pop\-up window:

      * > View the detailed information of the parameter template application task, including task progress, total number of tasks, and execution results of individual tasks.

      * > **For failed tasks, click**Retry in the **Actions** column on the right side of the corresponding instance to re\-initiate the parameter template application task for that instance.

      * > Click **Batch retry** in the bottom\-right corner to re\-initiate the parameter template application task for all failed instances.

      * > Click **Terminate** in the bottom\-left corner to stop this batch parameter template application operation. All running or pending tasks will be terminated.

      * > Click **OK** in the lower\-right corner to close the dialog box.

## Subsequent operations

After the parameter template is successfully applied, you can view the modification records of the modified parameters in the parameter template application under the **Parameter modification history** tab, including the name of the modified parameters, the values before and after modification, the parameter modification status, and the modification time. For specific procedures, refer to [Viewing parameter modification history](https://docs.byteplus.com/en/docs/redis/view-parameter-modification-history).
