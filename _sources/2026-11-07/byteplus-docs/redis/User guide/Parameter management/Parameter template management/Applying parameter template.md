---
title: "Applying parameter template"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/apply-parameter-template"
---

This topic describes how to apply parameter templates to the target instance.

## Prerequisite

* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

* A parameter template has been created. For specific procedures, refer to [Creating parameter template](https://docs.byteplus.com/en/docs/redis/create-parameter-template).

## Precautions

* The database version of the target instance should be consistent with the parameter template database version to be applied. For example, if the parameter template supports Redis database version 6.0, then the parameter template only supports instances applied for Redis version 6.0.

* If the parameter template to be applied includes parameters that require restarting, the instance will restart after the parameter template is applied. Restarting the instance typically takes 30 to 60 seconds, and one or two temporary disconnections may occur during this process. Please proceed with caution. We recommend that you perform restarts during off\-peak hours and ensure that applications have an automatic reconnection mechanism.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Parameters** tab.

5. On the **Parameter** tab, click **Apply parameter template**.

6. In the pop\-up dialog box, select the template to be applied from the **Select template** drop\-down list.

   > **tip**

   * > The database version of the target instance should be consistent with the parameter template database version to be applied. For example, if the parameter template supports Redis database version 6.0, then the parameter template only supports instances applied for Redis version 6.0.

   * > After selecting a parameter template, a parameter value comparison list will appear. Please confirm the details of the parameters to be modified in the list, including the parameter name, the parameter values before and after modification, and whether a restart is required for the changes to take effect.

   * > If the parameter template to be applied includes parameters that require restarting, the instance will restart after the parameter template is applied. Restarting the instance typically takes 30 to 60 seconds, and one or two temporary disconnections may occur during this process. Please proceed with caution. We recommend that you perform restarts during off\-peak hours and ensure that applications have an automatic reconnection mechanism.

7. Click **OK**.

## Subsequent operations

After the parameter template is successfully applied, you can view the modification records of the modified parameters in the parameter template application under the **Parameter modification history** tab, including the name of the modified parameters, the values before and after modification, the parameter modification status, and the modification time. For specific procedures, refer to [Viewing parameter modification history](https://docs.byteplus.com/en/docs/redis/view-parameter-modification-history).
