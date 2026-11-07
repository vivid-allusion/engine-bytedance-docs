---
title: "Instance deletion protection"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Instance_deletion_protection"
---

To avoid instance deletion caused by misoperation, HBase supports instance deletion protection. When this feature is enabled, the instance cannot be deleted. This article describes how to enable and disable instance deletion protection.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* For pay\-as\-you\-go instances, if the instance is shut down due to arrears in the account, the instance will be forcibly deleted even if deletion protection is enabled. For more information on account arrears, see [Arrears description](https://docs.byteplus.com/en/docs/HBase/Arrears_and_expiration).


<span id=".5byA5ZCv5a6e5L6L5Yig6Zmk5L-d5oqk"></span>
## Enable instance deletion protection

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After instance deletion protection is enabled, the instance cannot be deleted. To delete an instance, you need to turn off the feature first.</div>


You can choose any of the following methods to enable the instance deletion protection function:


* **Method 1**

   Enable the deletion protection function when creating an instance. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/HBase/Creating_an_instance_1).

* **Method 2**

   1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

   2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   3. On the **Instances** page, click the name of the target instance.

   4. In the **Basic information** area under the **Summary** page, click **Enable delete protection** after **Deletion protection**.

   5. In the dialog box that appears, click **OK**.


<span id=".5YWz6Zet5a6e5L6L5Yig6Zmk5L-d5oqk"></span>
## Disable instance deletion protection


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. In the **Basic information** area under the **Summary** page, click **Disable delete protection** after **Deletion protection**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyInstanceDeletionProtectionPolicy](https://docs.byteplus.com/en/docs/HBase/ModifyInstanceDeletionProtectionPolicy) |Call the ModifyinstanceDeletionProtectionPolicy interface to enable or disable the instance deletion protection function. |
