---
title: "Associating allowlist and instance"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Associating_allowlist_and_instance"
---

This article describes how to associate an allowlist with an instance. After the allowlist is associated, only IP addresses in the allowlist can access the instance.

<span id="前提条件"></span>
## Prerequisites


* The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

* (Optional) An allowlist has been created. For details, see [Creating an allowlist](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_allowlist). If no allowlist has been created, you can also temporarily create a new allowlist through the page prompts.


<span id="使用限制"></span>
## Limitation


* A single account in the same region can create up to 100 allowlists, each allowlist can contain up to 300 IP addresses or IP address segments, and each allowlist can bind up to 50 instances.

* A single instance can bind up to 100 allowlists and up to 1000 IP addresses.


<span id="操作步骤"></span>
## Procedure

You can choose any of the following methods to associate an instance with an allowlist:

<span id="方法一：绑定实例至当前白名单"></span>
### Method 1: Associate the instance to the allowlist


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the allowlist.

3. Click **Allowlists** in the left\-side navigation bar.

4. On the **Allowlists** page, click **Associate instance** in the allowlist actions column.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also click on the target allowlist name, and in the pop\-up control panel, in the <strong>List of associated instances</strong> area, click <strong>Associate instance</strong>.   </div>
   

5. In the pop\-up control panel, select the target instance to be associated and click **OK**.


<span id="方法二：绑定白名单至当前实例"></span>
### Method 2: Associate the allowlist to the instance


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click the **Security** tab, and then click **Associate instance**.

5. On the **Associate allowlist** page, select **Existing allowlist** or **New allowlist**.

   * If you select **Existing allowlist**, check the allowlist associated with the current instance in the list.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can filter the target allowlist based on the <strong>project</strong> to which it belongs. The default is all resources.      </div>
      

   * If you select **New allowlist**, configure the parameters according to the page prompts, create a new allowlist, and associate it with the current instance. For how to configure parameters, see [Creating an allowlist](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_allowlist).

6. Click **OK**.


<span id="相关-api"></span>
## Related APIs


|API |Description |
|---|---|
|[AssociateAllowList](https://www.byteplus.com/en/docs/NDB_for_MySQL/AssociateAllowList) |Call the AssociateAllowList to associate the instance to the allowlist. |
