---
title: "Creating a subscription task for PostgreSQL connected over express network"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Creating_a_subscription_task_for_PostgreSQL_connected_over_express_network"
---

This topic describes how to create a subscription task for PostgreSQL connected over express network on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Set the source information as needed, as detailed below:

   * When using VPN to perform data migration, the local network where the self\-managed database is located has been connected to BytePlus via VPN gateway. For detailed steps, refer to [Building a cloud VPC and on-premises multi-data-center network interconnection](https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-multiple-data-centers).

   * If data migration requires a dedicated line connection, you need to establish a dedicated line connection between a single cloud VPC and a single on\-premises data center network. For more information, refer to [Configuring direct connections](https://docs.byteplus.com/en/docs/directconnect/Quick-start#.6YWN572u5LiT57q_6L-e5o6l).

* If consuming data through the Kafka connected over express network, configure the consumer information as needed, as shown below:

   * When using VPN to achieve data subscription, the local network of the self\-managed database has been connected to the BytePlus via VPN gateway. For detailed steps, refer to [Building a cloud VPC and on-premises multi-data-center network interconnection](https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-multiple-data-centers).

   * If data subscription requires a dedicated line connection, you need to establish a dedicated line connection between a single cloud VPC and a single on\-premises data center network. For more information, refer to [Configuring direct connections](https://docs.byteplus.com/en/docs/directconnect/Quick-start#.6YWN572u5LiT57q_6L-e5o6l).


<span id=".6K6i6ZiF5YmN5YeG5aSH"></span>
## Preparation before subscription


* When your instance connects via the VPC, the subnet of the VPC must communicate with the source or target database. To allow DTS to access instances in the VPC normally, add the subnet CIDR block to the source or target database allowlist or security group rules. For more information, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

* Confirm the network connectivity and service availability of the source database and destination before creating a data subscription task.

* You can also prepare the migration objects in the source and target databases according to the instructions in the Pre\-check items. For more information, refer to [Pre-check items (PostgreSQL)](https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_postgresql).


<span id="9GIpki4j"></span>
## Limits


|Limits |Description |
|---|---|
|Source database limits |Database version: RDS for PostgreSQL 10, 11, 12, 13, 14, 15, 16, and 17 instances are supported. |
|Consumer restrictions |* The following restrictions apply when messages are subscribed to built\-in middleware:<br><br>   * Messages exceeding 10MB per single message will be discarded when subscribed.<br><br>   * When messages are subscribed to built\-in middleware, the default Topic contains only one Partition, ensuring message delivery order. For higher traffic delivery, choose to subscribe data to customer owned middleware.<br><br>* The following restrictions apply when messages are subscribed to Kafka:<br><br>   * After a subscription task is successfully created, it is not supported to modify the reception policy for Kafka Partition.<br><br>   * If the consumer is Kafka connected over express network or Message Queue for Kafka, do not modify the number of Partitions after creating the subscription task.<br><br>   * Only SASL authentication with the PLAIN mechanism is supported. Specify the username for the PLAIN mechanism here. For how to create a SASL user with the PLAIN mechanism, refer to [Creating a SASL user](https://docs.byteplus.com/en/docs/kafka/creating-SASLuser). |
|Other limits |* When selecting **Subscription data delivery**, the built\-in middleware is shared by all users and is only applicable to test scenarios; in business scenarios, it is recommended to select Customer owned middleware.<br><br>* Currently, only the **Standard** link specification is supported when creating a data subscription task. For details on the link specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/DTS/product_specifications).<br><br>* If subscribing messages to customer owned middleware , do not modify the parameter configuration of the owned middleware instance during the data subscription process, or the task will fail.<br><br>* For RDS for PostgreSQL synchronization tasks, the source database account must create triggers, functions, and other objects in the source database. Therefore, during the synchronization process, do not modify the access permissions of objects such as triggers, functions, or internal tables created by this account in the source database.<br><br>* **Avro format** for subscription is currently in beta testing. To use it, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |


<span id=".5pSv5oyB55qELXNxbC3or63lj6U="></span>
## Supported SQL statements


|**Operation type** |**SQL statement** |
|---|---|
|DML |INSERT, UPDATE, DELETE |
|DDL |CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE, CREAT INDEX, DROP INDEX, CREATE SEQUENCE, ALTER SEQUENCE, DROP SEQUENCE, DROP RULE |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, click **Data subscription**.

4. On the **Data subscription list** page, click **Create subscription**.

5. On the **Configure source database** page, configure the following parameters

&nbsp;

   
   |**Type** |**Parameter** |||**Description** |
   |---|---|---|---|---|
   |**Basic information** |**Task name** |||Optional. Customize the task name. Naming rules are as follows:<br><br><br>* Must start with a Chinese character or letter.<br><br>* Must be 64 characters or less.<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-). |
   ||**Link specification** |||Select the link specification for the subscription task. Currently only **Standard** is supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For details on the link specifications, refer to <a href="https://docs.byteplus.com/en/docs/DTS/product_specifications">Product specifications</a>.</div><br> |
   |**Basic configuration** |**Select an existing data source** |||You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |||Select **PostgreSQL**. |
   ||**Access method** |||Select **PostgreSQL connected over express network**. |
   ||**Region** |||Select the region of the virtual private cloud. |
   ||**Host address** |||Enter the host address of the target self\-managed instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, only IPv4 addresses are supported for access. IPv6 addresses are not yet supported.</div><br> |
   ||**Port** |||Enter the port number of the target self\-managed instance. |
   ||**Database name** |||Enter the database name of the target self\-managed instance. |
   ||**Virtual private cloud (VPC)**  |||Select the target VPC from the drop\-down list as follows:<br><br><br>* Direct connect: Select any VPC under the CEN when achieving data connectivity through a dedicated line CEN.<br><br>* VPN connection: Select the VPC bound to the VPN gateway when achieving data connectivity through VPN. |
   ||**Subnet** |||Select the subnet connected to the VPC from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When migrating a PostgreSQL instance connected over express network, you need to add subnet CIDR block access permissions to the allowlist or security group policy on the source end in advance. Click <strong>View subnet CIDR blocks</strong> to view and copy CIDR blocks.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When creating a data migration task via express network, the system creates several network cards by default in your selected VPC, and the network cards are mounted by default to the subnet you selected. The network card name format is <code>dts_shuttle_********</code>.</div><br> |
   ||**Database account** |||Enter the database account of the target instance. |
   ||**Database password** |||Enter the password corresponding to the database account of the target instance. |
   ||**Test connection** |||Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check the network**: When this error prompt appears, confirm network connectivity.<br><br>* **Connection authentication failed. Check the username and password**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical staff.<br><br>* **Invalid IP address**: When this error prompt appears, verify the accuracy of the IP address.<br><br>* **The Express network requires the subnet to have \* available IPs. The current number of available IPs in the subnet is insufficient, and the task can not be created. Check the subnet resources in the VPC**: When this error prompt appears, adjust the number of available IPs in the VPC subnet to ensure enough IPs in the target VPC subnet. |
   |**Middleware configuration** |**Select an existing data source** |||You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Subscription built\-in middleware**<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Subscription built\-in middleware is only applicable to test scenarios.</div><br> |**Virtual private cloud (VPC)**  ||Select the target VPC from the drop\-down list. |
   |||**Subnet** ||Select the subnet within the target VPC from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The subnet in the target VPC must have at least one available IP.</div><br> |
   ||**Customer owned middleware**<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For business scenarios, it is recommended to select self\-owned middleware.</div><br> |**Message Queue for Kafka** |**Kafka instance** |Select the target instance from the drop\-down list. |
   ||||**Topic** |Select the target Topic information from the drop\-down list. |
   ||||**Kafka user** |Enter the Kafka username.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only SASL authentication with the PLAIN mechanism is supported. Specify the username for the PLAIN mechanism here.</div><br> |
   ||||**Password** |Enter the Kafka user's password. |
   |||**Kafka connected over express network** |**Broker** |Enter the IP address and port number of all Brokers, formatted as `host1:port1`, for example `10.1.1.1:9093`. If there are multiple Brokers, separate them with commas (,). |
   ||||**Topic** |Enter the target Topic information. |
   ||||**Virtual private cloud (VPC)**  |Select the target VPC from the drop\-down list as follows:<br><br><br>* Direct connect: Select any VPC under the CEN when achieving data connectivity through a dedicated line CEN.<br><br>* VPN connection: Select the VPC bound to the VPN gateway when achieving data connectivity through VPN. |
   ||||**Subnet** |Select a subnet within the VPC from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When subscribing to a Kafka instance connected over express network, you need to add subnet CIDR block access permissions in the allowlist or security group policy on the source end in advance. Click <strong>View subnet CIDR blocks</strong> to view and copy CIDR blocks.</div><br> |
   ||||**Kafka user** |Enter the Kafka username.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only SASL authentication with the PLAIN mechanism is supported. Specify the username for the PLAIN mechanism here.</div><br> |
   ||||**Password** |Enter the Kafka user's password. |
   |||**Test connection** ||If the test connection fails, modify the configuration based on the failure prompt, then test to verify if the instance connects successfully. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct.** <br><br>   * When subscribing to messages in Kafka connected over express network or Message Queue for Kafka, this error prompt requires verification of the username and password accuracy.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical staff.<br><br>* **Invalid IP address**: When this error prompt appears, verify the accuracy of the IP address.<br><br>* **Connection authentication failed, check if the network is normal**: This error prompt appears only when subscribing to messages in Kafka connected over express network. When this error prompt appears, verify network connectivity.<br><br>* **The VPC requires the subnet to have \* available IPs. The current number of available IPs in the subnet is insufficient, and the task can not be created. Check the subnet resources in the VPC**: This error message will only appear when you subscribe to a Kafka connected over express network. When this error occurs, adjust the number of available IPs in the VPC subnet to ensure enough IPs are available within the target VPC subnet. |
   |**Project and billing** |**Project** |||Optional. Select the affiliated project for the task from the drop\-down list. By default, it is under **default (default project)** . You can also click **Create new project** to create a new project. For more information, refer to [Creating a new project](https://docs.byteplus.com/en/docs/6649/94336#%E6%96%B0%E5%BB%BA%E9%A1%B9%E7%9B%AE).<br><br>Description<br><br><br>* To grant sub\-user privileges to access resources in a specific project, refer to [Modifying project privileges](https://docs.byteplus.com/en/docs/6649/173422#%E4%BF%AE%E6%94%B9%E9%A1%B9%E7%9B%AE%E6%9D%83%E9%99%90).<br><br>* After a task is created successfully, if you need to change its affiliated project, you can move the resource to another project. For more information, refer to [Moving resources to a project](https://docs.byteplus.com/en/docs/6649/94337).<br><br>* A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources. |
   ||**Tag** |||Optional. Click **Add tag** to set the tag key and tag value to add a tag to the instance. The rules for tag key\-value pairs are as follows:<br><br><br>* Key<br><br>   * Supports any language, characters, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 1 to 128 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br>   * Keys cannot start with any form of `volc:`, such as `Volc:` or `VOLC:`.<br><br>* (Optional) Value<br><br>   * Supports any language, character, digit, space, or symbol (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 0 to 256 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">A tag consists of a key\-value object that identifies cloud resources. It can help you classify cloud resources with the same characteristics (such as use, owner, or environment) for easy filtering and aggregation, so that you can easily manage the cloud resources. For more details about tags, refer to <a href="https://docs.byteplus.com/en/docs/6649/189377">Tag overview</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Tags help you categorize cloud resources, control access to cloud resources, and manage billing and cost allocation.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A maximum of 20 tags can be associated with a task in a single operation. A maximum of 50 tags can be associated with a single task.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For a single resource, tag keys must be unique, and each tag key can have only one Value.</div><br> |
   ||**Billing type** |||Select a billing method: **Pay\-as\-you\-go** or **Subscription**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For detailed billing information, refer to <a href="https://docs.byteplus.com/en/docs/DTS/billing_overview">Billing instructions</a>.</div><br> |
   ||**Subscription duration** |||Select the duration of the subscription as needed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When selecting <strong>Subscription</strong> in <strong>Billing method</strong>, you can set the purchase time and also check <strong>Automatic renewal</strong>. The system automatically renews before task expiration.</div><br> |
   



&nbsp;

1. Click **Next: Configure subscription object**.

2. On the **Configure subscription object** page, configure the following parameters.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you do not need to start the subscription task immediately, click <strong>Save </strong>at the bottom right of the page after completing the subscription object configuration. Saving means the subscription task is created successfully but not started.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After saving, the task status will be <strong>To be started</strong>. When you need to start this task, on the <strong>Data subscription list page</strong>, click Configure <strong>subscription channel</strong> under the <strong>Actions</strong> column for the subscription task that has not yet started   </div>
   

   
   |**Parameter** ||**Description** |
   |---|---|---|
   |**Basic information** |**Subscription format** |Select data subscription format. Subscription formats support **BytePlus Proto**, **Canal Proto**, **Canal JSON**, **Avro format**, and **Debezium JSON format**. For details on subscription formats, refer to [Data subscription format](https://docs.byteplus.com/en/docs/DTS/data_subscription_format).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>Avro format</strong> and <strong>Debezium JSON format</strong> are currently in beta testing. To use it, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> for technical support.</div><br> |
   ||**Kafka Partition policy** |Select the reception policy for the target Topic Partition as needed. The following reception policies are supported:<br><br><br>* Deliver unified to Partition 0<br><br>* Deliver to different Partitions based on the combined hash value of the database name and the table name<br><br>* Deliver to different Partitions based on the hash value of the primary key<br><br>* Deliver to different Partitions based on the hash value of the specified column<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When the access method selects <strong>Kafka connected over express network</strong> or <strong>Message Queue for Kafka</strong>, this parameter can be configured.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">After the subscription task starts, the following actions are not supported:</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Modify the reception strategy of the Kafka Partition in the DTS console.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Modify the number of Partitions in Kafka.</div><br> |
   ||**Subscription type** |Currently, only **Incremental subscription** can be selected. |
   ||**Subscription object** |Select the objects to subscribe from the **Subscription object**. After selecting the target subscription object, confirm the subscription objects again in the **Selected object** box on the right. Meanwhile, if the entire database is checked in the **Subscription object** area, expanding the database is not supported in the **selected object** area. |
   |<div style="text-align: center"><br><strong>Advanced configuration</strong></div><br> |**Selected databases and tables**<br><br> |Supports reconfiguring the selected databases and tables individually. The specific configuration is as follows:<br><br><br>* **Topic**: Set the Topic in Kafka where tables are delivered according to the drop\-down list, supporting batch modification of the Topic for all target tables. When **Middleware configuration** **Access method** selects **Message Queue for Kafka** or **Kafka connected over express network**, this configuration is supported.<br><br>* **Specify the columns to compute the hash value**: Enter the column name used to compute the hash value. After that, the data will be delivered to the specified Partition or queue according to the hash value of this column. The system supports batch selection of columns for hash value computation across all databases and tables. This configuration is supported when the delivery policy selects **Deliver to different Partitions based on the hash value of the specified column** or **Deliver to different queues based on the hash value of the specified column**. |
   ||**Error retry time** |If the source database or target database disconnects, the subscription task automatically recovers if reconnection occurs within that time. Value range: 600–86400, in seconds (s). The default value is 600 seconds. |
   



&nbsp;

1. Click **Pre\-check**.

2. Optional. If a pre\-check has been performed for the created task, you can confirm whether to restart the pre\-check based on the prompts. If you need to restart, click **OK** in the **Whether to restart the pre\-check** dialog box.

   * If the instances of the source and target databases are not modified, there is no need to restart the pre\-check.

   * If you modify the source and target database instance information or the subscription task parameters, it is recommended to restart the pre\-check to avoid task startup failures or interruptions.

10. On the **Pre\-check** configuration wizard page, perform the following actions based on the check result:

   * Click **Details** in the **Actions** column to view detailed alert and failure messages. After modifying the databases and tables accordingly, click **Retry**.

   * Click **Ignore** in the **Actions** column to ignore the alert and continue starting the subscription task. You can also click **Ignore all** to ignore all alert messages with one click.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Do not ignore the alert when the pre\-check results have failed.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">After selecting <strong>Ignore</strong> alert and starting the subscription task, certain risks may exist. For more information, refer to the prompt on the interface.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For details about the pre\-check, refer to <a href="https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_postgresql">Pre\-check items (PostgreSQL)</a>.      </div>
      

11. At the bottom\-right of the **Pre\-check** page, click **Confirm order**.

12. Select the configuration method according to the billing method of the task creation:

   * For pay\-as\-you\-go, reconfirm the configuration on the **Confirm order** wizard page. Read the Service\-Specific Terms for BytePlus Database Products and Services and check **I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**, and click **Create and start a task**.

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

   * [Consuming BytePlus Proto subscription data via Kafka](https://docs.byteplus.com/en/docs/DTS/Consuming_Volcano_Engine_Proto_subscription_data_via_Kafka)


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[CreateTransmissionTask](https://docs.byteplus.com/en/docs/DTS/CreateTransmissionTask) |Call the CreateTransmissionTask API to create a DTS task. |
|[ModifyTransmissionTask](https://docs.byteplus.com/en/docs/DTS/modifytransmissiontask) |Call the ModifyTransmissionTask API to modify the transmission task. |


&nbsp;
