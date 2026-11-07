---
title: "Create a workflow"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_a_workflow"
---

Milvus for VectorDB supports data migration. You can migrate existing data from other data sources to Milvus for VectorDB through workflows. This topic describes how to create a workflow.

<span id="31TFo3FZ"></span>
## Prerequisites


* A Milvus instance, Flink project, and Flink resource pool are created, and the Milvus instance and Flink resource pool are in the same private network. see 

* If the data migration source is Kafka, create a Kafka instance and obtain the access point. Ensure the Kafka instance and Milvus instance are in the same private network. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/kafka/creating-instance) and [View access points](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints).

* To add an Embedding Transform node, the Flink project must enable public network access. 


<span id="eMIIhhtO"></span>
## Procedure


1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. Select the project and region for the workflow at the top navigation bar.

3. In the left navigation bar, select **Data migration**, then click **Create workflow**.

4. In the **Select source type** dialog, choose the data migration source, then click **Create**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The current data migration sources support <strong>Kafka</strong>, <strong>TOS</strong>, <strong>Self\-built Milvus</strong>, and <strong>Viking DB</strong>. Selecting <strong>Self\-built Milvus</strong> or <strong>Viking DB</strong> will redirect to the database transfer service DTS to create sync tasks. For specific steps, refer to <a href="https://docs.byteplus.com/en/docs/DTS/Synchronizing_to_Volcano_Engine_Milvus">Sync to BytePlus VectorDB for Milvus </a>.   </div>
   

5. On the **Create workflow** page, configure the following parameters.

   
   |Parameter |sub\-parameter |Description |
   |---|---|---|
   |**Basic information** |||
   |Workflow name ||Enter the workflow name. Naming rules are as follows:<br><br><br>* Length must be 4 to 128 characters.<br><br>* Must start and end with a letter or digit.<br><br>* Can only contain letters, digits, underscores (_), and hyphens (\-). |
   |Remarks (optional) ||Enter remarks for the workflow, supporting up to 128 characters. |
   |**Workflow**<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Configure each node in the workflow. The workflow includes <strong>Source</strong> and <strong>Destination</strong> nodes by default, serving as the start and end points respectively. You can also click <strong>Add Transform</strong> to add up to 5 <strong>Transform</strong> nodes.</div><br> |||
   |Source |Kafka |Select **Kafka** from the **Type** dropdown list, then configure the following fields.<br><br><br>* Kafka instance: Select the Kafka instance to migrate from the dropdown list. To create a new Kafka instance, see [Create an instance](https://docs.byteplus.com/en/docs/kafka/creating-instance).<br><br>* Kafka Topic: select the Kafka message topic to migrate from the dropdown list. To create a new Kafka message topic, see [Create a topic](https://docs.byteplus.com/en/docs/kafka/creating-topic).<br><br>* Bootstrap Servers: enter the access point IP address of the Kafka instance. For how to get the access point IP address, see [View access points](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints).<br><br>* Consumer Group: enter the consumer group of the Kafka instance. For how to get the consumer group, see [View group details](https://docs.byteplus.com/en/docs/kafka/Viewing-consumption-status). If the Kafka instance has not enabled the automatic group creation feature, you need to manually create the consumer group in the Kafka instance. For specific operations, see [Create a group](https://docs.byteplus.com/en/docs/kafka/creating-group).<br><br>* Advanced configuration (optional): You can also use code for advanced configuration. Click a field to view detailed descriptions on the right. Example configuration is as follows.<br><br>   ```JSON```<br>```   {```<br>```       # 指定数据 schema 告知数据来源如何将数据解析为想要的行。```<br>```       "schema": {```<br>```           "fields": {```<br>```               "id": "int",```<br>```               "age": "int",```<br>```               "name": "string",```<br>```               "description": "string"```<br>```           },```<br>```           "primaryKey": {```<br>```               "name": "id",```<br>```               "columnNames": [```<br>```                   "id"```<br>```               ]```<br>```           }```<br>```       },```<br>```       "kafka.config": {```<br>```           # Kafka 消费者客户端 ID。```<br>```           "client.id": "kafka2milvus_client",```<br>```           # 最大拉取数据条数。```<br>```           "max.poll.records": 500,```<br>```           # 当不存在消费 offset 时的消费位点策略。```<br>```           "auto.offset.reset": "earliest",```<br>```           # 是否开启 offset 自动提交。```<br>```           "enable.auto.commit": "true",```<br>```           # Kafka 接入点认证协议。获取方式请参见使用 PLAINTEXT 接入点连接实例。```<br>```           "sasl.mechanism":"PLAIN"```<br>```       },```<br>```       # 数据格式。```<br>```       "format": "json",```<br>```       # 消费者的初始消费模式。```<br>```       "start_mode": "earliest"```<br>```   }```<br>```   ```<br>    |
   ||TOS |Select **TOS** in the **type** dropdown, then configure the following fields.<br><br><br>* Bucket: select the TOS bucket. To create a new TOS bucket, refer to [Create a bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).<br><br>* Path: select files or directories in the TOS bucket. When selecting a directory, you can use the [file_filter_pattern](https://seatunnel.apache.org/zh-CN/docs/connector-v2/source/S3File/#file_filter_pattern-string) option to filter files.<br><br>* Endpoint: enter the access domain name of the TOS bucket. <br><br>* Credentials Providers: credential providers. Currently fixed as `org.apache.hadoop.fs.s3a.SimpleAWSCredentialsProvider`.<br><br>* Access Key: enter the obtained access key Access Key. <br><br>* Access Secret: enter the obtained access key Access Secret. <br><br>* File Format: select the file format from the dropdown list. Currently supports `text`, `csv`, `parquet`, `orc`, `json`, `excel`, `xml`, and `binary` formats.<br><br>* Advanced configuration (optional): you can also configure with code. Click a field to view detailed descriptions on the right. Example configuration is as follows.<br><br>   ```JSON```<br>```   {```<br>```       # 指定数据 schema 告知数据来源如何将数据解析为想要的行。```<br>```       "schema": {```<br>```           "fields": {```<br>```               "id": "int",```<br>```               "age": "int",```<br>```               "name": "string",```<br>```               "description": "string"```<br>```           },```<br>```           "primaryKey": {```<br>```               "name": "id",```<br>```               "columnNames": [```<br>```                   "id"```<br>```               ]```<br>```           }```<br>```       }```<br>```   }```<br>```   ```<br>    |
   |Destination ||data migration destination. currently fixed to **Milvus**, configure the following fields.<br><br><br>* Instance type: select **Dedicated** or **Serverless**.<br><br>* Milvus instance: select the Milvus instance to migrate data to from the dropdown. To create a new Milvus instance, refer to [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance).<br><br>* URL: displays the access address of the Milvus instance, not editable.<br><br>* Token: enter the Milvus instance account and password, separated by `:`.<br><br>* Database: enter the database name to migrate data to.<br><br>* Collection: enter the name of the collection to migrate data to.<br><br>* Advanced configuration (optional): you can also configure using code. Click a field to view detailed descriptions on the right. Example configuration is as follows.<br><br>   ```JSON```<br>```   {```<br>```     # 是否开启自动 ID```<br>```     "enable_auto_id": true,```<br>```     # 批量写入大小```<br>```     "batch_size": 1000,```<br>```     # schema 保存模式```<br>```     "schema_save_mode": "RECREATE_SCHEMA",```<br>```     # 数据保存模式```<br>```     "data_save_mode": "APPEND_DATA",```<br>```     # 自动创建索引，默认 false```<br>```     "create_index": true,```<br>```     # 自动加载集合，默认 false```<br>```     "load_collection": true```<br>```   }```<br>```   ```<br>    |
   |Transform (optional) |LLM |Select **LLM** from the dropdown, then configure the following fields.<br><br><br>* Model Provider: select the LLM model provider from the dropdown list.<br><br>* Model: enter the LLM model name, e.g., **doubao\-seed\-1\-6\-251015**.<br><br>* API Key: enter the API key used to call the LLM model.<br><br>* Prompt: enter the prompt that tells the LLM model the expected result.<br><br>* Output Column: enter the output column of the LLM model.<br><br>* Advanced configuration (optional): You can also use code for advanced configuration. Click a field to view detailed descriptions on the right. Example configuration is as follows.<br><br>   ```JSON```<br>```   {```<br>```       # 指定输入数据中的哪些字段值用作模型的输入，例如以下是将 name 字段值作为输入。```<br>```       "inference_columns": ["name"]```<br>```   }```<br>```   ```<br>    |
   ||Embedding |Select **LLM** from the dropdown list, then configure the following fields.<br><br><br>* Model Provider: Select the embedding model provider from the dropdown list.<br><br>* Model: enter the Embedding model name, for example, **doubao\-seed\-1\-6\-251015**.<br><br>* API Key: enter the API Key used to call the Embedding model.<br><br>* Advanced configuration: you can also configure using code. Click the field to view detailed descriptions on the right. The configuration example is as follows.<br><br>   ```JSON```<br>```   { ```<br>```       # 原始字段和向量字段的映射，将使用原始字段的值 Embedding 后作为向量字段的值```<br>```       "vectorization_fields": {```<br>```           "description_vector": "description"```<br>```       }```<br>```   }```<br>```   ```<br>   <br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Embedding node supports configuring Doubao multimodal vectorization models to vectorize multiple data types such as text, pictures, and video in mixed layouts. For details, see <a href="https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Multimodal_data_vectorization">Multimodal data vectorization</a>.</div><br> |
   ||Field Mapper |Select **FieldMapper** from the dropdown list, then configure it using code. Click a field to view its detailed description on the right. Example configuration is as follows.<br><br>```JSON```<br>```{```<br>```    # 映射字段, 以下配置将数据中的 age 字段修改为 real_age 字段。未配置的字段将被滤不再向后传递。```<br>```    "field_mapper": {```<br>```      "id": "id",```<br>```      "age": "real_age",```<br>```      "name": "name",```<br>```      "description": "description"```<br>```    },```<br>```}```<br> |
   |Task mode ||Select **BATCH** or **STREAMING**. |
   |**Flink resource pool** |||
   |Private network ||Fixed to the private network where the current Milvus instance resides and cannot be modified. |
   |Flink project ||Select the project from the dropdown list.  |
   |Flink resource pool ||Flink resource pool used in the dropdown list.  |
   |**Flink advanced configuration** |||
   |Concurrency ||Enter the total global concurrency for the task, default is **4**. |
   |CPU cores for a TaskManager ||Select the CPU cores for a single TaskManager from the dropdown list. The default value is **1**. |
   |Memory size for a TaskManager ||Select the memory size of a single TaskManager from the dropdown. Options adjust automatically based on your CPU core settings. |
   |Slots for a TaskManager ||Number of slots per TaskManager, default value is **4**. |
   |JobManager CPU cores ||The CPU cores for JobManager default to **1**. |
   |JobManager memory size ||JobManager memory size will automatically adjust based on the CPU cores you set. |
   

6. Click **Create** or **Create and start** as needed.

   * **Create**: Create the workflow without running it. After you click Create, the system returns to the **Data migration** page, and the workflow is in the **initializing** state. In the workflow list, click **Start** in the **Actions** column of the target workflow to start the data migration workflow.

   * **Create and start**: complete creation and begin running the data migration workflow.
