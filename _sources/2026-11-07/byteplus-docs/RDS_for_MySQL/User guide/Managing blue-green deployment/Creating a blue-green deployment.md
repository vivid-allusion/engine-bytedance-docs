---
title: "Creating a blue-green deployment"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Creating_a_blue-green_deployment"
---

RDS for MySQL supports creating blue\-green deployments for instances, which provides seamless switching with zero downtime to ensure business continuity and stability. This article describes the steps to create a blue\-green deployment for an instance.

<span id="fvPvVM77"></span>
## Prerequisites


* An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* To create a pay\-as\-you\-go green instance, ensure that your account balance is 100 yuan or more.

* To create a subscription\-based green instance, ensure your account has a sufficient balance to pay for the order.


<span id="B3OLhtJI"></span>
## Supported regions

The blue\-green deployment feature is currently available only in the following regions:


* China (Beijing)

* China (Shanghai)

* China (Guangzhou)

* Asia Pacific (Johor)


<span id="fKBmzwMd"></span>
## Limitation


* Creating blue\-green deployments for disaster recovery instances is not supported.

* A green instance can be created for an instance with Transparent Data Encryption enabled. However, a blue\-green switch is not supported because Transparent Data Encryption cannot be disabled once it is enabled.

* A green instance can be created for an instance with SSL encryption enabled, but SSL encryption must be disabled before the blue\-green switch.

* The engine type of the green instance must be the same as that of the blue instance and cannot be changed.

* Creating green instances for MySQL 8.4 instances is not supported.


<span id="3RihZwpN"></span>
## Precautions

After a blue\-green deployment is created, the green instance is in global read\-only mode. Do not modify this mode. If this mode is modified, a blue\-green switch cannot be performed.

<span id="1Wp79y97"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. In the left navigation bar, click **Instances** to view the list of RDS for MySQL instances.

4. On the **Instances** page, click the name of the target instance to go to the **Summary** tab.

5. On the **Connectivity** tab, in the **Instance topology** area, click **Create green instance** to go to the **Create green instance** page.

6. On the **Create green instance** page, after completing the settings, click **Confirm order** to go to the **Confirm order** page.

   
   |**Parameter** |**Description** |
   |---|---|
   |Instance name |You cannot set the instance name for the green instance during creation. The default instance name is `the name of the blue instance`+`-green`+`-a six-digit random code`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Since an RDS for MySQL instance name cannot exceed 128 characters, and the `<code>-green</code>` and `<code>-six-digit random code</code>` suffixes take up a fixed 13 characters. If the name of the blue instance exceeds 115 characters, only the first 115 characters are kept.</div><br> |
   |Compatible version |Select the compatible version for the green instance. RDS for MySQL supports two compatible versions, **MySQL 5.7** and **MySQL 8.0**. The rules for selecting a compatible version for the green instance are as follows:<br><br><br>* If the compatible version of the blue instance is MySQL 5.7, you can select MySQL 5.7 or MySQL 8.0 as the compatible version for the green instance.<br><br>* If the compatible version of the blue instance is MySQL 8.0, you can only select MySQL 8.0 as the compatible version for the green instance. |
   |Kernel version |Select the compatible version for the green instance. The rules for selecting the kernel version for the green instance are as follows:<br><br><br>* If the compatible version is the same for both the blue and green instances, you can select a kernel version for the green instance that is equal to or higher than that of the blue instance.<br><br>* If the compatible versions of the blue and green instances are different (for example, the compatible version of the blue instance is MySQL 5.7, and that of the green instance is MySQL 8.0), you can only select the latest kernel version for the green instance.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For more information about the kernel versions released for RDS for MySQL, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/kernal_version_release_notes">Kernel minor version release notes</a>.</div><br> |
   |Instance type |Select the instance type for the green instance. RDS for MySQL provides **Single node**, **Double node**, and **Multiple node** instance types. The rules for selecting the instance type for the green instance are as follows:<br><br><br>* If the blue instance is a single\-node type, you can select a single\-node or double\-node type for the green instance.<br><br>* If the blue instance is a double\-node type, you can select a double\-node or multiple\-node type for the green instance.<br><br>* If the blue instance is a multiple\-node type, you can only select the multiple\-node type for the green instance. |
   |Specification type |Select the specification type for the green instance. RDS for MySQL provides two specification types: **General type** (formerly 'Shared type') and **Dedicated type** (formerly 'General type').<br><br><br>* General type: Exclusive use of allocated memory and storage resources, shares CPU resources with other shared instances in the same physical machine.CPU utilization is maximized through resource reuse, with high cost performance. CPU utilization is maximized through resource reuse, with high cost performance.<br><br>* Dedicated type: Fully exclusive use of allocated CPU, memory, and storage resources, with stable performance, not affected by other instances in the physical machine.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The specification type of the green instance is the same as the blue instance by default and can be modified. If the instance type of the blue instance is Single node, the specification type of the green instance can only be General type.</div><br> |
   |Node specification |Configure the node specification, availability zone, and number of nodes for the green instance. The node configuration for the green instance is the same as the blue instance by default, but it can be adjusted. The specific configuration rules are as follows:<br><br><br>* If you choose the instance type as **Double node**:<br><br>   * Up to 10 read\-only nodes can be added, and the data on each node is exactly the same as the primary node.<br><br>   * You can specify different availability zones in the same region for the primary node and the secondary node.<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">For zone\-level disaster recovery, it is recommended to deploy the primary and secondary nodes in different availability zones.      </div><br>      <br><br>   * The specification of the secondary node is consistent with that of the primary node.<br><br>   * Up to 10 read\-only nodes can be added, and the specifications of the read\-only nodes can be set on demand.<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If the specification of a read\-only node is lower than that of the primary node, high load on the primary node may cause latency or even OOM in the read\-only node. It is recommended to select the same or a higher specification for the read\-only nodes as that of the primary node.      </div><br>      <br><br>   * Primary, secondary, and read\-only nodes can be deployed in up to three availability zones.<br><br>* If you choose the instance type as **Multiple node**:<br><br>   * The specification of the secondary node is consistent with that of the primary node.<br><br>   * You can add up to 8 secondary nodes, and at least 1 secondary node needs to be reserved.<br><br>   * Nodes can be distributed in at most 3 availability zones.<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">For zone\-level disaster recovery, it is recommended to deploy the primary and secondary nodes in different availability zones.      </div><br>      <br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the blue instance is a double\-node type and you select the multiple\-node type for the green instance, the read\-only node configuration of the blue instance will not be retained for the green instance.   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For multi\-node instances, it is recommended to reserve an independent secondary node that does not carry business, so that it can be switched to the primary node if necessary. RDS for MySQL assumes no responsibility for any risks or losses incurred due to the failure to configure independent secondary nodes or the inability to complete the primary node switching due to excessive latency of all secondary nodes.   </div><br>   <br><br>* If the instance type is **Single node**, you only need to set the specification and availability zone for the primary node. |
   |Storage type |Select the storage type for the instance. You can select **Local SSD, Cloud ESSD FlexPL, Cloud ESSD PL0**, or **High performance cloud disk** as the storage type.<br><br><br>* **Local SSD disk**: An SSD disk on the same node as the database engine. Storing data on the local SSD disk reduces I/O latency.<br><br>* **Cloud ESSD FlexPL**: High throughput, high IOPS, and low latency, suitable for large I/O\-intensive business scenarios.<br><br>* **Cloud ESSD PL0**: Balanced IOPS and throughput, and low latency, suitable for scenarios with certain IO performance requirements.<br><br>* **High performance cloud disk:**  Built on Cloud ESSD FlexPL, it provides additional IO bursting capabilities to meet IO demands during business peaks. Suitable for scenarios with high I/O loads and I/O fluctuations.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the instance type is <strong>Single node</strong>, you can only select <strong>Cloud ESSD FlexPL, Cloud ESSD PL0</strong>, or <strong>High performance cloud disk</strong> as the storage type. <strong>Local SSD disk</strong> is supported, and the SSD must be in the same node as the database engine.</div><br> |
   |Storage space |Storage space includes data space, system file space, Binlog file space, and transaction file space. Enter a storage space from 20 GiB to 32,000 GiB in 10 GiB increments based on your business requirements.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The storage space of the green instance must be greater than or equal to both the storage space of the blue instance and the minimum space of the instance specification. For more information on the value range of storage space corresponding to each specification, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications">Product specifications</a>.</div><br> |
   |Deletion protection |Set whether to enable deletion protection for the green instance. Deletion protection is a feature provided by RDS for MySQL to protect instances from accidental deletion. After this feature is enabled, the instance cannot be deleted directly. You must disable the deletion protection for the instance before it can be deleted.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Deletion protection is enabled by default for the green instance.</div><br> |
   |Network protocol type |Set the network protocol type of the green instance. The green instance must use the same network protocol type as the blue instance. |
   |Virtual private cloud |The green instance must use the same virtual private cloud as the blue instance. This setting cannot be changed. |
   |Subnet |Select the subnet for the green instance. The subnet used by the blue instance is selected by default. You can also select another subnet within the virtual private cloud of the blue instance. |
   |Database proxy |Configure the database proxy for the green instance. The following rules apply when configuring the database proxy for a green instance:<br><br><br>* If the green instance is a Double node instance, you can enable or disable its database proxy.<br><br>* If the instance type of the blue instance is multiple node, the database proxy for the green instance can only be enabled. |
   |Number of proxy cores |Set the number of cores for the database proxy service of the green instance. The value range for the number of cores for the proxy service varies by instance type:<br><br><br>* Maximum: 1024.<br><br>* Minimum value:<br><br>   * Multiple node instance: The greater of 2 or (Number of primary node CPU cores \* 0.125).<br><br>   * Double node instance: The greater of 2 or (Number of primary node CPU cores \* 0.5).<br><br>* Default value:<br><br>   * Multiple node instance: (Total number of CPU cores of all available nodes in the instance \* 0.25), rounded up.<br><br>   * Double node instance: (Total number of CPU cores of all available nodes in the instance \* 0.5), rounded up. |
   |Parameter configuration |Configure parameters for the green instance. The rules for configuring parameters for the green instance are as follows:<br><br><br>* If the blue and green instances have the same compatible version, you can set the parameter configuration for the green instance to **Inherit the blue instance** or **Select parameter template**.<br><br>* If the blue and green instances have different compatible versions, the parameter configuration for the green instance can only be set to **Select parameter template**. |
   |Parameter templates |If **Parameter configuration** is set to **Select parameter template**, select a parameter template for the green instance. You can select a system or custom parameter template for the green instance from the drop\-down list. |
   |Kernel version upgrade policy |Method for upgrading the database kernel minor version. The following types are supported.<br><br><br>* Automatic: When a new kernel minor version is released, the instance is automatically upgraded to the latest kernel version during the configured [Maintenance window](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period?lang=en).<br><br>* Manual: When a new kernel minor version is released, you must manually upgrade to the latest kernel version in the console. For details, refer to [Manually upgrading instance kernel minor versions](https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version?lang=en).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If an instance's kernel minor version exceeds its maintenance cycle, the system temporarily ignores the upgrade policy and automatically upgrades the kernel minor version.</div><br> |
   |Billing method |Select the billing method for the green instance. RDS for MySQL supports two billing methods: **Pay\-as\-you\-go** and **Subscription**.<br><br><br>* Pay\-as\-you\-go: If you plan to use your MySQL instance for a short period of time, choose pay\-as\-you\-go (hourly rate). You can release the instance when it is no longer needed, saving money.<br><br>* Subscription: If you plan to use your MySQL instance for a long period of time, select Subscription (one\-time payment) and choose the duration of the purchase in the lower left corner of the page. Subscription is more affordable than pay\-as\-you\-go, and the longer you buy, the more discounts you get.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can also create a pay\-as\-you\-go instance first and confirm that the instance meets the requirements before switching to a yearly/monthly subscription.</div><br> |
   |Subscription duration |If you choose Subscription, you need to select the purchase duration. Support monthly purchase (can purchase 1~9 months) and yearly purchase (can purchase 1~3 years). |
   |Automatic renewal |If you select Subscription, you can also configure **Automatic renewal**. If enabled, the platform automatically renews the subscription on a monthly basis before the instance expires, without requiring manual renewal. You can also modify the renewal configuration. For more information, please refer to [Renewal Management](https://console.byteplus.com/finance/renew/). |
   

7. On the **Confirm order** page, confirm the order details. After reading and selecting [Database Products and Services Terms](https://docs.byteplus.com/en/docs/RDS_for_MySQL/service-specific_terms) and [Unsubscription rules](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management), click **Buy now** to create a green instance.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">On the <strong>Create green instance</strong> page, the creation progress of the green instance is displayed. Click <a href="https://console.byteplus.com/db/region:db+cn-guangzhou/rds-mysql/taskCenterDetail/202501062132291128321CAC330B1F9478-f00f35">Task center</a> on the page to go to the task page in the task center and view the details for creating the green instance. If the <strong>Create green instance</strong> page is closed, click <strong>Green instance creation progress</strong> in the <strong>Instance topology</strong> area of the blue instance to reopen the page.</div>


* <div data-tips="true" data-tips-type="default">After the green instance is created, it appears in the Instances list.</div>


* <div data-tips="true" data-tips-type="default">Billing for the green instance starts upon its creation. Click <strong>Create synchronization link</strong> as soon as possible to establish a synchronization link between the blue and green instances.</div>


* <div data-tips="true" data-tips-type="default">After the green instance is created, the blue and green instances are labeled "Blue" and "Green" respectively.</div>



<span id="kFDmd25x"></span>
## Subsequent steps

[Create a synchronization link for the blue-green deployment](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Creating_a_blue-green_deployment)

<span id="3rib03p5"></span>
## Related API


|API |Description |
|---|---|
|[CreateDBBlueGreenInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/CreateDBBlueGreenInstance) |Call the CreateDBBlueGreenInstance API to create a blue\-green deployment for an instance. |
|[DescribeDBBlueGreenInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBBlueGreenInstance) |Call the DescribeDBBlueGreenInstance API to query the blue\-green deployment information for the instance. |
