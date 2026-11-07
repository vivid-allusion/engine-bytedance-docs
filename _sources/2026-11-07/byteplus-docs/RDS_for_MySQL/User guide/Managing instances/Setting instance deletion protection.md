---
title: "Setting instance deletion protection"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Setting_instance_deletion_protection"
---

Deletion protection is a feature provided by RDS for MySQL to prevent instances from being accidentally deleted. You can configure this feature both when creating and using an instance. This article describes the steps to configure this feature while using an instance.

<span id="前提条件"></span>
## Required

An instance has been created, and its state is **Running** or **Suspended**. For details, refer to [Create instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id="操作步骤"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

3. Click **Instances** in the left\-side navigation bar.

4. Click the name of the target instance on the Instance list page to go to the Instance information page.

5. On the **Summary** page, you can view the status of deletion protection for the instance. Click **Enable deletion protection** or **Disable deletion protection**, and then click **OK** in the dialog box that appears to enable or disable deletion protection for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When deletion protection is enabled for an instance, a green shield icon is displayed to the right of the instance name in the Instances list.</div>


<span id="相关-api"></span>
## Related API


|API |description |
|---|---|
|[ModifyDBInstanceDeletionProtectionPolicy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Setting_instance_deletion_protection) |Call the ModifyDBInstanceDeletionProtectionPolicy API to configure deletion protection for an instance. |
