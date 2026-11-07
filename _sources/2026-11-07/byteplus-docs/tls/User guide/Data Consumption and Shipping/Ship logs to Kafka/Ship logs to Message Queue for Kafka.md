---
title: "Ship logs to Message Queue for Kafka"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/ship_logs_to_message_queue_for_kafka"
---

Torch Log Service (TLS) allows you to ship logs to Kafka. This topic describes how to create a shipping configuration.

<span id="前提条件"></span>
## **Before you begin**


* Activate TLS, and use it to collect log data successfully.

* Activate BytePlus Message Queue for Kafka. Create a Kafka instance and a topic in the same Region as the specified topic.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To ensure the order of data in a Shard, TLS will ship the data in a Shard to a Kafka Topic Partition. Therefore, it is recommended that the number of Kafka Topic Partitions created is greater than or equal to the number of TLS Topic Shards.   </div>
   

* TLS needs to play the ServiceRoleForTLS role to achieve cross\-service access to other cloud service resources, that is, you need to grant TLS the permission to access and write to Kafka instances.

   If you have not yet created the ServiceRoleForTLS role, TLS will guide you to operate when you create a shipping configuration in the console. For more information, refer to [Authorize cross-service access](https://docs.byteplus.com/docs/tls/Authorizing_cross-service_access).


<span id="操作步骤"></span>
## Procedure


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Data processing** \> **Log shipping**.

3. On the **Kafka shipping** Page, click **Create Kafka shipping configuration**.

4. Specify the basic information for the shipping configuration.

   
   |Parameter |Description |
   |---|---|
   |Configuration name |Set the name of the shipping configuration. |
   |Source project |Select the data source project from the drop\-down list. |
   |Source topic |Select the data source topic from the drop\-down list. |
   

5. Specify the object information for the shipping configuration.

   
   |Parameter |Description |
   |---|---|
   |Kafka instance |Specify the name of the destination Kafka instance.<br><br>If no Kafka instance is available, create one in the Kafka console as prompted. |
   |Target topic |Select the data source topic from the drop\-down list.<br><br>If no Kafka topic is available, create one in the Kafka console as prompted. |
   |Compression type |Log data can be compressed based on the specified compression type before the log data is shipped to a Kafka instance. This reduces read traffic costs. The following compression types are supported:<br><br><br>* No compression<br><br>* snappy<br><br>* gzip<br><br>* lz4 |
   |Shipping format |The format of log data shipped to the Kafka instance. The raw format and JSON are supported.<br><br><br>* Raw format: ships raw logs that are received by TLS and are not structured in TLS to the Kafka instance. The data does not include the reserved fields and defined fields added by TLS.<br><br>* JSON format: ships log data in JSON format. The name and value of each log field is a key\-value pair. If you use JSON, configure the shipping field list as needed. |
   |Whether to escape |If you ship log data in JSON format, specify whether to escape log data shipped to the Kafka instance.<br><br><br>* Escape: In the first\-level nodes of JSON, if the value of a field is a JSON array or in other formats, TLS uses escape characters () to convert the value into a string and reserves one level of nodes. Such data can be added to big data systems or stream computing platforms.<br><br>* Do not escape: The log data is in JSON format. TLS does not modify the JSON structure or level.<br><br>   For example, log data in JSON format is `{"level":"info", "message":{"city":"beijing", "name":"zhangsan"}}`. The escaped log data is `{"level":"info","message":"{\"city\":\"beijing\", \"name\":\"zhangsan\"}"}`. If not escaped, the log data in the original format is shipped. |
   |Shipping log field |If you ship log data in JSON format, specify the keys of all fields to be shipped.<br><br><br>* Select the fields to be shipped to the Kafka instance from the list of fields.<br><br>* In addition to the fields defined in the log source, default metadata fields such as **source** added to each log entry by TLS can be shipped. |
   |Shipping time range |Specify the time period during which log data is shipped. Only log data within the specified time period is shipped to the Kafka instance.<br><br><br>* If the end time is not specified, the latest written log data is shipped continuously.<br><br>* Historical log data can be shipped. All log data retained can be shipped to the Kafka instance.<br><br>* The specified time period cannot be changed. |
   

6. Click **Submit**.

   After you create the shipping configuration, view the rule information in the list of shipping configurations. By default, the shipping configuration is enabled.
