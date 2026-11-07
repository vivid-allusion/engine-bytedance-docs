---
title: "Regular modification of specification"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/regular-modification-of-specification"
---

You can regularly modify your instance configuration to meet your business needs. This topic describes how to adjust the node specification and storage space for your instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**

An instance has been created and is in the **Running** state. For details, see [Create an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Shrinking the storage space is not currently supported.

* Modifying the instance configuration causes database interruptions or transient disconnections. During this process, most operations related to the database, accounts, and network cannot be performed. Avoid changing the node specification during peak business hours.

* You do not need to manually restart the instance after its configuration is modified. The process takes several minutes, and the exact duration depends on the amount of stored data, write speed, and the number of read\-only nodes.

* Modifying the configuration does not change the instance ID or connection address.

* Note the following when a primary instance has read\-only instances:

   * When modifying the storage space of a primary instance or a read\-only instance, ensure that the storage space of the read\-only instance is greater than or equal to that of the primary instance. Otherwise, the modification will fail.

   * The number of cores of a read\-only instance must be at least half the number of cores of the primary instance.


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper\-left corner of the top menu bar, select the project and region where the instance is located.

3. RDS for SQL Server provides two entries for you to modify the configuration:

   * On the **Instances** page, click **Modify configuration** in the **Acitons** column for the target instance or read\-only instance.

   * On the **Instance details** page, click **Modify configuration** in the upper\-right corner.

4. Configure the following parameters based on your business requirements:

   
   |**Parameter** |**Description** |
   |---|---|
   |**Configuration modification type** |**Regular modification of specification** is selected by default. |
   |**Specification type** |Select a specification type as needed. The available options are **Exclusive Type II** and **General Type II**. **Exclusive Type II** and **General Type II** can be changed to **Exclusive Type II** or **General Type II**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For more information about each specification type, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/product-specification-family">Product specification family</a>.</div><br> |
   |**Node specification** |Configure the specifications and availability zones for the instance's primary and secondary nodes as needed. Details are as follows:<br><br><br>* **Node specification**: Select the node specification for the primary node from the drop\-down list. The specification for the standby node automatically matches that of the primary node. For more information about node specifications, see [Node specification](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/master-instance-specification).<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can change node specifications to other specifications within the same family or upgrade to a higher specification family. The supported modification logic is as follows:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The 1ie specification family can be changed to the 1ie, 3il, and 4il specification families.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The 3il specification family can be changed to the 3il and 4il specification families, but not to the 1ie specification family.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The 4il specification family can be changed to the 4il specification family, but not to the 1ie or 3il specification families.   </div><br>   <br><br>* **Availability zones**: Select the availability zone for the node from the drop\-down list. The availability zone is the geographic location of the node. If an instance has primary and secondary nodes, you can deploy them across different availability zones.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Select an availability zone close to your target users to improve access speed.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The availability zone can not be modified after the instance is created successfully.   </div><br>    |
   |**Storage Type** |**Extremely\-Fast SSD PL1 Cloud Disk** is selected by default. |
   |**Storage space** |Storage space includes data file space and temporary file space. Enter a storage space between 20 GiB and 4000 GiB in 10 GiB increments. Select a value based on your business needs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Storage resizing does not cause connection interruptions.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For details on the storage space range for each instance specification, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/master-instance-specification">Instance specification</a>.</div><br> |
   |**Execution Time** |You can select **Execute Now** or **Maintenance window**.<br><br><br>* **Execute Now**: The modification is executed immediately after the order is submitted.<br><br>* **Maintenance window**: The modification is executed during the maintenance window set for the instance. You can view the current maintenance window set for instance on the **Summary page**. To adjust it, see [Set maintenance window](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/configuring-maintenance-window).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you choose to modify the configuration during the maintenance window, RDS for SQL Server immediately starts preliminary actions such as resource scheduling and data synchronization after the order is submitted, and the instance status switches to <strong>Updating</strong>. The route is switched after the maintenance window begins. After the task is complete, the instance status changes to <strong>Running</strong>.</div><br> |
   

5. Click **Confirm order**.

6. Complete the subsequent steps based on the billing method of the instance.

   * If the instance's billing method is **Pay\-as\-you\-go**: On the **Confirm Order** page, confirm the order details, select the checkbox to agree to  , [BytePlus Customer Agreement](https://docs.byteplus.com/en/docs/legal/docs-customer-agreement), [Service Specific Terms](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/specific-terms-for-bytePlus-database-products-and-services), and [SLA for RDS for SQL Server](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/service-level-agreement-for-RDS-for-SQL-Server), then click **Buy Now**.

   * If the instance's billing method is **Subscription**:

      1. On the **Confirm Order** page, confirm the order details, read and select [BytePlus Customer Agreement](https://docs.byteplus.com/en/docs/legal/docs-customer-agreement),[ Service Specific Terms](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/specific-terms-for-bytePlus-database-products-and-services), [SLA for RDS for SQL Server](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/service-level-agreement-for-RDS-for-SQL-Server), and click **Submit Order**.

      2. On the **Confirm order Information** page, confirm the order information again, and click **Next**.

      3. On the **Submit payment information** page, confirm the payment details, select a payment method, click **Go to Pay**, and follow the prompts to complete the payment and create the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details on the fees related to configuration changes, refer to <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/unsubscribe-or-change-instructions">Unsubscription and modification instructions</a>.</div>
