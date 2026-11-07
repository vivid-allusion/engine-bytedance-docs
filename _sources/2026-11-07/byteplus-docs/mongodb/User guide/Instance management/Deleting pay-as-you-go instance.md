---
title: "Deleting pay-as-you-go instance"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/delete-instance"
---

Document Database for MongoDB supports manually deleting Pay\-as\-you\-go instances. This topic describes how to manually delete MongoDB instances.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* The instance billing method is **Pay\-as\-you\-go**.

* The instance status must be **Running**, **Unavailable**, or **Closed**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).


<span id=".6K6h6LS56K-05piO"></span>
## Billing instruction

Billing for Pay\-as\-you\-go MongoDB instances stops immediately upon deletion. For more information about the Pay\-as\-you\-go billing method, refer to [Pay-as-you-go](https://docs.byteplus.com/en/docs/mongodb/pay-as-you-go).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, find the target instance, and in the **Actions** column on the right, select  **... \> Delete instance**.

5. In the pop\-up dialog box, confirm the instance information (such as instance ID and name) to be deleted, and set the following parameters.

   
   |Option |Description |
   |---|---|
   |Backup policy |The default backup policy is **Create a final backup**, and no selection is required.<br><br><div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div><br><br><br><br>* <div data-tips="true" data-tips-type="danger">When an instance is deleted, the system automatically initiates a backup to save all data before deletion. You can view backup details of deleted instances on the <strong>Backups of deleted instances</strong> page.</div><br><br><br>* <div data-tips="true" data-tips-type="danger">The retention period for backups of deleted instances is 7 days by default. If necessary, we recommend you promptly restore data to a new instance using backups of deleted instances. For specific procedure, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/recovery_from_a_deleted_instance">Recovery from deleted instance</a>. Otherwise, after the instance is forcefully deleted and the retention period for backups of deleted instances expires, all nodes and all data will be permanently cleared and unrecoverable.</div><br> |
   |Confirm deletion |Enter the name of the target instance for confirmation. |
   

6. Click **Delete**.


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[DeleteDBInstance](https://docs.byteplus.com/en/docs/mongodb/deletedbinstance) |Call the DeleteDBInstance API to delete a specified MongoDB instance. |
