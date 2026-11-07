---
title: "Viewing instance information"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/view-instance"
---

You can view the instance's basic information, configuration information, billing information, and node information on the MongoDB console. This topic describes how to view MongoDB instance information.

## Prerequisite

MongoDB instance has been created. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/mongodb/create-instance).

## Procedure

1. Log on to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

   > **tip**

   * > If there are many instances in your list, you can quickly find the target instances that meet the conditions in the search box above the list by using the instance name or instance ID. The search rules are as follows:

      * > Fuzzy search is supported for instance names, while only exact search is supported for instance IDs.

      * > You can enter multiple instance names or instance IDs for search simultaneously. Separate multiple names or IDs with a comma (,).

      * > The length of the instance name entered for each search shall not exceed 120,000 characters, and the instance ID shall not exceed 800 characters.

      * > Multiple instance names or instance IDs are in an **OR** relationship.

   * > For instances with a long name, you can adjust the list by dragging the right border of the **Instance name/ID** column.

5. You can view the following information about the MongoDB instance under the **Summary** tab.

   |Information category |Description |
   |---|---|
   |Basic information |You can perform the following actions in the **Basic information** area:<br><br><br>* View information such as instance ID, name, type, creation time, associated tags, and the instance's VPC, subnet, and availability zone.<br><br>* Modify instance names, manage instance tags, and so on. For how to manage instance tags, refer to [Tag management](https://docs.byteplus.com/en/docs/mongodb/tag-overview). |
   |Configuration |Different instance types display different configuration information, specifically:<br><br><br>* **Sharding cluster**: Supports viewing the database version, storage type, specification type, storage engine, AI capabilities (enabled/not enabled), maximum available storage space, total number of shards, the number and specifications of nodes in each shard, the specifications and number of Mongos and ConfigServer nodes, and the number of read\-only nodes.<br><br>* **Replica set**: Supports viewing the database version, storage type, specification type, instance specification, maximum available storage space, storage engine, AI capabilities (enabled/not enabled), and the number of read\-only nodes.<br><br><br>> **tip**<br><br><br>> Maximum available storage is the disk space available for storing business data. The calculation method of maximum available storage capacity varies with the instance type. For the specific calculation method, refer to [Maximum available storage](https://docs.byteplus.com/en/docs/mongodb/product-specification?lang=en#f60XnNXz).<br> |
   |Billing information |View instance billing method information and some billing\-related operations. Different instance billing methods support different operations, including:<br><br><br>* **Subscription**: View the expiration date of subscription instances. You can manually renew or enable automatic renewal before the instance expires. For specific procedures, refer to [Automatic or manual renewal](https://docs.byteplus.com/en/docs/mongodb/automatic-manual-renewal).<br><br>* **Pay\-as\-you\-go**: Supports switching the billing method of pay\-as\-you\-go instances to subscription. For specific procedures, refer to [Switching to subscription](https://docs.byteplus.com/en/docs/mongodb/switch-to-subscription). |
   |Node information |The node information and operations available vary by instance type. Specifically:<br><br><br>* **Sharding cluster**<br><br>   * **Mongos**<br><br>      View information such as ID, status, specifications, CPU utility, availability zone, and memory utility for each Mongos node.<br><br>   * **Shard**<br><br>      * View information such as ID, status, role, specifications, storage space, CPU utility, availability zone, memory utility, space utility, and replication lag for each node within each Shard.<br><br>      * Modify the configuration of a specified Shard (including scaling node specifications and storage space). For specific procedures, refer to [Modifying Sharding configuration](https://docs.byteplus.com/en/docs/mongodb/modify-shard-config).<br><br>      * Switch the roles of primary and secondary nodes within a specified Shard. For specific procedures, refer to [Switching primary node](https://docs.byteplus.com/en/docs/mongodb/switch-primary-node).<br><br>   * **Mongot**<br><br><br>View information such as the ID, status, specifications, CPU utility, availability zone, and memory utility for each Mongot node.<br><br><br>   * **ConfigServers**<br><br>      * View information such as the ID, status, role, specifications, storage space, CPU utility, availability zone, memory utility, and space utility for each ConfigServer node.<br><br>      * Modify the configuration of ConfigServer nodes (including upgrading or downgrading node specifications and storage space). For specific procedures, refer to [Modifying ConfigServer node configuration](https://docs.byteplus.com/en/docs/mongodb/modify-configserver-config).<br><br>      * Switch the roles of primary and secondary nodes in ConfigServer. For specific procedures, refer to [Switching primary node](https://docs.byteplus.com/en/docs/mongodb/switch-primary-node).<br><br>* **Replica set**<br><br>   * **Mongod**<br><br>      * View information such as the ID, status, role, specifications, CPU utilization, availability zone, memory utilization, space utilization, and primary\-secondary replication lag for Mongod nodes in the instance.<br><br>      * Change the configuration of Mongod nodes in the instance, including upgrading or downgrading node specifications and storage space. For specific procedures, refer to [Modifying replica set instance configuration](https://docs.byteplus.com/en/docs/mongodb/modify-replica-set-instance-spec).<br><br>      * Switch the roles of primary and secondary nodes in instance. For specific procedures, refer to [Switching primary node](https://docs.byteplus.com/en/docs/mongodb/switch-primary-node).<br><br>      > **tip**<br>      <br><br>      > If your instance is deployed in multiple availability zones, different role nodes will be located in different availability zones. For more details, refer to [Multi\-availability\-zone disaster recovery solution](https://docs.byteplus.com/en/docs/mongodb/multi-az-solution?lang=en).<br>      <br><br>* **Mongot**<br><br><br>View information such as the ID, status, specifications, CPU utility, availability zone, and memory utility for Mongot nodes. |

## Relevant APIs

|API |Description |
|---|---|
|[DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) |Call the DescribeDBInstances API to query the basic information of the MongoDB instance. |
|[DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/mongodb/describedbinstancedetail) |Call the DescribeDBInstanceDetail API to query the detailed information of the target MongoDB instance. |
