---
title: "Creating a data subscription task for PostgreSQL connected over public network"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/creating_public_network_data_subscription_task_postgresql"
---

This topic introduces how to create a public network PostgreSQL data subscription task through Database Transmission Service (DTS).

## Prerequisites

* An RDS for PostgreSQL database has been set up independently and is accessible via the public network.

* If consuming data through the Kafka connected over express network, configure the consumer information as needed, as shown below:

   * When using VPN to achieve data subscription, the local network of the self\-managed database has been connected to the BytePlus via VPN gateway. For detailed steps, refer to [Building a cloud VPC and on-premises multi-data-center network interconnection](https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-multiple-data-centers).

   * If data subscription requires a dedicated line connection, you need to establish a dedicated line connection between a single cloud VPC and a single on\-premises data center network. For more information, refer to [Configuring direct connections](https://docs.byteplus.com/en/docs/directconnect/Quick-start#.6YWN572u5LiT57q_6L-e5o6l).

## Preparation before subscription

* Allowlist and access permissions:

* When the access method of the database instance is self\-managed over the Internet and access restrictions are enabled, add the DTS server IP addresses to the allowlist or security group of the database instance before creating the database transmission task. DTS server IP addresses vary by region, as detailed below:

   * DTS server IP addresses in China (Guangzhou), China (Shanghai), and China (Beijing) are `221.194.189.0/27,157.148.90.32/27,180.184.132.64/27,61.129.54.64/27,220.196.172.32/27,117.135.143.32/27,220.196.168.32/27,116.132.250.32/27,111.45.13.32/27,125.88.248.32/27,180.153.35.32/27,220.181.65.32/27,220.181.65.64/27`.

   * DTS server IP addresses in Asia Pacific (Johor) are `101.47.0.32/27,220.181.65.32/27,220.181.65.64/27,101.47.65.192/27,101.47.65.32/27`.

   * DTS server IP addresses in Asia Pacific (Jakarta) are `221.194.189.0/27,157.148.90.32/27`.

   * DTS server IP addresses in China (Hong Kong) are `101.47.0.32/27,220.181.65.32/27,220.181.65.64/27,101.47.65.192/27,101.47.65.32/27`.

      For more information on the CIDR block of DTS servers, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

   * When the database instance’s access method is VPC and access restrictions are enabled, add the subnet CIDR blocks to the database instance’s allowlist or security group before creating the database transmission task. The subnet CIDR block for China (Guangzhou) is `172.31.0.0/20`, while the subnet CIDR blocks for China (Shanghai) and China (Beijing) are `192.168.3.0/24`. The subnet CIDR block for Asia Pacific (Johor) is `192.168.0.0/24`. For more information, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

* Network connectivity: Confirm the network connectivity and service availability of the source database and destination before creating a data subscription task.

* You can also prepare the migration objects in the source and target databases according to the instructions in the Pre\-check items. For more information, refer to [Pre-check items (PostgreSQL)](https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_postgresql).

## Limits

|Limits |Description |
|---|---|
|Source database limits |Database version: RDS for PostgreSQL 10, 11, 12, 13, 14, 15, 16, and 17 instances are supported. |
|Consumer restrictions |* The following restrictions apply when messages are subscribed to built\-in middleware:<br><br>   * Messages exceeding 10MB per single message will be discarded when subscribed.<br><br>      * When messages are subscribed to built\-in middleware, the default Topic contains only one Partition, ensuring message delivery order. For higher traffic delivery, choose to subscribe data to customer owned middleware.<br><br>* The following restrictions apply when messages are subscribed to Kafka:<br><br>   * After a subscription task is successfully created, it is not supported to modify the reception policy for Kafka Partition.<br><br>   * If the consumer is Kafka connected over express network or Message Queue for Kafka, do not modify the number of Partitions after creating the subscription task.<br><br>   * Only SASL authentication with the PLAIN mechanism is supported. Specify the username for the PLAIN mechanism here. For how to create a SASL user with the PLAIN mechanism, refer to [Creating a SASL user](https://docs.byteplus.com/en/docs/kafka/creating-SASLuser). |
|Other limits |* When selecting **Subscription data delivery**, the built\-in middleware is shared by all users and is only applicable to test scenarios; in business scenarios, it is recommended to select Customer owned middleware.<br><br>* Currently, only the **Standard** link specification is supported when creating a data subscription task. For details about the link specification, refer to [Product specification](https://docs.byteplus.com/en/docs/DTS/product_specifications).<br><br>* If subscribing messages to customer owned middleware, do not modify the parameter configuration of the owned middleware instance during the data subscription process, or the task will fail.<br><br>* **Avro format** for subscription is currently in beta testing. To use it, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support.<br><br>* For RDS for PostgreSQL synchronization tasks, the source database account must create triggers, functions, and other objects in the source database. Therefore, during the synchronization process, do not modify the access permissions of objects such as triggers, functions, or internal tables created by this account in the source database. |

## Supported SQL statements

|**Operation type** |**SQL statement** |
|---|---|
|DML |INSERT, UPDATE, DELETE |
|DDL |CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE, CREAT INDEX, DROP INDEX, CREATE SEQUENCE, ALTER SEQUENCE, DROP SEQUENCE, DROP RULE |

## Procedure

1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, click **Data subscription**.

4. On the **Data subscription list** page, click **Create subscription**.

5. On the **Configure source database** page, configure the following parameters.

   |**Type** |**Name** |||**Description** |
   |---|---|---|---|---|
   |**Basic information** |**Task name** |||Optional. Customize the task name. The length must be within 256 characters.<br><br>> **tip**<br><br><br>> If not set, the system generates a task name by default according to the naming rule, starting with `dts-`.<br> |
   ||**Link specification** |||Select the link specification for the subscription task. Currently only **Standard** is supported.<br><br>> **tip**<br><br><br>> For details about the link specification, refer to [Product specification](https://docs.byteplus.com/en/docs/DTS/product_specifications).<br> |
   |**Basic configuration** |**Select an existing data source** |||You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |||Select **PostgreSQL**. |
   ||**Access method** |||select **PostgreSQL connected over public network**. |
   ||**PostgreSQL instance** |||Select the target instance from the drop\-down list. |
   ||**Database account** |||Enter the database account information. |
   ||**Database password** |||Enter the database password. |
   ||**Test connection** |||If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check the network**: When this error prompt appears, confirm network connectivity.<br><br>* **Connection authentication failed. Check the username and password**: When this error prompt appears, verify your username and password.<br><br>* **Invalid IP address**: When this error prompt appears, verify the accuracy of the IP address. |
   |**Middleware configuration** |**Select an existing data source** |||You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Subscription built\-in middleware**<br><br>> **tip**<br><br><br>> Subscription built\-in middleware is only applicable to test scenarios.<br> |**VPC** ||Select the target VPC from the drop\-down list. |
   |||**Subnet** ||Select the subnet within the target VPC from the drop\-down list.<br><br>> **tip**<br><br><br>> The subnet in the target VPC must have at least one available IP.<br> |
   ||**Customer owned middleware**<br><br>> **tip**<br><br><br>> For business scenarios, it is recommended to select self\-owned middleware.<br> |**Message Queue for Kafka** |**Kafka instance** |Select the target instance from the drop\-down list. |
   ||||**Topic** |Select the target Topic information from the drop\-down list. |
   ||||**Kafka user** |Enter the Kafka username.<br><br>> **tip**<br><br><br>> Only SASL authentication with the PLAIN mechanism is supported. Specify the username for the PLAIN mechanism here.<br> |
   ||||**Password** |Enter the Kafka user's password. |
   |||**Kafka connected over express network** |**Broker** |Enter the IP address and port number of all Brokers, formatted as `host1:port1`, for example `10.1.1.1:9093`. If there are multiple Brokers, separate them with commas (,). |
   ||||**Topic** |Enter the target Topic information. |
   ||||**VPC** |Select the target VPC from the drop\-down list as follows:<br><br><br>* Direct connect: Select any VPC under the CEN when achieving data connectivity through a dedicated line CEN.<br><br>* VPN connection: Select the VPC bound to the VPN gateway when achieving data connectivity through VPN. |
   ||||**Subnet** |Select a subnet within the VPC from the drop\-down list.<br><br>> **tip**<br><br><br>> When subscribing to a Kafka instance connected over express network, you need to add subnet CIDR block access permissions in the allowlist or security group policy on the source end in advance. Click **View subnet CIDR blocks** to view and copy CIDR blocks.<br> |
   ||||**Kafka user** |Enter the Kafka username.<br><br>> **tip**<br><br><br>> Only SASL authentication with the PLAIN mechanism is supported. Specify the username for the PLAIN mechanism here.<br> |
   ||||**Password** |Enter the Kafka user's password. |
   |||**Test connection** ||If the test connection fails, modify the configuration based on the failure prompt, then test to verify if the instance connects successfully. The details are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct.** <br><br>   * When subscribing to messages in Kafka connected over express network or Message Queue for Kafka, this error prompt requires verification of the username and password accuracy.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical staff.<br><br>* **Invalid IP address**: When this error prompt appears, verify the accuracy of the IP address.<br><br>* **Connection authentication failed, check if the network is normal**: This error prompt appears only when subscribing to messages in Kafka connected over express network. When this error prompt appears, verify network connectivity.<br><br>* **The VPC requires the subnet to have \* available IPs. The current number of available IPs in the subnet is insufficient, and the task can not be created. Check the subnet resources in the VPC**: This error message will only appear when you subscribe to a Kafka connected over express network. When this error occurs, adjust the number of available IPs in the VPC subnet to ensure enough IPs are available within the target VPC subnet. |
   |**Project and billing** |**Project** |||Optional. Select the affiliated project for the task from the drop\-down list. By default, it is under **default (default project)** . You can also click **Create new project** to create a new project. For more information, refer to [Creating a new project](https://docs.byteplus.com/en/docs/6649/94336#%E6%96%B0%E5%BB%BA%E9%A1%B9%E7%9B%AE).<br><br>Description<br><br><br>* To grant sub\-user privileges to access resources in a specific project, refer to [Modifying project privileges](https://docs.byteplus.com/en/docs/6649/173422#%E4%BF%AE%E6%94%B9%E9%A1%B9%E7%9B%AE%E6%9D%83%E9%99%90).<br><br>* After a task is created successfully, if you need to change its affiliated project, you can move the resource to another project. For more information, refer to [Moving resources to a project](https://docs.byteplus.com/en/docs/6649/94337).<br><br>* A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources. |
   ||**Tag** |||Optional. Click **Add tag** to set the tag key and tag value to add a tag to the instance. The rules for tag key\-value pairs are as follows:<br><br><br>* Key<br><br>   * Supports any language, characters, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 1 to 128 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br>   * Keys cannot start with any form of `volc:`, such as `Volc:` or `VOLC:`.<br><br>* (Optional) Value<br><br>   * Supports any language, character, digit, space, or symbol (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 0 to 256 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br><br>> **tip**<br><br><br><br>* > A tag consists of a key\-value object that identifies cloud resources. It can help you classify cloud resources with the same characteristics (such as use, owner, or environment) for easy filtering and aggregation, so that you can easily manage the cloud resources. For more details about tags, refer to [Tag overview](https://docs.byteplus.com/en/docs/6649/189377).<br><br><br>* > Supports fuzzy search for selecting existing tag keys and tag values.<br><br><br>* > Tags help you categorize cloud resources, control access to cloud resources, and manage billing and cost allocation.<br><br><br>* > A maximum of 20 tags can be associated with a task in a single operation. A maximum of 50 tags can be associated with a single task.<br><br><br>* > For a single resource, tag keys must be unique, and each tag key can have only one value.<br> |
   ||**Billing type** |||Select a billing method: **Pay\-as\-you\-go** or **Subscription**.<br><br>> **tip**<br><br><br>> For detailed billing information, refer to [Billing instructions](https://docs.byteplus.com/en/docs/DTS/billing_overview).<br> |
   ||**Subscription duration** |||Select the duration of the subscription as needed.<br><br>> **tip**<br><br><br>> When selecting **Subscription** in **Billing method**, you can set the purchase time and also check **Automatic renewal**. The system automatically renews before task expiration.<br> |

1. Click **Next: Configure subscription object**.

2. On the **Configure subscription object** page, configure the following parameters.

   > **tip**

   * > If you do not need to start the subscription task immediately, click **Save**at the bottom right of the page after completing the subscription object configuration. Saving means the subscription task is created successfully but not started.

   * > After saving, the task status will be **To be started**. When you need to start this task, on the **Data subscription list** page, click **Configure subscription channel** under the **Actions** column for the subscription task that has not yet started. For steps, refer to step 5 and the following steps

   |**Name** ||**Description** |
   |---|---|---|
   |**Basic information** |**Subscription format** |Select data subscription format. Subscription formats support **BytePlus Proto**, **Canal Proto**, **Canal JSON**, **Avro format**, and **Debezium JSON format**. For details on subscription formats, refer to [Data subscription format](https://docs.byteplus.com/en/docs/DTS/data_subscription_format).<br><br>> **tip**<br><br><br>> **Avro format** and **Debezium JSON format** are currently in beta testing. To use it, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support.<br> |
   ||**Kafka Partition policy** |Select the reception policy for the target Topic Partition as needed. The following reception policies are supported:<br><br><br>* Deliver unified to Partition 0<br><br>* Deliver to different Partitions based on the combined hash value of the database name and the table name<br><br>* Deliver to different Partitions based on the hash value of the primary key<br><br>* Deliver to different Partitions based on the hash value of the specified column<br><br><br>> **warning**<br><br><br><br>* > When the access method selects **Kafka connected over express network** or **Message Queue for Kafka**, this parameter can be configured.<br><br><br>* > After the subscription task starts, the following actions are not supported:<br><br><br>   * > Modify the reception strategy of the Kafka Partition in the DTS console.<br><br><br>   * > Modify the number of Partitions in Kafka.<br> |
   ||**Subscription type** |Currently, only **Incremental subscription** can be selected. |
   ||**Subscription object** |Select the objects to subscribe from the **Subscription object**. After selecting the target subscription object, confirm the subscription objects again in the **Selected object** box on the right. Meanwhile, if the entire database is checked in the **Subscription object** area, expanding the database is not supported in the **selected object** area. |
   |**Advanced configuration** |**Selected databases and tables** |Supports reconfiguring the selected databases and tables individually. The specific configuration is as follows:<br><br><br>* **Topic**: Set the Topic in Kafka where tables are delivered according to the drop\-down list, supporting batch modification of the Topic for all target tables. When **Middleware configuration** **Access method** selects **Message Queue for Kafka** or **Kafka connected over express network**, this configuration is supported.<br><br>* **Specify the columns to compute the hash value**: Enter the column name used to compute the hash value. After that, the data will be delivered to the specified Partition or queue according to the hash value of this column. The system supports batch selection of columns for hash value computation across all databases and tables. This configuration is supported when the delivery policy selects **Deliver to different Partitions based on the hash value of the specified column** or **Deliver to different queues based on the hash value of the specified column**. |
   ||**Database & table automatic delivery rules** |**Database & table automatic delivery rules** refer to the process where table data from a database is delivered to a Topic via DTS. It supports automatically matching table names based on the table name matching rules, and then automatically delivering the data of the matched tables to the corresponding Topic.<br><br>Select whether to enable **Database & table automatic delivery rules**.<br><br><br>* Enable **Database & table automatic delivery rules**.<br><br>   1. After enabling **Database & table automatic delivery rules**, click **Add a row** in the database & table matching rules list.<br><br>   2. In the database & table matching rules input box, enter a regular expression in the format of `DBRegex\.TableRegex`.<br><br>   3. Select the target Topic from the drop\-down list. Data from table names matching this regular expression will be delivered to the target Topic.<br><br>* Disable **Database & table automatic delivery rules**. DTS does not enable **Database & table automatic delivery rules** by default.<br><br><br>> **tip**<br><br><br><br>* > Up to 10 database & table matching rules can be configured for a subscription task.<br><br><br>* > The smaller the priority value, the higher the priority. Drag rules with the mouse to adjust their priority up or down.<br><br><br>* > Message delivery Topic priority: Database & table automatic delivery rules \> Custom database & table delivery Topic \> Default Topic specified when creating the subscription task.<br><br><br>* > The following conditions must be met to configure this parameter:<br><br><br>   * > The **Instance type** of the source database is RDS for PostgreSQL.<br><br><br>   * > **Subscription data delivery** selects **Customer owned middleware**, and **Access method** selects **Message Queue for Kafka** or **Kafka connected over express network**.<br> |
   ||**Error retry time** |If the source database or target database disconnects, the subscription task automatically recovers if reconnection occurs within that time. Value range: 600–86400, in seconds (s). The default value is 600 seconds. |
   ||**Enable millisecond\-level delay monitoring** |Enable or disable millisecond\-level latency monitoring as needed. When enabled, it provides high\-precision, full\-link, proactive end\-to\-end latency measurement, effectively improving monitoring stability and sensitivity to abnormal conditions such as network interruptions and idle disconnections.<br><br>When enabled, DTS writes heartbeat signals to the source database. The source end account must have `SELECT`, `INSERT`, and `UPDATE` permissions. You can also manually create a heartbeat table on the source database to enable millisecond\-level latency monitoring. For detailed steps, see [Manually create a heartbeat table](https://docs.byteplus.com/en/docs/DTS/Why_is_a_heartbeat_table_required_when_enabling_millisecond-level_latency_monitoring?lang=en).<br><br>> **tip**<br><br><br>> This parameter must be configured when consuming data from the RDS for PostgreSQL edition instance through Kafka or RocketMQ.<br> |
   ||**Automatic skip tables without permission**<br><br> |Select whether to automatically skip tables without permission as needed. When encountering tables without sufficient permissions, the system will automatically skip them without interrupting the task. However, data loss may occur, potentially causing business anomalies. It is recommended to configure event alert rules simultaneously. For detailed actions, refer to [Creating event rule](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule). |

1. Click **Pre\-check**.

2. Optional. If a pre\-check has been performed for the created task, you can confirm whether to restart the pre\-check based on the prompts. If you need to restart, click **OK** in the **Whether to restart the pre\-check** dialog box.

   * If the instances of the source and target databases are not modified, there is no need to restart the pre\-check.

   * If you modify the source and target database instance information or the subscription task parameters, it is recommended to restart the pre\-check to avoid task startup failures or interruptions.

10. On the **Pre\-check** configuration wizard page, perform the following actions based on the check result:

   * Click **Details** in the **Actions** column to view detailed alert and failure messages. After modifying the databases and tables accordingly, click **Retry**.

   * Click **Ignore** in the **Actions** column to ignore the alert and continue starting the subscription task. You can also click **Ignore all** to ignore all alert messages with one click.

      > **tip**

      * > Do not ignore the alert when the pre\-check results have failed.

      * > After selecting **Ignore** alert and starting the subscription task, certain risks may exist. For more information, refer to the prompt on the interface.

      * > For details about the pre\-check, refer to [Pre\-check items (PostgreSQL)](https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_postgresql).

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

      > **tip**

      > Once the **Payment is completed** on the configuration wizard page, a **Successful payment** message means your task has been created.

After successfully creating the data subscription task, you can view the data subscription task in the subscription task list on the DTS console.

## Subsequent operations

1. [Creating a consumer group](https://docs.byteplus.com/en/docs/DTS/adding_a_consumer_group)

2. Consuming subscription data

   * [Consuming BytePlus Proto subscription data via Kafka](https://docs.byteplus.com/en/docs/DTS/Consuming_Proto_subscription_data_via_Kafka)

   * [Consuming Canal Proto subscription data via RocketMQ](https://docs.byteplus.com/en/docs/DTS/Consuming_Canal_Proto_subscription_data_via_RocketMQ)

## Related APIs

|**API** |**Description** |
|---|---|
|[CreateTransmissionTask](https://docs.byteplus.com/en/docs/DTS/CreateTransmissionTask) |Call the CreateTransmissionTask API to create a DTS task. |
|[ModifyTransmissionTask](https://docs.byteplus.com/en/docs/DTS/modifytransmissiontask) |Call the ModifyTransmissionTask API to modify the transmission task. |
