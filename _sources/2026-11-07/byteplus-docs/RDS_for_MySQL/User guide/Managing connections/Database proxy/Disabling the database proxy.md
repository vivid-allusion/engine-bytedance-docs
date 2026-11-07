---
title: "Disabling the database proxy"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/disable_database_agent"
---

This topic describes how to disable the database proxy feature.

## Precautions

After you disable the database proxy feature, the read/write splitting policy of the connection endpoint becomes invalid, and the default connection endpoint is disassociated from read\-only nodes.

## Limitation

* You may not be able to disable the database proxy if your instance has not been fully upgraded for more than six months. To disable the database proxy feature, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.

* The database proxy cannot be disabled for multiple node instances.

## Prerequisites

When disabling the database proxy, RDS for MySQL performs a pre\-check on the instance. If the pre\-check is successful, refer to the [Procedure](https://docs.byteplus.com/en/docs/RDS_for_MySQL/disable_database_agent#.5pON5L2c5q2l6aqk) in this article to disable the database proxy. If any check items fail, refer to the following content for solutions.

|Check items |Check result |Solutions |
|---|---|---|
|Instance version |The current instance version does not support enabling or disabling the database proxy |You can troubleshoot and resolve the issue by checking the following two items. If the instance meets the following two conditions but you still cannot enable or disable the database proxy, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000178) to contact technical support for assistance.<br><br>Confirm that the instance is a double\-node instance. You cannot enable or disable the database proxy for non\-double\-node instances.<br><br>Confirm that the allowlist version of the instance is v2. To confirm the allowlist version of the instance, call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancedetail) API and check the returned value of the AllowListVersion field. If the allowlist version is v1, you can call the [UpgradeAllowListVersion](https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgradeallowlistversion1) API to upgrade the allowlist version to v2. |
|Instance state |The database proxy cannot be enabled or disabled because the instance is not in the Running state. |Confirm that the instance state is **Running**. If the instance is not in the **Running** state, check for any ongoing operations. After the operations are complete and the instance returns to the **Running** state, enable or disable the database proxy again. |
||You cannot enable or disable the proxy if there are running network events. |Confirm whether the instance has any running network events. Network events include creating and deleting public network addresses, creating, editing, and deleting endpoints, modifying the prefix or port of a connection address, and modifying the resolution method for a private network address. After the running network events are complete, enable or disable the database proxy again. |
|Allowlist limit |You cannot enable or disable the database proxy because the number of IP addresses in the allowlist exceeds the limit. |Confirm whether the number of IP addresses or IP address segments currently associated with the instance exceeds 290. If the number of currently associated IP addresses or IP address segments exceeds 290, you need to adjust it. To make adjustments, refer to [Modify allowlist](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_an_allowlist) and [Disassociate allowlist](https://docs.byteplus.com/en/docs/RDS_for_MySQL/disassociating_an_allowlist_from_an_instance). |
|Instance configuration |The transaction\-level connection pool is enabled for the current instance and does not support enabling or disabling the proxy |Switch the instance's connection pool mode to direct connection mode. For more details, refer to [Switching connection pool mode](https://docs.byteplus.com/en/docs/RDS_for_MySQL/switching_connection_pool_mode). |
||The current status of the instance's connection endpoint does not support enabling or disabling the database proxy. |Check and adjust the customized connection endpoints of the instance to ensure that each customized read\-only endpoint is associated with only one read\-only node, and the associated read\-only node is only associated with that customized read\-only endpoint and the default endpoint. For details about modifying the nodes associated with a connection endpoint, refer to [Editing connection endpoints](https://docs.byteplus.com/en/docs/RDS_for_MySQL/editing_connection_endpoints); to delete a connection endpoint, refer to [Deleting connection endpoints](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleting_connection_endpoints). |
||Read/Write separation is enabled for the current instance, which does not support enabling or disabling the database proxy. |Check and adjust the instance's connection endpoints to ensure that read/write splitting is disabled for each one. Refer to [Enabling or disabling read/write separation](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_read-write_splitting). |
||The 'Automatically associate new node' feature is enabled for the customized_endpoint of the current instance, which does not support enabling or disabling the database proxy. |Check and adjust the connection endpoints of the instance. Ensure that the **Automatically associate new node** feature is disabled for all connection endpoints except the default connection endpoint. For details about disabling the automatically associate new node feature, refer to [Modify endpoint](https://docs.byteplus.com/en/docs/RDS_for_MySQL/editing_connection_endpoints). |
||The database proxy cannot be enabled or disabled because the current account has customized access accounts. |Check whether the instance has custom access accounts (accounts authorized by host IP addresses). If custom access accounts exist, refer to [Modifying account permissions](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_account_permissions) to remove the host IP addresses set for the accounts, or [delete the accounts](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_and_managing_an_account#.5Yig6Zmk6LSm5Y-3). |
|Others |Unable to enable or disable the database proxy due to backend system restrictions. |[Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000178) to contact technical support for assistance. |

## Procedure

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the project and region for the instance.

   > **tip**

   > If the project of the instance has not been set, the project should be selected as **All resources**.

3. Click **Instances** in the left navigation bar.

4. On the **Instances** page, click the instance name of the target instance to enter the **Instances** page.

5. Click the **Connectivity** tab. In the **Database proxy** section, click the switch to the right of **Database proxy**![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png)icon.

6. In the **Disable database proxy** dialog box, click **OK** to disable the database proxy.

   When disabling the database proxy, RDS for MySQL evaluates the instance state. If the evaluation passes, click **OK** to disable the database proxy feature. If the evaluation fails, the failed check items and check results are displayed in the **Disable database proxy** dialog box. Make the necessary adjustments based on the **solutions** in the [Prerequisites](https://docs.byteplus.com/en/docs/RDS_for_MySQL/disable_database_agent#.5YmN5o-Q5p2h5Lu2), then click Retry to **re\-run** the evaluation. If the evaluation passes, click **OK** to disable the database proxy feature. If it fails, make adjustments based on the listed failed check items and results.

## Related API

|API |Description |
|---|---|
|ModifyDBProxy |Call the ModifyDBProxy API to enable or disable the database proxy feature. |
