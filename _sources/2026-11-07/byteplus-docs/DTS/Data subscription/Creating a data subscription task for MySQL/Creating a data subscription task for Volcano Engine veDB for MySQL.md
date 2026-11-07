---
title: "Creating a data subscription task for Volcano Engine veDB for MySQL"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Creating_a_data_subscription_task_for_Volcano_Engine_veDB_for_MySQL"
---

This topic describes how to create a data subscription task for BytePlus veDB MySQL on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An RDS for MySQL database has been set up independently and is accessible via the public network.

* If consuming data through the Kafka connected over express network, configure the consumer information as needed, as shown below:

   * When using VPN to achieve data subscription, the local network of the self\-managed database has been connected to the BytePlus via VPN gateway. For detailed steps, refer to [Building a cloud VPC and on-premises multi-data-center network interconnection](https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-multiple-data-centers).

   * If data subscription requires a dedicated line connection, you need to establish a dedicated line connection between a single cloud VPC and a single on\-premises data center network. For more information, refer to [Configuring direct connections](https://docs.byteplus.com/en/docs/directconnect/Quick-start).


<span id=".6K6i6ZiF5YmN5YeG5aSH"></span>
## Preparation before subscription


* Allowlist and access permissions:

* When the access method of the database instance is self\-managed over the Internet and access restrictions are enabled, add the DTS server IP addresses to the allowlist or security group of the database instance before creating the database transmission task. DTS server IP addresses vary by region, as detailed below:

   * DTS server IP addresses in China (Guangzhou), China (Shanghai), and China (Beijing) are `221.194.189.0/27,157.148.90.32/27,180.184.132.64/27,61.129.54.64/27,220.196.172.32/27,117.135.143.32/27,220.196.168.32/27,116.132.250.32/27,111.45.13.32/27,125.88.248.32/27,180.153.35.32/27,220.181.65.32/27,220.181.65.64/27`.

   * DTS server IP addresses in Asia Pacific (Johor) are `101.47.0.32/27,220.181.65.32/27,220.181.65.64/27,101.47.65.192/27,101.47.65.32/27`.

   * DTS server IP addresses in Asia Pacific (Jakarta) are `221.194.189.0/27,157.148.90.32/27`.

   * DTS server IP addresses in China (Hong Kong) are `101.47.0.32/27,220.181.65.32/27,220.181.65.64/27,101.47.65.192/27,101.47.65.32/27`.

      For more information on the CIDR block of DTS servers, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

   * When the database instance’s access method is VPC and access restrictions are enabled, add the subnet segment of the VPC connected by the dedicated line to the database instance’s allowlist or security group before creating the database transmission task. For more information, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

* Network connectivity: Confirm the network connectivity and service availability of the source database and destination before creating a data subscription task.

* You can also prepare the migration objects in the source and target databases according to the instructions in the Pre\-check items. For more information, refer to [Pre-check items (MySQL)](https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_mysql).


<span id=".6ZmQ5Yi26K-05piO"></span>
## Limits


|Limits |Description |
|---|---|
|Source database limits |* Database version: MySQL 5.5, 5.6, 5.7, and 8.0 instances are supported.<br><br>* When the instance version of the source database is greater than or equal to 5.6, the parameter `gtid_mode` is set to `ON`.<br><br>* When the instance type is **MySQL** and **Access method** is **MySQL connected over public network** (for example, the source database is a third\-party cloud service instance), you need to retain logs for at least 24 hours (e.g., Binlog logs), and it is recommended to keep logs for more than 7 days. Otherwise, DTS may fail due to unavailable logs, which may also cause data loss in some cases. |
|Consumer restrictions |* The following restrictions apply when messages are subscribed to built\-in middleware:<br><br>   * Messages exceeding 10MB per single message will be discarded when subscribed.<br><br>      * When messages are subscribed to built\-in middleware, the default Topic contains only one Partition, ensuring message delivery order. For higher traffic delivery, choose to subscribe data to customer owned middleware.<br><br>* The following restrictions apply when messages are subscribed to Kafka:<br><br>   * After a subscription task is successfully created, it is not supported to modify the reception policy for Kafka Partition.<br><br>   * If the consumer is Kafka connected over express network or Message Queue for Kafka, do not modify the number of Partitions after creating the subscription task.<br><br>   * Only SASL authentication with the PLAIN mechanism is supported. Specify the username for the PLAIN mechanism here. For how to create a SASL user with the PLAIN mechanism, refer to [Creating a SASL user](https://docs.byteplus.com/en/docs/kafka/creating-SASLuser). |
|Other limits |* When selecting **Subscription data delivery**, the built\-in middleware is shared by all users and is only applicable to test scenarios; in business scenarios, it is recommended to select Customer owned middleware.<br><br>* Currently, only the **Standard** link specification is supported when creating a data subscription task. For details about the link specification, refer to [Product specification](https://docs.byteplus.com/en/docs/DTS/product_specifications).<br><br>* When the **Subscription format** selects **Debezium JSON format**, it does not support selecting **Database table structure subscription** for **Subscription type**.<br><br>* **Incremental subscription** is supported when **Built\-in middleware** is selected for **Subscription data delivery**.<br><br>* If subscribing messages to customer owned middleware, do not modify the parameter configuration of the owned middleware instance during the data subscription process, or the task will fail.<br><br>* **Avro format** for subscription is currently in beta testing. To use it, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support.<br><br>* Do not perform frequent DDL operations on the same table, as repeated DDL operations may cause DTS metadata update failures and risk transmission interruptions. The mitigation measures are as follows:<br><br>   * Method 1: in the console, DDL operations should be performed at intervals of at least 1–3 seconds.<br><br>   * Method 2: perform DDL operations using [lock-free schema change tickets](https://docs.byteplus.com/en/docs/DBW/creating-a-lock-free-structural-change-ticket-onlineddl-ticket-for-mysql) or [lock-free data change tickets](https://docs.byteplus.com/en/docs/DBW/creating-a-lock-free-sql-change-ticket-for-mysql) of Database Workshop (DBW). |


<span id=".5pSv5oyB55qELXNxbC3or63lj6U="></span>
## Supported SQL statements

The supported SQL operations for incremental subscription are shown in the following table.


|**Operation type** |**SQL operation statements** |
|---|---|
|**DML** |INSERT, UPDATE, DELETE |
|**DDL** |ALTER TABLE, CREATE TABLE, DROP TABLE, RENAME TABLE, TRUNCATE TABLE |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, click **Data subscription**.

4. On the **Data subscription list** page, click **Create subscription**.

5. On the **Configure source database** page, configure the following parameters.

   
   |**Type** |**Name** |||**Description** |
   |---|---|---|---|---|
   |**Basic information** |**Task name** |||Optional. Customize the task name. The length must be within 256 characters.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If not set, the system generates a task name by default according to the naming rule, starting with <code>dts-</code>.</div><br> |
   ||**Link specification** |||Select the link specification for the subscription task. Currently only **Standard** is supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For details about the link specification, refer to <a href="https://docs.byteplus.com/en/docs/DTS/product_specifications">Product specification</a>.</div><br> |
   |**Basic configuration** |**Select an existing data source** |||You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |||Select **MySQL**. |
   ||**Access method** |||Select **BytePlus veDB for MySQL**. |
   ||**Region** |||Select the region where the target instance is located. |
   ||**Cross\-BytePlus account?**  |||Select whether to transmit data cross\-account as needed, with the following options:<br><br><br>* **This account**: Selecting this means data transmission occurs only within this account.<br><br>* **Cross\-account**: Selecting this means data transmission occurs between two accounts.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When transmitting data across accounts, log on to the Database Transmission Service (DTS) console through the account of the destination.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Before cross\-account data transmission, create and authorize an IAM role in the source root user. For detailed steps, refer to <a href="https://docs.byteplus.com/en/docs/DTS/How_to_authorize_users_for_cross-account_data_transmission">How to authorize users for cross\-account data transmission</a>.   </div><br>    |
   ||<div style="text-align: center"><br><strong>Cross\-account ID</strong></div><br> |||Enter the BytePlus account ID to which the source database belongs. |
   ||<div style="text-align: center"><br><strong>Cross\-account roles</strong></div><br> |||Enter the IAM role authorized for DTS to access cross\-account resources. |
   ||**MySQL instance** |||Select the target instance of BytePlus veDB for MySQL from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The drop\-down list only shows the first 10 instances. You can also search for the target instance by instance ID or name.</div><br> |
   ||**Node type** |||Select node types as needed, currently supporting **Primary node** and **Read\-only node**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Select read\-only nodes when read\-only nodes are created within the instance. For specific steps on creating a read\-only node, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/overview_of_read-only_nodes">Read\-only node overview</a>.</div><br> |
   ||**MySQL read\-only node** |||Select the target read\-only node from the drop\-down list.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When a read\-only node is created in the instance and <strong>Node type</strong> selects <strong>Read\-only node</strong>, this parameter can be configured.</div><br> |
   ||**Database account** |||Enter the database account of the target instance. |
   ||**Database password** |||Enter the password corresponding to the database account of the target instance. |
   ||**Test connection** |||Click **Test connection** to verify the connection to the instance.<br><br>If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
   |**Middleware configuration** |**Select an existing data source** |||You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Subscription built\-in middleware**<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Subscription built\-in middleware is only applicable to test scenarios.</div><br> |**VPC** ||Select the target VPC from the drop\-down list. |
   |||**Subnet** ||Select the subnet within the target VPC from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The subnet in the target VPC must have at least one available IP.</div><br> |
   ||**Customer owned middleware**<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For business scenarios, it is recommended to select self\-owned middleware.</div><br> |**Message Queue for Kafka** |**Kafka instance** |Select the target instance from the drop\-down list. |
   ||||**Topic** |Select the target Topic information from the drop\-down list. |
   ||||**Kafka user** |Enter the Kafka username.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only SASL authentication with the PLAIN mechanism is supported. Specify the username for the PLAIN mechanism here.</div><br> |
   ||||**Password** |Enter the Kafka user's password. |
   |||**Kafka connected over express network** |**Broker** |Enter the IP address and port number of all Brokers, formatted as `host1:port1`, for example `10.1.1.1:9093`. If there are multiple Brokers, separate them with commas (,). |
   ||||**Topic** |Enter the target Topic information. |
   ||||**VPC** |Select the target VPC from the drop\-down list as follows:<br><br><br>* Direct connect: Select any VPC under the CEN when achieving data connectivity through a dedicated line CEN.<br><br>* VPN connection: Select the VPC bound to the VPN gateway when achieving data connectivity through VPN. |
   ||||**Subnet** |Select a subnet within the VPC from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When subscribing to a Kafka instance connected over express network, you need to add subnet CIDR block access permissions in the allowlist or security group policy on the source end in advance. Click <strong>View subnet CIDR blocks</strong> to view and copy CIDR blocks.</div><br> |
   ||||**Kafka user** |Enter the Kafka username.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only SASL authentication with the PLAIN mechanism is supported. Specify the username for the PLAIN mechanism here.</div><br> |
   ||||**Password** |Enter the Kafka user's password. |
   |||**Test connection** ||If the test connection fails, modify the configuration based on the failure prompt, then test to verify if the instance connects successfully. The details are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct.** <br><br>   * When subscribing to messages in Kafka connected over express network or Message Queue for Kafka, this error prompt requires verification of the username and password accuracy.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical staff.<br><br>* **Invalid IP address**: When this error prompt appears, verify the accuracy of the IP address.<br><br>* **Connection authentication failed, check if the network is normal**: This error prompt appears only when subscribing to messages in Kafka connected over express network. When this error prompt appears, verify network connectivity.<br><br>* **The VPC requires the subnet to have \* available IPs. The current number of available IPs in the subnet is insufficient, and the task can not be created. Check the subnet resources in the VPC**: This error message will only appear when you subscribe to a Kafka connected over express network. When this error occurs, adjust the number of available IPs in the VPC subnet to ensure enough IPs are available within the target VPC subnet. |
   |**Project and billing** |**Project** |||Optional. Select the affiliated project for the task from the drop\-down list. By default, it is under **default (default project)** . You can also click **Create new project** to create a new project. For more information, refer to [Creating a new project](https://docs.byteplus.com/en/docs/6649/94336).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To grant sub\-user privileges to access resources in a specific project, refer to <a href="https://docs.byteplus.com/en/docs/6649/173422">Modifying project privileges</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After a task is created successfully, if you need to change its affiliated project, you can move the resource to another project. For more information, refer to <a href="https://docs.byteplus.com/en/docs/6649/94337">Moving resources to a project</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources.</div><br> |
   ||**Tag** |||Optional. Click **Add tag** to set the tag key and tag value to add a tag to the instance. The rules for tag key\-value pairs are as follows:<br><br><br>* Key<br><br>   * Supports any language, characters, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 1 to 128 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br>   * Keys cannot start with any form of `volc:`, such as `Volc:` or `VOLC:`.<br><br>* (Optional) Value<br><br>   * Supports any language, character, digit, space, or symbol (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 0 to 256 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">A tag consists of a key\-value object that identifies cloud resources. It can help you classify cloud resources with the same characteristics (such as use, owner, or environment) for easy filtering and aggregation, so that you can easily manage the cloud resources. For more details about tags, refer to <a href="https://docs.byteplus.com/en/docs/6649/189377">Tag overview</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Supports fuzzy search for selecting existing tag keys and tag values.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Tags help you categorize cloud resources, control access to cloud resources, and manage billing and cost allocation.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A maximum of 20 tags can be associated with a task in a single operation. A maximum of 50 tags can be associated with a single task.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For a single resource, tag keys must be unique, and each tag key can have only one value.</div><br> |
   ||**Billing type** |||Select a billing method: **Pay\-as\-you\-go** or **Subscription**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For detailed billing information, refer to <a href="https://docs.byteplus.com/en/docs/DTS/billing_overview">Billing instructions</a>.</div><br> |
   ||**Subscription duration** |||Select the duration of the subscription as needed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When selecting <strong>Subscription</strong> in <strong>Billing method</strong>, you can set the purchase time and also check <strong>Automatic renewal</strong>. The system automatically renews before task expiration.</div><br> |
   

6. Click **Next: configure subscription object**.

7. On the **Configure subscription object** page, configure the following parameters.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you do not need to start the subscription task immediately, click <strong>Save </strong>at the bottom right of the page after completing the subscription object configuration. Saving means the subscription task is created successfully but not started.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After saving, the task status will be <strong>To be started</strong>. When you need to start this task, on the <strong>Data subscription list</strong> page, click <strong>Configure subscription channel</strong> under the <strong>Actions</strong> column for the subscription task that has not yet started. For steps, refer to step 5 and the following steps.   </div>
   

   
   |**Name** ||**Description** |
   |---|---|---|
   |**Basic information** |**Subscription format** |Select data subscription format. Subscription formats support **BytePlus Proto**, **Canal Proto**, **Canal JSON**, **Avro format**, and **Debezium JSON format**. For details on subscription formats, refer to [Data subscription format](https://docs.byteplus.com/en/docs/DTS/data_subscription_format).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>Avro format</strong> and <strong>Debezium JSON format</strong> are currently in beta testing. To use it, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> for technical support.</div><br> |
   ||**Kafka Partition policy** |Select the reception policy for the target Topic Partition as needed. The following reception policies are supported:<br><br><br>* Deliver unified to Partition 0<br><br>* Deliver to different Partitions based on the combined hash value of the database name and the table name<br><br>* Deliver to different Partitions based on the hash value of the primary key<br><br>* Deliver to different Partitions based on the hash value of the specified column<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When the access method selects <strong>Kafka connected over express network</strong> or <strong>Message Queue for Kafka</strong>, this parameter can be configured.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">After the subscription task starts, the following actions are not supported:</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Modify the reception strategy of the Kafka Partition in the DTS console.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Modify the number of Partitions in Kafka.</div><br> |
   ||**Subscription type** |Select subscription types as needed. Current support includes **Database table structure subscription**, **Incremental subscription**, and **Full subscription**. including:<br><br><br>* When **Subscription data delivery** selects **Subscription built\-in middleware**, only the **Incremental subscription** can be selected in the **Subscription type**.<br><br>* When the **Subscription format** selects **Debezium JSON format**, it does not support selecting **Database table structure subscription** for **Subscription type**. |
   ||**Starling timestamp** |Set to pull Binlog logs from a specified position or timestamp. The values are as follows:<br><br><br>* **System default**: The default is the task start time.<br><br>* **Specify GTID**: Enter the specified GTID in the input box, formatted as `source_id:transaction_id`.<br><br>* **Specify GTID**_**EXECUTED**: Enter the specified GTID_EXECUTED in the input box, formatted as `source_id:transaction_id`. If multiple exist, separate them with commas (,).<br><br>* **Specify timestamp**: Click the input box to select a date, click **Select time** to set the time point, then click **OK**.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the <strong>Subscription type</strong> is selected <strong>Incremental subscription</strong>, this configuration is supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When <strong>Subscription type</strong> selects both <strong>Full subscription</strong> and <strong>Incremental subscription</strong>, the <strong>Starting timestamp</strong> defaults to the current time point and can not be modified.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">GTID and GTID_EXECUTED must be legal values from the source end. Otherwise, pre\-check reports an error.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When selecting <strong>Specify timestamp</strong>, the time you set must be later than the earliest Binlog time on the source end. If there is no corresponding time Binlog, the closest Binlog starting point will be selected.</div><br> |
   ||**Subscription scope** |Select subscription scope as needed, currently supporting `Insert`, `Update`, `Delete`, and DDL.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the <strong>Subscription type</strong> is selected <strong>Incremental subscription</strong>, this configuration is supported.</div><br> |
   ||**Subscription object** |Select the objects to subscribe in the **Subscription object** area. You can query target objects via **Normal search** or **Global search**. After selecting the target subscription object, confirm the subscription objects again in the **Selected object** box on the right. Meanwhile, if the entire database is checked in the **Subscription object** area, expanding the database is not supported in the **selected object** area.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Regular expression search for target objects is supported in the <strong>Subscription object</strong> or <strong>Selected object</strong> areas.</div><br> |
   |**Advanced configuration** |**Selected databases and tables** |Supports reconfiguring the selected databases and tables individually. The specific configuration is as follows:<br><br><br>* **Full subscription**: When the subscription format selects full subscription, it supports selecting or canceling full subscription of target tables as needed.<br><br>* **Incremental subscription**: When the subscription format selects incremental subscription, it supports selecting or canceling incremental subscription of target tables as needed.<br><br>* **Topic**: You can set the target Topic for delivering a single table from the drop\-down list as needed. Meanwhile, DTS supports batch modification of the Topic name of all target tables to quickly achieve flexible routing and isolation of data. The detailed operations are as follows:<br><br>   1. Click the **Batch** button after Topic.<br><br>   2. Configure the following parameter information in the **Batch set Topic** dialog:<br><br>      * **Select scope**: select the range of tables to apply as needed, supporting modifying based on the current Topic name or modifying based on the table name.<br><br>      * **Select object**: select the specific operation object.<br><br>      * **Rule settings**: supports the following three batch modification modes:<br><br>         * **Add prefix and suffix to name**: add specified characters before or after the current line's topic name or table name.<br><br>         * **Unified renaming**: Replace the selected Topic names uniformly with the specified new name.<br><br>         * **Uniformly reduce in the name**: Batch remove specified characters from the selected Topic names.<br><br>   3. Click **Apply**, and DTS will automatically update the corresponding target Topics according to the set rules.<br><br><br>When **Middleware configuration** **Access method** selects **Message Queue for Kafka** or **Kafka connected over express network**, this configuration is supported. Also, when using batch modification of Topic names (such as adding prefixes and suffixes, unified renaming), ensure the modified Topic names already exist in Kafka.<br><br><br>* **Specify the columns to compute the hash value**: Enter the column name used to compute the hash value. After that, the data will be delivered to the specified Partition or queue according to the hash value of this column. The system supports batch selection of columns for hash value computation across all databases and tables. This configuration is supported when the delivery policy selects **Deliver to different Partitions based on the hash value of the specified column** or **Deliver to different queues based on the hash value of the specified column**. |
   ||**Database & table automatic delivery rules** |**Database & table automatic delivery rules** refer to the process where table data from a database is delivered to a Topic via DTS. It supports automatically matching table names using regular expressions based on the database name or table name, and then automatically delivering the data of the matched tables to the corresponding Topic.<br><br>Select whether to enable **Database & table automatic delivery rules**.<br><br><br>* Enable **Database & table automatic delivery rules**.<br><br>   1. After enabling **Database & table automatic delivery rules**, click **Add a row** in the database & table matching rules list.<br><br>   2. In the database & table matching rules input box, enter a regular expression in the format of `DBRegex\.TableRegex`.<br><br>   3. Select the target Topic from the drop\-down list. Data from table names matching this regular expression will be delivered to the target Topic.<br><br>* Disable **Database & table automatic delivery rules**. DTS does not enable **Database & table automatic delivery rules** by default.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Up to 10 database & table matching rules can be configured for a subscription task.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The smaller the priority value, the higher the priority. Drag rules with the mouse to adjust their priority up or down.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Message delivery Topic priority: Database & table automatic delivery rules \> Custom database & table delivery Topic \> Default Topic specified when creating the subscription task.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The following conditions must be met to configure this parameter:</div><br><br><br>   * <div data-tips="true" data-tips-type="default">The <strong>Instance type</strong> of the source database is RDS for MySQL.</div><br><br><br>   * <div data-tips="true" data-tips-type="default"><strong>Subscription data delivery</strong> selects <strong>Customer owned middleware</strong>, and <strong>Access method</strong> selects <strong>Message Queue for Kafka</strong> or <strong>Kafka connected over express network</strong>.</div><br> |
   ||**Enable ETL configuration** |1. Choose whether to enable the ETL function.<br><br>   * **Yes**: indicates enabling ETL functions.<br><br>      * After enabling ETL rules, click **Quick configuration field mapping/filtering rules**, configure synchronization objects in the **Quick configuration field mapping/filtering rules** dialog box, and click **OK** to quickly generate ETL statements.<br><br>      * After enabling the ETL function, refer to [DSL syntax](https://docs.byteplus.com/en/docs/DTS/dsl_syntax) to configure data processing rules in **Code goes here...**  Enter the data processing ETL rules, i.e., the DSL script, in the input box, and click **Verification** to verify whether the data processing statements are correct.<br><br>      * You can also click **Debug** to test the effects of the ETL rules you created. For details on debugging, refer to [Verifying ETL rules through ETL Playground tool](https://docs.byteplus.com/en/docs/DTS/debugging-ETL-rules-with-ETL-Playground-tool).<br><br>   * **No**: indicates not enabling ETL functions.<br><br>2. Choose whether to quickly configure the filtering of DML generated by OnlineDDL as needed. If configuration is needed, click **Quickly configure DML generated by OnlineDDL**.<br><br>   1. When the OnlineDDL tool is `gh-ost`, filter temporary tables `_tableName_ghc`, `_tablename_gho`, `_tablename_del` to the target database.<br><br>   2. When the OnlineDDL tool is `pt-osc`, filter temporary tables `_tablename_new`, `_tablename_old` to the target database.<br><br>   3. You need to confirm that no tables in the synchronization list match the temporary table command method. |
   ||**Error retry time** |If the source database or target database disconnects, the subscription task automatically recovers if reconnection occurs within that time. Value range: 600–86400, in seconds (s). The default value is 600 seconds. |
   ||**Subscription Begin/Commit** |Set whether to subscribe to messages by transaction as needed to ensure message consistency and completeness.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The following conditions must be met to configure this parameter:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Subscription format</strong> selects <strong>BytePlus Proto</strong>, <strong>Canal Proto</strong>, <strong>Canal JSON</strong> or <strong>Avro</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Subscription data delivery</strong> selects <strong>Subscription built\-in middleware</strong>, <strong>Subscription data delivery</strong> selects <strong>Customer owned middleware</strong>, and <strong>Access method</strong> selects <strong>Message Queue for Kafka</strong> or <strong>Kafka connected over express network</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When selecting <strong>Message Queue for Kafka or Kafka connected over express network</strong> as the <strong>Access method</strong>, choose the <strong>Kafka Partition policy</strong> to <strong>uniformly deliver to Partition 0</strong>.</div><br> |
   ||**Subscribe to all fields**<br><br> |Set whether to subscribe to all fields as needed. In Canal JSON format Update messages, the complete before\-image information is subscribed to by default. If you only need to subscribe to the before\-image of the changed column, you can configure it through this parameter.<br><br><br>* **Yes**: The default value, indicating that you are subscribing to the full before\-image of the row containing the updated field in the UPDATE statement.<br><br>* **No**: indicates that only the before\-image of the updated field in the UPDATE statement is subscribed.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter can be configured only when the <strong>Instance type</strong> is <strong>MySQL</strong>, the middleware access method is <strong>Message Queue for Kafka</strong> or <strong>Kafka connected over express network</strong>, and the <strong>Subscription format</strong> is <strong>Canal JSON</strong>.</div><br> |
   ||**Disable scientific notation** |Select the numeric type when writing MySQL data to Kafka as needed. When selected, FLOAT and DOUBLE types will convert to regular numeric format instead of scientific notation.<br><br><br>* This parameter supports configuration only when the **Instance type** is **MySQL**, middleware Access method is Kafka connected over express network, Message queue Kafka version**Kafka connected over express network**, Message queue Kafka version or **Message queue RocketMQ version**, and subscription mode includes either full subscription or incremental subscription.<br><br>* This method changes the output format of subscription data; configure carefully according to downstream requirements. |
   ||**Time zone configuration** |This parameter specifies the output time zone for the timestamp type in data subscription (default is UTC). If the downstream requires parsing by local time zone or alignment with business time, select the corresponding time zone as needed.<br><br>This parameter supports configuration only when the **Instance type** is **MySQL**, the middleware access method is **Message queue Kafka version**, **Kafka connected over express network**, or **Message queue RocketMQ version**, and the subscription method includes at least one of full subscription or incremental subscription. |
   



&nbsp;

8. Click **Pre\-check**.

9. Optional. If a pre\-check has been performed for the created task, you can confirm whether to restart the pre\-check based on the prompts. If you need to restart, click **OK** in the **Whether to restart the pre\-check** dialog box.

   * If the instances of the source and target databases are not modified, there is no need to restart the pre\-check.

   * If you modify the source and target database instance information or the subscription task parameters, it is recommended to restart the pre\-check to avoid task startup failures or interruptions.

10. On the **Pre\-check** configuration wizard page, perform the following actions based on the check result:

   * Click **Details** in the **Actions** column to view detailed alert and failure messages. After modifying the databases and tables accordingly, click **Retry**.

   * Click **Ignore** in the **Actions** column to ignore the alert and continue starting the subscription task. You can also click **Ignore all** to ignore all alert messages with one click.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Do not ignore the alert when the pre\-check results have failed.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">After selecting <strong>Ignore</strong> alert and starting the subscription task, certain risks may exist. For more information, refer to the prompt on the interface.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For details about the pre\-check, refer to <a href="https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_mysql">Pre\-check items (RDS for MySQL)</a>.      </div>
      

11. At the bottom\-right of the **Pre\-check** page, click **Confirm order**.

12. Select the configuration method according to the billing method of the task creation:

   * Pay\-as\-you\-go

      On the **Confirm order** configuration wizard page, confirm the configuration information again. Read the Service\-Specific Terms for BytePlus Database Products and Services and check **I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**, and click **Create and start a task**.

   * Subscription

      1. On the **Confirm order** configuration wizard page, confirm the configuration information again. Read the Service\-Specific Terms for BytePlus Database Products and Services and check **I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**, and click **Create and start a task**.

      2. On the **Confirm billing information** configuration wizard page, verify the instance’s billing information.

      3. Optional. Click **Voucher redemption**. In the **Voucher redemption** dialog box, enter the voucher code and click **Redeem**.

      4. Optional. In the voucher area, select an available voucher as needed. Only one voucher can be selected at a time to offset part of the cost. You can also choose not to use a voucher.

      5. Click **Next step**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Once the <strong>Payment is completed</strong> on the configuration wizard page, a <strong>Successful payment</strong> message means your task has been created.      </div>
      

After successfully creating the data subscription task, you can view the data subscription task in the subscription task list on the DTS console.

<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations


1. [Creating a consumer group](https://docs.byteplus.com/en/docs/DTS/adding_a_consumer_group)

2. Consuming subscription data

   * [Consuming BytePlus Proto subscription data via Kafka](https://docs.byteplus.com/en/docs/DTS/Consuming_Proto_subscription_data_via_Kafka)

   * [Consuming Canal Proto subscription data via RocketMQ](https://docs.byteplus.com/en/docs/DTS/Consuming_Canal_Proto_subscription_data_via_RocketMQ)


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[CreateTransmissionTask](https://docs.byteplus.com/en/docs/DTS/CreateTransmissionTask) |Call the CreateTransmissionTask API to create a DTS task. |
|[ModifyTransmissionTask](https://docs.byteplus.com/en/docs/DTS/modifytransmissiontask) |Call the ModifyTransmissionTask API to modify the transmission task. |
