---
title: "Instance deletion protection"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Instance_deletion_protection"
---

To avoid instance deletion caused by misoperation, NDB for MySQL supports instance deletion protection. Once this feature is enabled, the instance cannot be deleted. This article describes how to enable and disable instance deletion protection.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

After instance deletion protection is enabled, the instance cannot be deleted. To delete an instance, you need to turn off the feature first. Some deletion scenarios are not restricted by the instance deletion protection feature, as shown in the following table.


|Instance type |Scene description |
|---|---|
|**Subscription** |* After enabling instance deletion protection, you can still cancel your subscription through the billing platform. For how to unsubscribe from yearly/monthly subscription, see [Subscription cancellation](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management).<br><br>* If the instance is shut down due to instance expiration, the instance will be forcibly deleted even if instance deletion protection is enabled. For more information about instance expiration, see [Expiration](https://www.byteplus.com/en/docs/NDB_for_MySQL/Arrears_and_expiration). |
|**Pay\-as\-you\-go** |For pay\-as\-you\-go instances, if the instance is shut down due to arrears in the account, the instance will be forcibly deleted even if deletion protection is enabled. For more information on account arrears, see [Arrears description](https://www.byteplus.com/en/docs/NDB_for_MySQL/Arrears_and_expiration). |


<span id=".5byA5ZCv5a6e5L6L5Yig6Zmk5L-d5oqk"></span>
## Enable instance deletion protection

You can choose any of the following methods to enable the instance deletion protection function:


* **Method 1**

   Enable the deletion protection function when creating an instance. For detailed steps, see [Creating an instance](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

* **Method 2**

   1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

   2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   3. On the **Instances** page, click the name of the target instance.

   4. In the **Basic information** area under the **Summary** page, click **Enable delete protection** after **Deletion protection**.

   5. Click **OK** in the pop\-up dialog box.


<span id=".5YWz6Zet5a6e5L6L5Yig6Zmk5L-d5oqk"></span>
## Disable instance deletion protection


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. In the **Basic information** area under the **Summary** page, click **Disable delete protection** after **Deletion protection**.

5. Click **OK** in the pop\-up dialog box.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyDBInstanceDeletionProtectionPolicy](https://www.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceDeletionProtectionPolicy) |Call the ModifyDBInstanceDeletionProtectionPolicy interface to enable or disable the instance deletion protection function. |
