---
title: "Unsubscribing from yearly or monthly subscription instance"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/unsubscribe-instance"
---

Document Database for MongoDB supports unsubscribe instances via the MongoDB console and billing center. This topic describes how to manually unsubscribe MongoDB instances.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* The instance billing method is **yearly or monthly subscription**.

* The instance status must be **Running**, **Unavailable**, or **Closed**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).


<span id="lIrTdzjr"></span>
## Billing instruction

After unsubscribing from yearly or monthly subscription MongoDB instances, the refund is returned to the account balance. For details on refund calculation rules, refer to [Unsubscription management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management#iv-unsubscription-procedure).

<span id="LXZtZYM6"></span>
## Precautions


* When you unsubscribe from a yearly or monthly subscription instance, the instance backup retention policy cannot be selected, and the system automatically initiates a backup to save all data before deletion. You can view backup details of deleted instances on the **Backups of deleted instances** page.

* The retention period for backups of deleted instances is 7 days by default. If necessary, we recommend you promptly restore data to a new instance using backups of deleted instances. For specific procedure, refer to [Recovery from deleted instance](https://docs.byteplus.com/en/docs/mongodb/recovery_from_a_deleted_instance). Otherwise, after the instance is forcefully unsubscribed and the retention period for backups of unsubscribed instances expires, all nodes and all data will be permanently cleared and unrecoverable.

* When managing subscription MongoDB instances with IAM user, the following points need to be noted:

   * If an IAM user needs to perform operations such as recharging, renewing, or unsubscribing for MongoDB instance, it is necessary to add the `BillingCenterFullAccess` permission to the IAM user within the **global** scope. For specific procedure to add permissions for IAM users, refer to [Managing user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-user-management).

   * If you convert the billing method of a pay\-as\-you\-go MongoDB instance to monthly or yearly subscription, even if the IAM user has the `BillingCenterFullAccess` permission for the instance under the corresponding project, you still need to add the `BillingCenterFullAccess` permission for the IAM user at the **global** scope. Otherwise, the IAM user will receive a permission insufficiency error when recharging, renewing, or unsubscribing from the instance. For specific procedure to add permissions for IAM users, refer to [Managing user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-user-management).

   For more information, refer to [Using MongoDB with IAM user](https://docs.byteplus.com/en/docs/mongodb/using_mongodb_services_with_subusers).


<span id=".6K6h6LS56K-05piO"></span>
## Unsubscribe instance via MongoDB console


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. Based on your actual business needs, choose to unsubscribe from a single instance or multiple instances in batches.

   
   |Unsubscription method |Procedure |
   |---|---|
   |**Unsubscribe single instance** |On the target instance type list page, locate the target instance, and in the **Actions** column on the right, select  **... \> Unsubscribe instance**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only subscription instances with <strong>Running</strong>, <strong>Unavailable</strong>, or <strong>Closed</strong> can be unsubscribed. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/instance-status">Instance status</a>.</div><br> |
   |**Unsubscribe instances in batchs** |On the target instance type list page, select the instances to unsubscribe, then at the bottom of the list, select  **... \> Unsubscribe instance**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only subscription instances with <strong>Running</strong> status can be selected for batch unsubscription. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/instance-status">Instance status</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can select up to 100 subscription instances for batch unsubscription at a time.</div><br> |
   

5. In the pop\-up dialog box, confirm the warning message, then click **OK** to proceed to the billing platform.

6. On the **Unsubscription** page, confirm information concerning the instance that you want to unsubscribe (such as product, configuration, instance ID, instance name and start and end time) and amount information (such as the amount actually paid, used amount and refundable amount), and click **Confirm unsubscription**.

   <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="1">danger   </div>
   

   * <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">Clicking <strong>Confirm unsubscription</strong> will immediately apply for unsubscription (the instance will enter the <strong>Deleting</strong> status), and there will be no secondary confirmation pop\-up. Please operate with caution.   </div>
   

   * <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">After clicking <strong>Confirm unsubscription</strong>, an <strong>Unsubscription details</strong> dialog will automatically pop up. You can view the relevant information of the unsubscribed instance (such as instance ID/name and refund amount) in the pop\-up window. You can also click the order number (starting with <strong>Order</strong>) to go to the order details page.   </div>
   


<span id=".6YCa6L-H6LS555So5Lit5b-D6YCA6K6i5a6e5L6L"></span>
## Unsubscribing instance via Billing center

You can unsubscribe subscription MongoDB instances in batches or individually through the billing center. For specific procedures, refer to [Unsubscription management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management#iv-unsubscription-procedure).
