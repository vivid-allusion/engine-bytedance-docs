---
title: "Use Logstash to read TLS data and write to Cloud Search"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Read_log_service_data_and_write_to_Cloud_Search"
---

This topic describes how to use a Logstash pipeline to read log data from TLS topics and write it to a Cloud Search index.

<span id="349e7074"></span>
## Background

TLS provides Kafka protocol consumption, allowing a log topic to be consumed as a Kafka topic, with each log corresponding to a Kafka message. You can use the Logstash Kafka connector to connect to the Log Service and consume log data from TLS via the Logstash pipeline to downstream big data components or data warehouses.

<span id="XeJH2IvJ"></span>
## Process description

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8e29a2a7513cc63d8811fcb467a8b725.png) </span>


1. Prepare the data source TLS topic.

   You need to create a log project in the TLS console, then create a log topic and enable Kafka protocol consumption.

   You also need to obtain the project access address, project ID, topic ID, and Kafka protocol topic ID to input this information in the Logstash pipeline to connect to TLS.

2. Prepare the target Cloud Search index.

   You need to create an instance and obtain its access address in the Cloud Search console.

3. Create a Logstash pipeline.

   After preparing the data source and data destination, you can create a Logstash pipeline in the Cloud Search console.


<span id="32f31eda"></span>
## Precautions

To ensure network access security, all cloud products used here access via internal networks. Therefore, Logstash and the Elasticsearch or OpenSearch instance must be within the same region and the same VPC.

You can create a virtual private cloud before creating cloud resources. For specific procedures, refer to [Creating VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [Creating subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).

<span id="qpwQ7EXM"></span>
## Step 1: Prepare the TLS topic for the data source

Before consuming TLS logs through the Logstash pipeline, complete the following preparations for TLS:


1. Create a log project. For more information, see [Create project](https://docs.byteplus.com/en/docs/tls/Managing_projects#.5Yib5bu65pel5b-X6aG555uu).

2. Create a log topic. For more information, see [Create a topic](https://docs.byteplus.com/en/docs/tls/Managing_topics#.5Yib5bu65pel5b-X5Li76aKY).

3. Enable Kafka protocol consumption and obtain the Kafka protocol consumption topic ID. For detailed operations, refer to [Enable the feature of using the Kafka protocol for consumption](https://docs.byteplus.com/en/docs/tls/use_the_kafka_protocol_to_consume_logs#.XzEt5byA5ZCva2Fma2HmtojotLnlip_og70=).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The Kafka protocol consumption ID indicates the target topic to read messages from in the Logstash pipeline that consumes messages.   </div>
   

4. Obtain the access point address, including the log project's ID, private network address, and log topic ID. For more information, see [View private network addresses and other information](https://docs.byteplus.com/en/docs/tls/Managing_projects#.5p-l55yL56eB572R5Zyw5Z2A562J5L-h5oGv).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Log project ID: Used as the Kafka SASL username when consuming TLS logs via Kafka protocol.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Log project private network address: Used as the connection address for the TLS log project in the Logstash pipeline.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Log topic ID: used in the Logstash pipeline that produces messages to specify the target topic for message writing.   </div>
   


<span id="36720258"></span>
## Step 2: Prepare the target cloud search service index

To consume TLS logs using the Logstash pipeline, you need to prepare a data destination. This article uses the cloud search service index as the destination. Follow these steps to create an instance and obtain its access address.


1. Create a Cloud Search service instance. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-instance).

2. Obtain the instance's private network address. For more information, see [View instance details](https://docs.byteplus.com/en/docs/cloudsearch/instance-details).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The instance's private network address is used to access the instance in the Logstash pipeline.   </div>
   

<span id="ae2e817b"></span>
## Step 3: Create the Logstash pipeline


1. Create a Logstash instance in the same region and VPC as the Cloud Search service instance in Step 2. For detailed operations, see [Create a Logstash instance](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_Logstash_instance).

2. Create a Logstash pipeline, referencing the `Input-kafka` and `Output-elasticsearch/opensearch` templates, and modify the templates according to actual conditions. For specific actions, see [Create a pipeline](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_pipeline). Example configuration is as follows.

   ```Ruby
   input {
     kafka {
       # note the domain must be replaced with the project domain
       bootstrap_servers => ["tls-cn-beijing.ivolces.com:9093"]
       auto_offset_reset => "latest"
       consumer_threads => 5
       decorate_events => true
       # Kafka protocol consumption ID obtained
       topics => ["out-**"]
       security_protocol => "SASL_SSL"
       sasl_mechanism => "PLAIN"
       # For username and password retrieval methods and details, refer to consuming logs via Kafka protocol
       sasl_jaas_config => "org.apache.kafka.common.security.plain.PlainLoginModule required username='***' password='***';"
       # Store JSON content in the topic, parse it, and write fields into the Cloud Search service index
       codec => json {
         ecs_compatibility => "disabled"
       }
     }
   }
   output {
     opensearch {
      # Target instance endpoint
       hosts => "https://elasticsearch-o-dev-******.escloud-dev.ivolces.com:****"# Cloud Search instance access link
       # Target instance basicAuth authentication information, if any
       user => "admin"
       password => "********"
       # Index name
       index => "test_orders"
       # The id here is a field present in some input. If not specified, ES generates it automatically
       # document_id => "%{id}"
       # Whether to request only HTTPS links in the `hosts` configuration array
       ssl => false
       # Whether to verify the Cloud Search server certificate when using HTTPS links. Must be false
       ssl_certificate_verification => false
     }
   }
   ```
   

3. Save and deploy the pipeline. When the Logstash instance status returns to **Running**, check the logs to verify whether the pipeline is running properly. For specific actions, refer to [Query logs](https://docs.byteplus.com/en/docs/cloudsearch/Query_logs).


<span id="oA7GcQa9"></span>
## Verify results

Query the data in the executed index in Dev Tools to verify the write results. For specific actions, see [Dev Tools](https://docs.byteplus.com/en/docs/cloudsearch/dev_tools). Example command is as follows.

```HTTP
GET  test_orders/_search
{
    "size": 10
}
```


Example output is as follows.

```JSON
{
  "took": 2,
  "timed_out": false,
  "_shards": {
    "total": 1,
    "successful": 1,
    "skipped": 0,
    "failed": 0
  },
  "hits": {
    "total": {
      "value": 1,
      "relation": "eq"
    },
    "max_score": 1,
    "hits": [
      {
        "_index": "test_orders",
        "_type": "_doc",
        "_id": "test_id_1",
        "_score": 1,
        "_source": {
          "id": "test_id_1",
          "i_field": 12,
          "k_field": "test_1",
          "@version": "1",
          "@timestamp": "2025-11-03T09:05:23.444042342Z"
        }
      }
    ]
  }
}
```
