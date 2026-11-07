---
title: "Enabling the database proxy"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/enable_database_agent"
---

This topic describes how to enable the database proxy.

## Billing

Billing for the database proxy feature starts at 00:00:00 (UTC+8) on November 20, 2024. For more information about the billing of the database proxy, refer to [Billing items and prices](https://docs.byteplus.com/en/docs/RDS_for_MySQL/charge_items_and_price).

## Precautions

* For multiple\-node instances, the database proxy is enabled by default when you create the instance and cannot be disabled.

* For double\-node instances, enabling the database proxy automatically switches the connection pool to transaction\-level mode and associates the default endpoint with all nodes except the secondary node.

* The database proxy service only supports the pay\-as\-you\-go billing method, and usage fees are periodically deducted from your account balance. To ensure the stability of your business, the database proxy service will not be suspended due to account arrears. Note that for pay\-as\-you\-go instances, arrears will cause the instance to shut down. Monitor your account balance to avoid business disruptions. For subscription instances, you can continue to use the database proxy service and will continue to be charged even if your account has arrears. Top up your account promptly. If you do not need the database proxy service, you can disable it manually. For more information about how to disable the database proxy, refer to [Disabling the database proxy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/disable_database_agent).

## Limitation

* You may not be able to enable the database proxy if your instance has not been fully upgraded for more than six months. If you need to use the database proxy feature, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.

* Some instances cannot use the database proxy feature due to their kernel version.

## Prerequisites

When you enable the database proxy feature, RDS for MySQL performs a pre\-check on the instance. If the check passes, refer to the [Procedure](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enable_database_agent#.5pON5L2c5q2l6aqk) in this article to enable the database proxy. If a check item fails, refer to the following content for a solution.

|Check items |Check result |Solutions |
|---|---|---|
|Instance version |The current instance version does not support enabling or disabling the database proxy |Check the following two points to resolve the issue. If the instance meets the following two conditions but you still cannot enable or disable the database proxy, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000178) to contact technical support for assistance.<br><br><br>* Confirm that the instance is a double\-node instance. You cannot enable or disable the database proxy for non\-double\-node instances.<br><br>* Confirm that the allowlist version of the instance is v2. To confirm the allowlist version of the instance, call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancedetail) API and check the returned value of the AllowListVersion field. If the allowlist version is v1, you can call the [UpgradeAllowListVersion](https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgradeallowlistversion1) API to upgrade the allowlist version to v2. |
|Instance state |The database proxy cannot be enabled or disabled because the instance is not in the Running state. |Confirm that the instance state is **Running**. If the instance is not in the **Running** state, check for any ongoing operations. After the operations are complete and the instance returns to the **Running** state, enable or disable the database proxy again. |
||Enabling or disabling the database proxy is not supported while network events are running. |Confirm whether the instance has any running network events. Network events include creating and deleting public network addresses, creating, editing, and deleting endpoints, modifying the prefix or port of a connection address, and modifying the resolution method for a private network address. After the running network events are complete, enable or disable the database proxy again. |
|Others |Unable to enable or disable the database proxy due to backend system restrictions. |[Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000178) to contact technical support for assistance. |

## Procedure

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the project and region for the instance.

   > **tip**

   > If the project of the instance has not been set, the project should be selected as **All resources**.

3. Click **Instances** in the left navigation bar.

4. On the **Instances** page, click the instance name of the target instance to enter the **Instances** page.

5. Click the **Connectivity** tab. In the **Database proxy** section, click the switch to the right of **Database proxy**![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png)icon.

6. Complete the evaluation for enabling the database proxy feature.

   > **tip**

   > When you enable the database proxy, RDS for MySQL evaluates the instance status. If the evaluation passes, the **Database proxy** window appears; proceed to step 7. If the evaluation fails, the failed check items and check results are listed in the **Enable database proxy** window. You can make adjustments based on the [solutions](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enable_database_agent#.5YmN5o-Q5p2h5Lu2) listed in the **Prerequisites** section of this topic. Then, click **Retry** in the window to run the evaluation again. If the evaluation is successful, click **OK** to enable the database proxy. If the evaluation fails, make adjustments based on the failed check items and results.

7. In the **Enable database proxy** window, set the number of proxy cores, select whether to convert the default endpoint to a proxy endpoint, select the checkbox to agree to the billing rules, and click **OK**.

   > **tip**

   * > The maximum number of proxy cores is 1024, and the minimum is the greater of 2 or half the number of CPU cores on the primary node. The adjustment increment is 2. The recommended number of proxy cores is the total number of CPUs of all serviceable nodes of the instance \* 0.5 (round up the result). For example, if the primary node has an 8\-core CPU and the instance has a 4\-core CPU read\-only node, since (8+4)\*0.5=6, the recommended number of proxy cores is 6.

   * > If you select **Endpoint conversion**, the default endpoint will be automatically converted to a proxy endpoint when you enable the proxy. Other endpoints will not be converted.

> **tip**

> After the database proxy is enabled, you can go to the **Database proxy** section on the **Connectivity** tab and click View monitoring to quickly check proxy\-related monitoring information. You can view the information by instance or connection endpoint. For more information about monitoring items and viewing monitoring data, refer to [Monitoring metrics](https://docs.byteplus.com/en/docs/RDS_for_MySQL/monitoring_metrics) and [Viewing monitoring information](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_monitoring_information). If the instance version is too low, "No data" may be displayed when you view proxy monitoring by endpoint. [Submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support to upgrade the instance.

## Related API

|API |Description |
|---|---|
|ModifyDBProxy |Call the ModifyDBProxy API to enable or disable the database proxy feature. |
