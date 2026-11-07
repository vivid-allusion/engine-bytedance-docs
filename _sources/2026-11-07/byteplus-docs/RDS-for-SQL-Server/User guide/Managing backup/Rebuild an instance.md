---
title: "Rebuild an instance"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/rebuilding-instance"
---

SQL Server supports rebuilding deleted instances from backups within the backup retention period. This topic describes how to rebuild an instance from the deleted backup list.

<span id="Nmb58hXh"></span>
## Description

For instances deleted under the following circumstances, their last full backup is moved to Backups of deleted instances and retained for 7 days:


* Manually deleted instances.

* Subscription instances with more than 7 days until expiration.

* Pay\-as\-you\-go instances that have been overdue for more than 170 hours.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Backups of deleted instances cannot be deleted and are automatically released if the instance is not rebuilt within 7 days.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper\-left corner of the top menu bar, select the target project and region.

3. In the left navigation pane, select **SQL Server** \> **Backups**.

4. On the **Backups** page, click **Backup of deleted instance**.

5. On the **Backup of deleted instance** tab, click **Rebuild instance** in the **Actions** column for the target instance.

6. On the **Rebuild instance** page, set the following instance parameters.

   
   |**Category** |**Parameter** |**Description** |
   |---|---|---|
   |**Restore configuration** |**Restore method** |Currently, only **by backup set** is supported. |
   ||**Backup set** |The default selection is the last backup set that is retained when the instance is deleted. |
   ||**Restore to** |You can only restore to a **new instance**. |
   |**Basic information** |**Instance name** |(Optional) Set an instance name. The naming rules are as follows:<br><br><br>* Can not start with digits or hyphen (\-).<br><br>* Can only contain Chinese characters, letters, digits, underscores (_) and hyphens(\-).<br><br>* The length must be between 1 and 128 characters.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not enter an instance name, it will be the same as the instance ID.</div><br> |
   ||**Compatible versions** |The compatible version of the instance is displayed by default. |
   |**Specification configuration** |**Instance type** |The instance type is displayed by default. |
   ||**Specification family** |Optional: Select the **Include previous generations** radio button to choose a specification type that includes previous generations in the **Specification type** section.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When the selected <strong>Compatible version</strong> is later than SQL Server 2022 , the 1ie specification family of <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/master-instance-specification?lang=zh#Jwh2eKoh">historical generation specifications</a> is not supported.</div><br> |
   ||**Specification type** |The specification type is **Exclusive Type** by default. If you click the **Include previous generation specifications** radio button above:<br><br><br>* When the **Compatible version** is later than SQL Server 2022, the **Specification type** only supports **Exclusive Type.** <br><br>* When the **Compatible version** is SQL Server 2022 or earlier, the **Specification type** supports    . **Exclusive Type II**, **General Type II.**  The details are as follows:<br><br>   * **Exclusive Type II**: Exclusive type instance performance is better and more stable, suitable for business scenarios with database as the core system, such as finance, e\-commerce, government affairs, large and medium\-sized Internet business.<br><br>   * **General Type II**: General type instance is suitable for scenarios with high requirements for cost efficiency and budget optimization.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information about each specification type, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/product-specification-family">Product specification family</a>.</div><br> |
   ||**Node specification** |Configure the node specifications and availability zones for the instance's primary and secondary nodes as needed. The details are as follows:<br><br><br>* **Node specification**: Select the node specification from the drop\-down list for the primary and secondary nodes. The secondary node uses the same specification as the primary node.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more details about node specifications, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/master-instance-specification?lang=en">Primary instance specifications</a>.   </div><br>   <br><br>* **Availability zones**: Select the availability zone for the node from the drop\-down list. The availability zone is the geographic location of the node. If an instance has primary and secondary nodes, you can deploy them across different availability zones.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Select an availability zone close to your target users to improve access speed.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The availability zone can not be modified after the instance is created successfully.   </div><br>    |
   ||**Storage Type** |Currently, only **Extremely\-Fast SSD PL1 Cloud Disk** is supported. |
   ||**Storage space** |Storage space includes data file space and temporary file space. The storage space of the new instance must be greater than or equal to that of the original instance. Enter a storage space between 20 GiB and 4000 GiB in 10 GiB increments. Select a value based on your business needs. |
   |**Network configuration** |**VPC** |Select the target VPC from the drop\-down list. You can also click Create VPC on the right to create a new VPC. For detailed instructions, see [Create a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">A VPC (Virtual Private Cloud) is an isolated network environment that offers higher security and better performance than a traditional classic network.</div><br> |
   ||**Subnet** |The subnets vary depending on the availability zones selected for the primary and secondary nodes, as follows:<br><br><br>* If the primary and secondary nodes are in the same availability zone, the field is displayed as Subnet. Select an available **subnet** in the VPC from the drop\-down list.<br><br>* If the primary and secondary nodes are in different availability zones, the fields are displayed as **Primary node subnet** and **Secondary node subnet**. From their respective drop\-down lists, select a subnet in the VPC for the **primary** and **secondary** nodes.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A subnet is an IP address block within a VPC. All cloud resources in the VPC must be deployed in a subnet. The subnet assigns private IP addresses to cloud resources. For more information, see <a href="https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet">Create a subnet</a>.</div><br> |
   ||**Allowlist** |Associate an allowlist with the instance. Click the allowlist text box to go to the **Associate allowlist** page. On this page, select an allowlist and click **Confirm** to return to the **Rebuild instance** page. The selected allowlist will then be displayed in the allowlist text box.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can also create a new allowlist on the <strong>Associate allowlist page</strong>. For more information about creating an allowlist, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-allowlist">Create an allowlist</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">An instance can bind a maximum of 100 allowlists.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Click <strong>×</strong> next to the allowlist to remove it.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If a default allowlist is set for the current account, it will appear in the allowlist box.</div><br> |
   |**Account configuration** |**Super account** |The system selects veyun_user by default and this cannot be modified. |
   ||**Super account password** |Set the password for the super account. The requirements are as follows:<br><br><br>* It must contain at least three of the following character types: uppercase letters, lowercase letters, numbers, and special characters.<br><br>* Special characters include `~!@#$%^&*()-_+=?`.<br><br>* It must be 8 to 32 characters long.<br><br>* It cannot contain the string `veyun_user` (case\-insensitive). |
   ||**Confirm password** |Enter the password again. |
   |**Advanced configuration** |**Time zone** |The only supported time zone is (UTC+08:00) Beijing, Chongqing, Hong Kong, Urumqi. |
   ||**Instance character set** |Select the character set for the instance database. Supported options include **Chinese_PRC_90_CI_AI**, **Chinese_PRC_BIN**, **Chinese_PRC_BIN2**, **Chinese_PRC_CI_AI**, **Chinese_PRC_CI_AS**, **Chinese_PRC_CS_AS**, **Chinese_Taiwan_Stroke_CI_AS**, **Chinese_Taiwan_Stroke_CS_AS**, **Cyrillic_General_CI_AS**, **Japanese_CI_AS**, **Japanese_CS_AS**, **Latin1_General_100_CI_AS_SC_UTF8, Latin1_General_CI_AS**, **Latin1_General_CS_AS**, **SQL_Latin1_General_CP1_CI_AS**, **SQL_Latin1_General_CP1_CS_AS**, and **Thai_CI_AS**. The default is **Chinese_PRC_CI_AS**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The instance character set can not be modified after the instance is successfully created.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">We recommend keeping the instance character set consistent with the original instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Even if you select a case\-sensitive instance character set, creating case\-sensitive databases is not supported. For example, databases named A and a will be treated as the same database.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For more information about the instance character set, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide?lang=en#PkNxJyXS">References</a>.</div><br> |
   ||**Project** |(Optional) Select the project for the instance from the dropdown list. The default is **default (Default project)** . You can also click to**create a new project**. For detailed instructions, see [Creating project](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management#creating-project).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">A project is a virtual concept that includes a set of resources, users, and roles. Projects allow you to centrally view and manage a group of resources and control the permissions of users and roles on these resources within the project. For more information, see  and <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Project_Overview">Project overview</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If this item is not configured, the instance you create will not belong to any project.</div><br> |
   ||**Tag** |(Optional) Add tags to the backup instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Tags help identify and categorize cloud resources. RDS for SQL Server lets you add tags to instances for classification, simplifying instance searches and resource aggregation. For more information, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/tag-overview">Tag overview</a>.</div><br> |
   |**Billing information** |**Billing methods** |Select a billing method as needed. The following billing methods are currently supported:<br><br><br>* **Pay\-as\-you\-go**: Select this option for short\-term use of SQL Server instances. Billing is hourly. You can release the instance when it is no longer needed to save costs.<br><br>* **Subscription**: If you plan to use a SQL Server instance for a long term, select the subscription method (one\-time payment), and select the subscription duration in the lower\-left corner of the page. Subscription is more cost\-effective than pay\-as\-you\-go, and the longer the subscription duration, the greater the discount.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you select pay\-as\-you\-go, ensure your BytePlus account has a balance of at least 100 yuan. For more information about billing, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/price-overview">Billing overview</a>.</div><br> |
   ||**Subscription duration** |Select a subscription duration by month (1–9 months) or by year (1–3 years).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you select Subscription as the billing method, you can configure the subscription duration.</div><br> |
   ||**Automatic renewal.**  |Select **Auto\-renewal** if needed. If selected, the platform will automatically renew the instance monthly before expiration, without requiring manual renewal. You can also modify the renewal configuration. For more information, see [Renewal Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-of-renewal-rules).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the Billing method is Subscription, you can configure the Subscription duration.</div><br> |
   

7. Click **Confirm order**.

8. Complete the following steps based on the selected billing method.

   * If the instance's billing method is **Pay\-as\-you\-go**: On the **Confirm Order** page, confirm the order details, select the checkbox to agree to  , [BytePlus Customer Agreement](https://docs.byteplus.com/en/docs/legal/docs-customer-agreement), [Service Specific Terms](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/specific-terms-for-bytePlus-database-products-and-services), and [SLA for RDS for SQL Server](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/service-level-agreement-for-RDS-for-SQL-Server), then click **Buy Now**.

   * If the instance's billing method is **Subscription**:

      1. On the **Confirm Order** page, confirm the order details, read and select [BytePlus Customer Agreement](https://docs.byteplus.com/en/docs/legal/docs-customer-agreement),[ Service Specific Terms](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/specific-terms-for-bytePlus-database-products-and-services), [SLA for RDS for SQL Server](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/service-level-agreement-for-RDS-for-SQL-Server), and click **Submit Order**.

      2. On the **Confirm order Information** page, confirm the order information again, and click **Next**.

      3. On the **Submit payment information** page, confirm the payment details, select a payment method, and click **Go to Pay**. Follow the prompts to complete the payment and rebuild the instance.
