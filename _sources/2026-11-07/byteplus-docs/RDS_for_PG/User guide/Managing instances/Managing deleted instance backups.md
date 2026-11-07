---
title: "Managing deleted instance backups"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/managing_deleted_instance_backup"
---

When you delete or unsubscribe from a PostgreSQL instance, the system supports creating a final backup for the instance. The backup file is retained for 7 days. Before the retention period expires, you can view the backup file in the **Backups of deleted instances** list, or recover the instance using this backup file. After the retention period expires, the backup file is deleted and cannot be recovered.

<span id=".5p-l55yL5bey5Yig6Zmk5a6e5L6L5aSH5Lu9"></span>
### Viewing deleted instance backups


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click **Backup of deleted instance** in the left\-side navigation bar to open the **Backups of deleted instanc**e page.

   The **Backups of deleted instance** page displays a list of backups for deleted instances. You can view the backup ID, instance name/ID, backup status, backup size, backup type, backup start/end time, instance status, database version, backup retention period, project, and actions of deleted instances.

   * **Backup status** shows the progress of the backup file and can be either Succeeded or a percentage of backup progress.

   * **Instance state** can be Deleted or Released. If the instance uses pay\-as\-you\-go billing, the instance state shows **Deleted** after backup succeeds; if it uses a subscription plan, it will show **Released** after backup succeeds.

   * **Backup retention period** for backups of deleted instances is 7 days. Hover over the backup retention period of the target instance to view the expiration time of the backup file.

   * **Actions** allow restoring the instance from the backup file before the backup expires for deleted instances.


<span id=".5oGi5aSN5bey5Yig6Zmk5a6e5L6L"></span>
### Recovering an deleted instance


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click **Backup of deleted instance** in the left\-side navigation bar to open the **Backups of deleted instanc**e page.

4. In the backup list on the **Backup of deleted instance** page, click **Restore** in the **Actions** column of the target backup file to open the **Data recovery** page.

5. After setting the following parameters for the new instance on the **Data recovery** page, click Confirm order.

   
   |Parameter |Is it required? |Note |
   |---|---|---|
   |Instance name |No |Sets the instance name. The instance name is optional, the default value is <source instance name\> _recovery, and when empty, the instance ID is named. Naming rules are as follows:<br><br><br>* The name length must be 1 to 128 characters.<br><br>* Cannot start with a digit or a hyphen (\-).<br><br>* The name consists of Chinese characters, English letters, digits, underscores (_), and hyphens (\-). |
   |Node specification |Yes |Each specification has a corresponding number of cores, memory, and maximum connections, which you can choose according to your business requirements.<br><br>Note During a recovery, the new instance has the same primary, secondary, and read\-only node specifications and availability zones as the source instance by default, and the same number of read\-only nodes is selected by default. You can reset the node specifications and the number of read\-only nodes according to business needs. When setting node specifications and the number of read\-only nodes, the following requirements must be met:<br><br><br>* The specifications of the secondary and primary nodes must be consistent.<br><br>* The specification of a read\-only node must be greater than or equal to that of the primary node.<br><br>* You can add up to 10 read\-only nodes.<br><br>* Primary, secondary, and read\-only nodes can be deployed in different availability zones in the same region. |
   |Storage space |Yes |Storage space includes data space, log space, WAL log space, and transaction file space. Select a value in the 20–3000 GB range. |
   |Virtual private cloud |Yes |Virtual private cloud, also known as VPC (Virtual Private Cloud), is supported. A VPC is an isolated network environment with higher security and performance than a classic network. You must select a VPC if private network is selected. You can also click Create VPC on the right to create a new VPC. For more information on this operation, refer to [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC). |
   |Subnet |Yes |Choose an available subnet in the selected VPC.<br><br>A subnet is an IP address block within a private network. All cloud resources in a private network must be deployed within the subnet, which is a cloud quota private network IP address. For more details, see [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet). |
   |Project |No |Select the project to which the instance belongs. A project is a virtual concept that includes a set of resources, users, and roles. A project allows you to view and manage a group of resources in a unified manner and control the permissions of users and roles to these resources. For more details, refer to [About Resource Management](https://docs.byteplus.com/en/docs/resourcemanagement/Product_Overview). If the project is not selected, the newly created instance will be assigned to the default project. |
   |Tag |No |Add tag (s) to the instance. Tag are used for the identification and classification of cloud resources.  RDS for PostgreSQL supports adding tag to instances. You can organize PostgreSQL instances by tags to facilitate instance search and resource aggregation. For more information, see [Tag overview](https://docs.byteplus.com/en/docs/RDS_for_PG/overview). If you need to separate accounts by tags, you need to enable tags in [Bill management > Bill tags](https://console.byteplus.com/finance/bill/tag/) to apply corresponding tags to bill details. For more details, see [Tag-based bill splitting for instances](https://docs.byteplus.com/en/docs/RDS_for_PG/tag-based_bill_splitting_for_instances). |
   |Billing method |Yes |RDS for PostgreSQL supports two billing methods: pay\-as\-you\-go and subscription.<br><br><br>* Pay\-as\-you\-go: If you plan to use your PostgreSQL instance for a short period of time, select pay\-as\-you\-go (hourly billing). You can release the instance when it is no longer needed, saving money.<br><br>* Subscription: If you plan to use your PostgreSQL instance for a long time, please select subscription (one\-time payment) and select the purchase duration in the lower left corner of the page. Subscription is more affordable than pay\-as\-you\-go billing, and the longer the purchase time, the more discounts.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can also create a pay\-as\-you\-go instance first, and then subcontract the annual subscription after confirming that the instance meets the requirements. If you choose pay\-as\-you\-go, make sure your BytePlus account balance is at least ￥100. For more information on billing, see <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/price_overview">Billing overview</a>.</div><br> |
   

6. Then click **Confirm order**.

7. Complete the next steps based on the selected billing method.

   1. If you select **Pay\-as\-you\-go**: On the **Confirm order** page, confirm the order details, read and check the **Database Product and Services Terms**, and click **Buy now** to restore to a new instance.

   2. If you select **Subscription**:

      * On the **Confirm order** page, confirm the order details, read and check the **Database Product and Services Terms**, and click **Submit the order**.

      * On the **Confirm order information** page, confirm the order information again and click **Next step**.

      * On the **Submit payment information** page, confirm the payment details and select the payment method, click **Go to pay**, and resume to the new instance after completing the payment according to the prompts.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Return to the instance list page, the new instance state changes to <strong>Creating</strong>, and wait for the backups to complete to use normally.</div>
