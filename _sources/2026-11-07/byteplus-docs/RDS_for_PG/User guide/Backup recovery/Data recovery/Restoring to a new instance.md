---
title: "Restoring to a new instance"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/recovery_from_a_backup_set"
---

This topic describes the procedure for restoring data to a new instance by backup set.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance is created and in the **Running** state. For more information about creating an instance, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance).

* The source instance must have at least one physical backup.

* The recovery process does not affect the original instance.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The data information in the restored instance is consistent with the information in the backup file at that time.

* The restored instance contains the account information of the backup file used at that time.

* If TDE encryption is enabled on the original instance, the restored new instance will automatically enable TDE encryption. This setting cannot be disabled, and the new instance will inherit the key configurations of the original one.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL](https://console.byteplus.com/db/rds-pg) console.

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In subsequent steps, only virtual private clouds and subnets under the selected item are supported for the instance.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can adjust the project to which the instance belongs in subsequent steps.   </div>
   

3. On the **Instances** page, click on the target instance name to enter the instance details page.

4. At the top of the page, click the **Backups** tab.

5. On the **Backups** tab, click **Restore to new instance** under the **Data backup** tab.

6. On the **Restore to new instance** page, click **Confirm** order after completing the following configuration.

   
   |Parameter |Required? |Note |
   |---|---|---|
   |Restore method |Yes |You can choose recovery **by backup set** or **by point in time**.<br><br><br>* Select **By backup set**, instances can be restored from a specified backup set, the backup set selection range is determined by the backup retention day.<br><br>* Select **By point in time**, instances can be restored to the specified point in time, and the supported recovery time range is affected by the backup retention policy. |
   |Backup set or recovery time point |Yes |Select a backup set or a point in time to restore based on the backup method you choose.<br><br><br>* If the recovery method is **By backup set**, you need to select the backup set.<br><br>* If the recovery method is **By point in time**, you need to select the time point where the recovery is expected. Select the required backup set from the drop\-down list. |
   |Instance name |No |Set the instance name. The instance name is optional, the default value is `<source instance name> _recovery`, and when empty, the instance ID is named. Naming rules are as follows:<br><br><br>* The length should be between 1 and 128 characters.<br><br>* It cannot start with a digit or hyphen (\-).<br><br>* The name consists of Chinese characters, English letters, digits, underscores (_), and hyphens (\-). |
   |Node specification |Yes |Each specification has corresponding cores, memory, and maximum connections, which you can choose based on your business requirements.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">During restoration, the nodes of the new instance will be configured with the same specifications and availability zones as the primary, standby, and read\-only nodes of the source instance by default. The same number of read\-only nodes as the source instance will also be selected by default. You may reconfigure these settings based on your business requirements. When setting up, the following requirements must be met:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The specifications of the secondary and primary nodes must be consistent.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The specification of a read\-only node must be greater than or equal to that of the primary node.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can add up to 10 read\-only nodes.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Primary, secondary, and read\-only nodes can be deployed in different availability zones within the same region.</div><br> |
   |Storage space |Yes |Select the storage space for the instance. Storage space includes data space, log space, WAL log space, and transaction file space. The storage space ranges from 20 to 12,000 GB. Select reasonably based on business needs.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Different specifications have different storage space value ranges. For detailed information on storage space value ranges, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/product_specifications">Product specifications</a>.</div><br> |
   |Virtual private cloud |Yes |Select the VPC used by the instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Virtual Private Cloud (VPC)</strong>, is an isolated network environment with higher security and performance than traditional classical networks. You can create a new private network by clicking <strong>Create VPC</strong> on the right. For more details, see <a href="https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC">Creating a VPC</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only the virtual private cloud under the project specified in the navigation bar is supported for selection.</div><br> |
   |Subnet |Yes |Select the subnets available to the instance in the VPC.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">A subnet is an IP address block in the VPC. All cloud resources in the VPC must be deployed in subnets, which assign VPC IP addresses to the cloud resources. You can create a new subnet by clicking<strong> Create subnet</strong> on the right. For more details, see <a href="https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet">Creating a subnet</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only subnets in the availability zone where the instance is located can be selected.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Subnet and VPC can be classified into different projects. Confirm that the target subnet and the selected VPC belong to the same project, which can be checked in the <a href="https://console.byteplus.com/iam/resourcemanage/project">Project console</a>.</div><br> |
   |Allowlists |No |Click the allowlist text box to go to the **Associate allowlist** page. Under this page, after checking the allowlist, click **OK** and go back to **Restore to new instance** page. The selected allowlist will be displayed in the allowlist text box.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">On the <strong>Associate allowlist</strong> page, you can also create a new allowlist. For more information about creating an allowlist, see <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/adding_an_ip_address_allowlist">Creating an allowlist</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">An instance can associate up to 100 allowlists.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Click the × after the allowlist to remove the allowlist.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If there is a default allowlist set under the current account, the allowlist will appear in the allowlist text box.</div><br> |
   |Maintenance window |No |Confirm the maintenance window for the instance. To modify, click the edit button to enter the maintenance window, set **Maintainable day** and **Maintenance window**, then click **OK**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">At least one day and up to seven days per week can be set as maintainable days.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The maintenance window can only be set from 00:00 to 05:59 (UTC+08:00).</div><br><br><br>* <div data-tips="true" data-tips-type="default">The minimum duration of the maintenance window is 2 hours and the maximum duration is 6 hours. Cross\-day settings are not allowed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After an instance is created, you can modify the maintenance window of the instance again. For details, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/Configuring_maintenance_window">Configuring maintenance window.</a></div><br> |
   |Data encryption |No<br><br> |If TDE encryption is enabled on the original instance, the restored new instance will automatically enable TDE encryption and inherit the key configurations of the original instance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">TDE encryption cannot be disabled once enabled.</div><br> |
   |Project |No |Select the project to which the instance belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">A project is a virtual concept that includes a set of resources, users, and roles. A project allows you to view and manage a group of resources in a unified manner and control the permissions of users and roles to these resources. For more details, refer to <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Product_Overview">About Resource Management</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you do not select any projects, newly created instances are added to the default project (default).</div><br> |
   |Tag |No |Add tag(s) to the instance. Tags are used for the identification and classification of cloud resources. RDS for PostgreSQL supports adding tags to instances. You can classify PostgreSQL instances by tags to facilitate instance search and resource aggregation. For more information, see [Tag overview](https://docs.byteplus.com/en/docs/RDS_for_PG/overview).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you need to separate accounts by tags, you need to enable tags in <a href="https://console.byteplus.com/finance/bill/tag/">Bill management \> Bill tags</a> to apply corresponding tags to bill details. For more details, see <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/tag-based_bill_splitting_for_instances">Tag\-based bill splitting for instances</a>.</div><br> |
   |Billing method |Yes |RDS for PostgreSQL supports two billing methods: pay\-as\-you\-go and subscription.<br><br><br>* Pay\-as\-you\-go: If you plan to use your PostgreSQL instance for a short period of time, choose pay\-as\-you\-go (hourly rate). You can save money by releasing the instance when you no longer need it.<br><br>* Subscription: If you plan to use your PostgreSQL instance for a long period of time, select Subscription (one\-time payment) and choose the duration of the purchase in the lower left corner of the page. Subscription is more affordable than pay\-as\-you\-go, and the longer you buy, the more discounts you get.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can also create a pay\-as\-you\-go instance first and confirm that the instance meets the requirements before switching to a yearly/monthly subscription. If you choose pay\-as\-you\-go billing, make sure your BytePlus account balance is at least 100 USD. For more information on billing, see <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/price_overview">Billing overview</a>.</div><br> |
   

7. Then click **Confirm order**.

8. Complete the next steps based on the selected billing method.

   * If you select **Pay\-as\-you\-go**: On the **Confirm order** page, confirm the order details. Read and check the **Database Product and Services Terms**, and click **Buy now** to restore to a new instance.

   * If you select **Subscription**:

      1. On the **Confirm order** page, confirm the order details. Read and check the **Database Product and Services Terms**, and click **Submit the order**.

      2. On the **Confirm order information** page, confirm the order information again and click **Next step**.

      3. On the **Submit payment information** page, confirm the payment details and select the payment method. Click **Go to pay**, and restore to the new instance after completing the payment according to the prompts.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Return to the instances page, refresh the current list, the source instance state becomes <strong>Recovering</strong>, and the new instance state becomes <strong>Creating</strong>. Wait for the backup and recovery to complete and then use it normally. When the source instance is in the <strong>Recovering</strong> state, it can not be accessed through the console, but it can be accessed through the command line without affecting the business.</div>


<span id="P7pwMGeT"></span>
## Related APIs


|API |Description |
|---|---|
|[RestoreToNewInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/restoretonewinstance) |Call the RestoreToNewInstance API to restore data to a new instance. |
