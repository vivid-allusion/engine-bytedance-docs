---
title: "Creating read-only instance"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-read-only-instance"
---

Read\-only instances are primarily used to offload the read pressure of the master instance. When there are a large number of read requests in the database, a master instance may not be able to meet the pressure of a large number of read and write requests at the same time. You can create multiple read\-only instances for the master instance to help you reduce the read pressure of the master instance and improve the overall processing power of the system. This article describes how to create a read\-only instance in the SQL Server Edition console of a cloud database.

<span id="prerequisite"></span>
## prerequisite

The cloud database SQL Server Moderator instance has been created, and the master instance must meet the following conditions. For the steps to create a master instance, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance).


* Compatible version: SQL Server 2019 Enterprise Edition.

* Instance Type: Cluster Edition.

* Instance status: Running.


<span id="precautions"></span>
## Precautions


* An instance can create up to 5 read\-only instances, and multiple read\-only instances under the master instance are independent of each other and do not affect each other.

* The time to create a read\-only instance is proportional to the amount of data and I/O of the master instance, so you need to evaluate and optimize the amount of data and I/O performance of the master instance before creating a read\-only instance to reduce the time it takes to create a read\-only instance to impact the performance of the master instance.

* **The primary instance in a read\-only instance change** or **in a changing** state does not support creating a new read\-only instance. The master instance in a read\-only instance change does not support modifying the configuration of the master instance.

* Only creating a read\-only instance on the master instance is supported, and switching the master instance to a read\-only instance is not supported.

* The data of the read\-only instance is replicated and synchronized from the data of the primary instance, and filtering of certain data is not supported.

* Configuration related precautions:

   * The read\-only instance is in the same region as the primary instance by default, and does not support modification.

   * A read\-only instance may not be in the same Availability Zone as the primary instance, and can be set up on its own when creating an instance.

   * The storage space of the read\-only instance needs to be greater than or equal to the storage space of the primary instance.

   * The specifications of the read\-only instance can be inconsistent with the master instance. In order to ensure sufficient I/O performance support when data is synchronized from the master instance to the read\-only instance, it is recommended to be greater than or equal to one\-half of the number of node specifications of the master instance.


<span id="operation-steps"></span>
## Operation steps


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. In the left navigation bar, click **Instance List**.

4. On the **Instance List** page, select... under the Target Enterprise Edition Instance **Actions column.**  \> **Create a read\-only instance**.

5. On the **Create Read\-Only Instance** page, configure the following parameter information.

   
   |**Category** |**parameter** |**explain** |
   |---|---|---|
   |**master instance configuration** ||**The master instance configuration** area displays the details of the master instance by default, including the name, ID, database version, instance type, VPC, subnet, availability area, node specification, and storage space of the master instance. You don't need to modify or configure it. |
   |**Basic information** |**compatible version** |The default is consistent with the master instance, and no modification is supported. |
   ||**instance name** |(Optional) Set the name of the read\-only instance. The naming convention is as follows:<br><br><br>* Can only contain Chinese, letters, numbers, underscores (_) and underscores (\-).<br><br>* The length should be between 1 and 128 characters.<br><br>* Cannot start with a number or a dash (\-).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the read\-only instance name is not set, the read\-only instance name is the same as the read\-only instance ID.</div><br> |
   |**specification configuration** |**instance type** |By default, **read\-only instances** are selected and modification is not supported. |
   ||**Specification type** |Select the specification type on demand, support the selection of **exclusive type**, **general type**, **exclusive type II**, **general type II**, as follows:<br><br><br>* **Exclusive type**, **exclusive type II**: Exclusive instance performance is better and more stable, suitable for business scenarios with database as the core system, such as finance, e\-commerce, government affairs, large and medium\-sized Internet business, etc.<br><br>* **General\-purpose type**, **General\-purpose type II**: General\-purpose examples are suitable for scenarios with high cost and cost performance requirements.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For more information on each specification type, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/product-specification-family">Product Specification Family</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Since Universal and Exclusive will not be sold in the new Availability Zone, you will not be able to directly purchase instances of these two specifications in the newly opened Availability Zone. Therefore, it is recommended that you choose Universal and Exclusive Type II first when creating new instances. This ensures that RDS for SQL Server instances are highly available and support cross\-availability zone configuration, improving system redundancy and reliability.</div><br> |
   ||**Node specification** |Sets the node specification and availability zone for the read\-only instance. The details are as follows:<br><br><br>* **Node specification**: Select the node specification of the read\-only instance from the node specification drop\-down list. Different node specifications indicate that the computing resources used by the instance are different, such as CPU, memory, storage, etc. For more information, see [Read-Only Instance Specifications](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/read-only-instance-specification).<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In order to ensure sufficient I/O performance support when data is synchronized from the master instance to the read\-only instance, the node specification of the read\-only instance is recommended to be greater than or equal to the node specification of the master instance.   </div><br>   <br><br>* **Availability Zones**: Select Availability Zones from the Availability Zones drop\-down list. Each region has multiple isolated areas called Availability Zones, and there is no essential difference between different Availability Zones. |
   ||**Storage space** |Storage space includes data file space and temporary file space. Please enter a storage space in the range of 20 GiB to 4000 GiB, with a step size of 10 GiB. Please choose reasonably according to the business situation.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The storage space of the read\-only instance needs to be greater than or equal to the storage space of the primary instance.</div><br> |
   |**network configuration** |**private network** |The private network of a read\-only instance is by default the same as the private network of the primary instance, and does not support modification. |
   ||**subnet** |Select the subnets available within the private network from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A subnet is a block of IP addresses within a private network. All cloud resources in a private network must be deployed within subnets, which are cloud quota private IP addresses. For more details, see <a href="https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet">Creating subnets</a>.</div><br> |
   ||**Allowlist** |Bind a allowlist for the instance. Click the allowlist text box to go to the **binding Allowlist** page. On this page, after checking the allowlist, click **Confirm** and return to the **Create Instance** page. The selected allowlist will be displayed in the allowlist text box.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">In the <strong>binding allowlist</strong> page, you can also create a new allowlist. For more information about creating a allowlist, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-allowlist">Creating allowlist</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">An instance can bind up to 100 Allowlists.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Click × after the allowlist to remove the allowlist.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If there is a default allowlist set under the current account, then the allowlist will appear in the allowlist box.</div><br> |
   |**Advanced Configuration** |Instance Character Set |The instance character set of a read\-only instance is the same as the instance character set of the primary instance by default, and modification is not supported. |
   ||**time zone** |The time zone of a read\-only instance defaults to the same time zone as the primary instance, and does not support modification. |
   ||**Tag** |(Optional) Click **Add Tag** to set the tag for the read\-only instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Tags are used for the identification and classification of cloud resources. RDS for SQL Server supports adding tags for read\-only instances. You can organize SQL Server read\-only instances by tags to facilitate instance search and resource aggregation. For more information, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/tag-overview">Tag Overview</a>.</div><br> |
   |**Billing Information** |**Billing Type** |You can choose the billing method for read\-only instances on demand. RDS for SQL Server Read\-Only Instances support **volume billing** and **annual subscription monthly** billing methods:<br><br><br>* **volume billing**: If you plan to use SQL Server Read\-Only Instances for a short period of time, please select volume billing (hourly billing). You can release the instance when it is no longer needed, saving money.<br><br>* **Pack Year Pack Month**: If you plan to use SQL Server Read\-Only Instances for a long time, select Pack Year Pack Month (One\-Time Payment) and select Duration of Purchase in the lower left corner of the page. The annual package is more affordable than the volume\-based billing, and the longer the purchase time, the more discounts.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can also create a read\-only instance of billing by volume first, and then subcontract the annual package after confirming that the instance meets the requirements. For more information about billing, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/price-overview">Billing Overview</a>.</div><br> |
   ||**purchase duration** |Select the purchase duration of the year and month on demand.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In the <strong>billing method</strong>, when selecting the <strong>annual package month</strong>, support setting the purchase time.</div><br> |
   ||**Auto\-Renewal** |Set on\-demand whether you need to auto\-renew the monthly subscription instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the <strong>billing method</strong> selects the <strong>package year and month</strong>, it supports setting automatic renewal.</div><br> |
   

6. Click **Confirm Order**.

7. Complete the next steps based on the selected billing type.

   * If you select **Billing by Volume**: On the **Confirm Order** page, confirm the order details, read and tick the **Database Product and Service Terms**, and click **Buy Now**.

   * If you choose the **annual package month**:

      1. On the **Confirm Order** page, confirm the order details, read and tick the **Database Product and Service Terms**, and click **Submit Order**.

      2. On the **Confirm Order Information** page, reconfirm the order information and click **Next**.

      3. On the **Submit Payment Information** page, confirm the payment details and select the payment method, click **Go to Pay**, and complete the payment according to the prompts to create the instance.
