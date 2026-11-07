---
title: "Changing instance type"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_instance_type"
---

RDS for MySQL supports the creation of single\-node instances (one primary node), double\-node instances (one primary, one secondary, and multiple read\-only nodes), and multi\-node instances in cluster mode (one primary and multiple secondary nodes). It also supports changing single\-node instances to double\-node or multi\-node instances, and changing double\-node instances to multi\-node instances. This topic describes the steps for changing the instance type.

## Prerequisites

* A single\-node or double\-node instance has been created and is in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* The database agent function of the instance is enabled. For specific operations, refer to [Enabling the database proxy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enable_database_agent).

## **Precautions**

* Changing the type of an instance that is temporarily upgraded is not supported.

* Changing the type of a multiple node instance is not supported.

* Changing the instance type can cause the automatic restart of the instance or data migration, resulting in database connection interruption. During the change of the instance type, most operations related to the database, account number, and network cannot be executed. Please proceed with caution.

* When a double\-node instance is changed to a multi\-node instance, the read\-only nodes under the current double\-node instance are removed. You can add secondary nodes on the **Change instance type** page as required.

* Multi\-node instances support a default endpoint, a write endpoint, a read\-only endpoint, and three custom read\-write direct connection endpoints. The default endpoint will inherit connection information from the double\-node instance. The write endpoint and read\-only endpoint will be automatically created, and custom endpoints will be automatically migrated. Before changing the instance type, assess and remove unqualified or over\-limit custom endpoints on the Connectivity tab to prevent the change from failing due to excessive custom endpoints.

* During the change of the instance type, you can only add secondary nodes and set the availability zones of primary and secondary nodes, and cannot modify the node specifications. For the modification of node specifications, refer to [Modifying an instance specification](https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_an_instance_configuration) after changing the instance type.

* A MySQL instance can only use subnets in the availability zones of its primary or secondary nodes. When changing the instance type, you cannot simultaneously deploy the primary node and all secondary nodes in availability zones different from the subnet's availability zone.

## Procedure

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the project and region for the instance.

   > **tip**

   > If the project of the instance has not been set, the project should be selected as **All resources**.

3. Click **Instances** in the left navigation bar.

4. Enter the **Change instance type** page for the target instance. RDS for MySQL provides two entry points:

   * On the **Instances** page, click **Modify configuration** \> **Change instance type** in the **Actions** column of the target instance.

   * After clicking the target instance name, click **Modify configuration** \> **Change instance type** in the upper right corner of the page.

5. On the **Change instance type** page, complete the following configuration.

   |Parameter |Description |
   |---|---|
   |Instance type |Supports Double node or Multiple node. |
   |Migrate endpoint |Multi\-node instances only support the default endpoint, write endpoint, read\-only endpoint, and up to three custom read\-write direct connection endpoints. The default endpoint will inherit connection information from the double\-node instance or single\-node instance. The write endpoint and read\-only endpoint will be automatically created, and custom endpoints will be automatically migrated. Before changing the instance type, assess and remove unqualified or over\-limit custom endpoints on the Connectivity tab. |
   |Node specification |Set the availability zones for the primary and secondary nodes, and add nodes on demand. Click the **Add secondary node** or **Add read\-only node** button at the bottom left to add a node. The setting rules are as follows:<br><br><br>* The setting rules for changing a single\-node instance to a double\-node or multi\-node instance are as follows:<br><br>   * The specification of the secondary node is consistent with that of the primary node.<br><br>   * Up to 10 read\-only nodes can be added, and the specifications of the read\-only nodes can be set on demand.<br><br>   * Primary, secondary, and read\-only nodes can be deployed in up to three availability zones.<br><br>* The setting rules for changing a double\-node instance to a multiple\-node instance are as follows:<br><br>   * Modifying the node specification when changing the instance type is not supported.<br><br>   * The specification of the secondary node is consistent with that of the primary node.<br><br>   * You can add up to 8 secondary nodes, and at least 1 secondary node needs to be reserved.<br><br>   * Nodes can be distributed in at most 3 availability zones.<br><br><br>> **tip**<br><br><br><br>* > For zone\-level disaster recovery, it is recommended to deploy the primary and secondary nodes in different availability zones.<br><br><br>* > For double\-node instances, if the specification of a read\-only node is lower than that of the primary node, high load on the primary node may cause latency or even OOM on the read\-only node. It is recommended to select the same or a higher specification for the read\-only nodes as that of the primary node.<br><br><br>* > For multiple\-node instances, it is recommended to reserve an independent secondary node that does not handle business workloads, allowing it to be switched to the primary node when necessary. RDS for MySQL assumes no responsibility for any risks or losses incurred due to the failure to configure independent secondary nodes or the inability to complete the primary node switching due to excessive latency of all secondary nodes.<br> |
   |Switch time |Select the switch time of the change. You can choose **Execute now** or **Maintenance window**.<br><br><br>* **Execute now**: Execute immediately after submitting the instance specification modification order.<br><br>* **Maintenance window**: Execute within the maintenance window set for the instance. You can view the currently set maintenance window for your instance on the Summary page. To adjust, see [Configuring maintenance window](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period).<br><br><br>> **tip**<br><br><br>> If you select to change the specification during the maintenance window, RDS for MySQL will immediately perform prerequisite actions such as resource scheduling and data synchronization after the modification order is submitted, and the instance status will be switched to Modifying. The route will be switched after the maintenance window starts. After the task is completed, the instance status will change to Running.<br> |

6. Click **Confirm order**.

7. Complete the subsequent steps based on the billing type selected.

   * If the billing method of the original instance is **Pay\-as\-you\-go**: on the **Confirm order** page, confirm the order details, read and check the **Database Products and Services Terms** and **Unsubscription rules**, and then click **Buy now**.

   * If the billing method of the original instance is **Subscription**:

      1. On the **Confirm order** page, confirm the order details, read and check the **Database Products and Services Terms** and **Unsubscription rules**, and click **Submit the order**.

      2. On the **Confirm order information** page, reconfirm the order information, and click **Next step**.

      3. On the **Submit payment information** page, confirm the payment details and select the payment method, click **Go to payment**, and complete the payment according to the prompts to complete the change of the instance type.
