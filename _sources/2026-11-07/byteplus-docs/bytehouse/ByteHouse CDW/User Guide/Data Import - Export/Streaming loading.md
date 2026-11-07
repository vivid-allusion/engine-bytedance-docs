---
title: "Streaming loading"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-kafka-stream-data-import-practice-parsing-nested-json"
---

ByteHouse supports streaming data through Kafka or other message queues compatible with the Kafka protocol. After launching the Kafka import task, ByteHouse continuously reads Topic messages, providing exactly once assurance, and data can be accessed immediately after consumption. ByteHouse also supports pausing and resuming data import tasks at any time to save resources, ensuring that data is not lost during the process through an internal offset mechanism, and maintaining data consistency. This article introduces how to stream import Kafka data using ByteHouse.

<span id="1f60251a"></span>
# Usage restrictions


* Supported Kafka versions: 0.10 and above.

* ByteHouse engine version requirements: 2.3 and above. You can check your current engine version on the ByteHouse Console on the **Tenant management** \> **Basic information** page.


<span id="0bd81676"></span>
# Prerequisites


* Before migrating Kafka data to ByteHouse, please ensure that the Kafka account and password you use have the following data permissions:

   * List Subjects (Topics)

   * List Consumer Groups (Consumer Group)

   * Consume Messages (Consume Message)

   * Create Consumers and Consumer Groups (Consumers & Consumer Groups)

* Obtain Kafka data source proxy list IP address, Username, and Password. If you need to access BytePlus Message Queue Kafka Edition internally, you also need to obtain the VPC ID where the Kafka data source resides.

* If you access BytePlus Message Queue Kafka Edition internally, add to the whitelist in the VPC security group rules where the Kafka data source resides: `100.64.0.0/10`. For configuration details, please see [manage security group rules](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules).


<span id="06936d09"></span>
# Create a task


1. In the ByteHouse Console, click on **Data loading** tab, then click the **New loading job** button to enter the task creation interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7b7571eb7f74a2ab4a2551844b31d49~tplv-goo7wpa0wc-image.image) </span>

2. Fill in the general information for the import task, customize the task name and task description.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b6fbad97ad14daf85fd9ed2fc66fb03~tplv-goo7wpa0wc-image.image) </span>

3. Select **Kafka data stream** as the data source type and choose the already created datasource from the dropdown list.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4443e4a3b3974577ac4b7c7859a4b63f~tplv-goo7wpa0wc-image.image) </span>

   If you have not created a data source yet, click **Connect to a new datasource**, create and configure Kafka Source, then click **Connect**.

   ByteHouse currently supports data import from the following data sources, with explanations of the parameters to be configured for different data sources as follows:

   
   |Datasource |BytePlus Kafka \- Same Availability Zone<br><br>(Public Network Access) |BytePlus Kafka \- Different Availability Zones<br><br>(Supports Public Network Access Only) |Non\-BytePlus Kafka Service<br><br>(Supports Public Network Access Only) |
   |---|---|---|---|
   |Source Name |Configure the Data Source Name, you can customize the data source name |||
   |BytePlus Internal Mode |Not supported |Not supported |Not supported |
   |VPC ID where Kafka is located |Not supported |Not supported |Not supported |
   |Kafka proxy list IP addresses |IP address consists of **Kafka public/private network address** + **port number**, in the format `Kafka network ID:port number`. Multiple concatenated Kafka proxy list IP addresses are separated by a comma `,`. When filling in, **please be sure to enter the IP addresses of all Broker nodes for the access point you are using**. |||
   ||You can log in to [BytePlus Message Queue Kafka Console](https://console.byteplus.com/kafka/region:kafka+ap-southeast-1/), click **the target instance in the instance list**, and view and copy the public network access IP address in **the instance details** page's **service access.**  |You can log in to [BytePlus Message Queue Kafka Console](https://console.byteplus.com/kafka/region:kafka+ap-southeast-1/), click **the target instance in the instance list**, and view and copy the public network access IP address in **the instance details** page's **service access.**  |You can view and copy it by logging into the Kafka Data Service console. |
   |Authentication mode |The current Kafka datasource supports four authentication modes: NONE, PLAIN, SCRAM\-SHA\-256, and SCRAM\-SHA\-512. It also supports SSL encryption, which you can enable as needed.<br><br>The Kafka broker IP address configuration requirements differ depending on the selected authentication mode:<br><br><br>* **None authentication**: the default port is 9092.<br><br>* **PLAIN、SCRAM\-SHA\-256、SCRAM\-SHA\-512**：<br><br>   * If SSL is not enabled, the default port is 9093.<br><br>   * If SSL is enabled, the default port is 9095. |||
   |Username |The username for Kafka service. |||
   |Password |The password for Kafka Service. |||
   

4. Configure the data source's Topic, consumer group, format, and other information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c67486ee0d43484ba45c5065a46cfcf5~tplv-goo7wpa0wc-image.image) </span>

   * **Topic**: Select the Topic to import.

   * **Consumer group**: For the selected Topic, choose or create a consumer group.

   * **Format**: Specify the consumption format, currently supports JSON_KAFKA and AVRO_KAFKA.

   * **Number of consumers**: This is an optional configuration, you can specify the number of consumers as needed, ensure that the maximum number of consumers equals the number of partitions.

5. Select the target database and table for import.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22020e60be3544848f7fd198edeaecc5~tplv-goo7wpa0wc-image.image) </span>

6. Define the Schema mapping. After setting the data source and target table, the System will automatically populate the Schema mapping table and generate the mapping relationships between the data source and the target table. ByteHouse currently supports the following Schema mapping configuration actions, which you can adjust as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07ea1fcb21c34a5f8ed8f1ee30a2abf3~tplv-goo7wpa0wc-image.image) </span>

   * **Adjust the Schema mapping**

      If the generated Schema does not meet expectations or you need to adjust the mapping relationships between source and target columns, you can click **Re\-parser**, and the System will re\-parser the data.

   * **Adjust the target table**

      You can open a new browser tab, go to the [database page](https://console.byteplus.com/bytehouse/region:bytehouse+ap-southeast-1/n/default/database) and adjust the target table. After adjustment, in the streaming loading page, click **Refresh target table** in the Schema Mapping module. The system will automatically read the adjustments to the target table and update the Schema mapping table.

   * **Real\-time deletion of unique key table data during import**

      If you need to delete data in the data source table during import and your target table is a unique key (Unique Key) table, you can set an expression to define whether to delete a particular data. For details, please see [Delete Data in Real-Time](https://docs.byteplus.com/docs/bytehouse/docs-kafka-stream-data-import-practice-parsing-nested-json#bde44b50).

   * **Generate database timestamps in the target table during import**

      If you need to record the import time of the data during import, you can use an Expression to add timestamps, which facilitates subsequent data query, analysis, and tracking based on the timestamps. For details, please see [Generate a database timestamp in the target table](https://docs.byteplus.com/docs/bytehouse/docs-kafka-stream-data-import-practice-parsing-nested-json#eaa8b2bd).

7. Configure the loading type, Max block size, and specify the virtual warehouse for the import task.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03991837932b4c2c8f7b1b2ef1ebc5fc~tplv-goo7wpa0wc-image.image) </span>

   * **Loading Type:**  Currently only supports incremental writing.

   * **Max Block Size**: Specifies the maximum memory of the writing block, the input value must be between 65,536 and 1,966,080. This parameter directly affects memory consumption; the larger the value, the higher the memory required. You can specify as needed .

   * **Virtual warehouse:**  Use an existing virtual warehouse to load tasks, to enjoy higher transmission performance.

8. Click **Create** to generate an import task. After the import task is created, the system will jump to the task details page, where the task will be in a suspended state, and you can click **Start** to start the task.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f83cbe0d29504b2da5cc90f15e2fe971~tplv-goo7wpa0wc-image.image) </span>

9. In the popup window for launching the Kafka job, confirm the task name and offset to be launched, and after ensuring they are correct, click **OK**, and the system will execute the data loading task.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5bdcc3fa79ad431c9442cf8499f44404~tplv-goo7wpa0wc-image.image) </span>

   To modify the offset, click on **Settings**, and select the partition and offset. Once configured, click **OK**, and the system will execute the data loading task.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/762584133294473e9051487f9c2ce53a~tplv-goo7wpa0wc-image.image) </span>

   * **Current**: Continue consuming from the offset position of the consumer group stored in the Kafka server.

   * **Earliest**: Start consuming from the earliest message stored in the Kafka server.

   * **Latest**: Start consuming the latest message stored in the Kafka server.

   * **Custom**: Customize the consumption position of the corresponding Kafka consumer group and continue consuming from the customized position.


<span id="af552be0"></span>
# View a task

On the data loading page, you can view all the created tasks through the task view.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6babbb10607b468b8913218b4f71c773~tplv-goo7wpa0wc-image.image) </span>

You can also view the task execution status, view task execution logs and configurations through the execution view.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68fb5ba620dc4dc9a25144197f4c477e~tplv-goo7wpa0wc-image.image) </span>


* **View task execution logs**

   Click the **Log** button of the target task row to view the current task's execution log, and you can click to copy or download the log.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19971f2e1dfe4ca4b403d0e43140ad63~tplv-goo7wpa0wc-image.image) </span>

* **View configuration**

   Click the **Config** button in the target task row to view the current task execution log. You can click copy or download the configuration JSON file to use as a reference for importing data via OpenAPI.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/312f0543fe7242b78001f0c777517572~tplv-goo7wpa0wc-image.image) </span>


<span id="7245d1af"></span>
# Start/stop a task


1. In the task list, click the source type dropdown and select Kafka.

2. Click the **Start** button in the target task row to launch the current import task.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f8eb599bf9b4fc8b346063f978c1c14~tplv-goo7wpa0wc-image.image) </span>

3. Click the **task name**, enter the task details page, and view the task sync history, consumption status, current schema mapping configuration, logs, and configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/58f6910cfcaa4cfc91c5dd24c2d9f242~tplv-goo7wpa0wc-image.image) </span>

4. Click **Stop** to stop a streaming task if needed.


<span id="ba9c8ff4"></span>
# Edit a task


1. In the task list, click the source type dropdown and select Kafka.

2. Click the **Edit** button in the target task row to enter the streaming import task configuration page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55bb7cd1368248d581820eeb874fe0f0~tplv-goo7wpa0wc-image.image) </span>

3. Adjust task settings as needed, edit them, and then click **Update**.


<span id="1e7b71dc"></span>
# Copy task configuration

If you need to import data through OpenAPI, you can copy the task configuration as a reference.

**How to use**:


1. In the task list, click the source type dropdown menu and select Kafka.

2. Click  **...**  on the target task row and then click **Copy Config**, and the system will copy the current import task configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dddb04dd7ae5497cbe98c1e0c7d25241~tplv-goo7wpa0wc-image.image) </span>


<span id="c1ae09b2"></span>
# Delete a task

In the task list, click  **...**  on the target task row and then click **Delete job**, and confirm to delete the current task.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73553512f4ec4a3fb8ee1370204a1494~tplv-goo7wpa0wc-image.image) </span>

<span id="77d90eeb"></span>
# Advanced usage

<span id="eaa8b2bd"></span>
## Generate a database timestamp in the target table

Go to **Data loading** \-\> **New loading job** \-\> **Define Schema Mapping** and configure the column mappings in the red box outlined below in :

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19b0d37d36834c9897cc08c40ae239ef~tplv-goo7wpa0wc-image.image) </span>


* _c0 is a placeholder.

* The data type should be selected as DateTime.

* The value of the Expression is BytePlus's now() expression, which returns the current time.


<span id="bde44b50"></span>
## Delete data in real\-time

When the target table you are using is a Unique Key table, ByteHouse supports mapping the column in the target table to the `_delete_flag_` column, and supports defining delete conditions through expressions. When there is data in the import task that meets the deletion conditions, ByteHouse will immediately delete that data.

<span id="9f52574d"></span>
### Steps


1. Go to **Data loading** \-\> **New loading job** \-\> **Define Schema Mapping**, open the **Row delete control** button to enable real\-time delete function. After enabling, the system automatically adds a `_delete_flag_` column to the mapping table.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c60ff5b1de5e472c91857a1c8438d337~tplv-goo7wpa0wc-image.image) </span>

2. Configure column mapping. You can specify columns in the target table and map them to `_delete_flag_`. Then configure the column mapping expression. When the expression condition is met, the system deletes the corresponding data.

   As shown below, map the `action` column in the target table to `_delete_flag_` and use the `multiIf` expression to define the `action` column. When the value of the `action` column is 1, the record with the unique key is deleted; when the value is 0, it indicates data insertion. An example of the multiIf expression is as follows:

   ```SQL
   multiIf(action='delete',1,0)
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/74cfab9368854f528251b1d78a149f95~tplv-goo7wpa0wc-image.image) </span>


<span id="ca3b4147"></span>
### Related reference: best practices for real\-time deletion of unique key table data

ByteHouse also supports real\-time deletion of specified unique key data via SQL commands. You can refer to [Example 3: Real-time deletion of data with a specified unique key](https://docs.byteplus.com/docs/bytehouse/bytehouse-best-practice-for-unique-key-tables#2bf65463) for more examples.
