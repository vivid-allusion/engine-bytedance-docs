---
title: "Use Logstash to read Message Queue for Kafka data into Cloud Search"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Read_Message_Queue_for_Kafka_data_into_Cloud_Search"
---

This topic describes how to use a Logstash pipeline to read message data from a Message Queue for Kafka topic and write it into a Cloud Search index.

<span id="eqVUVRTE"></span>
## Background

Message Queue for Kafka is a distributed message middleware service built on Apache Kafka. It features high throughput and scalability, provides streaming data publish/subscribe and multi\-replica storage mechanisms, and is widely used in log compression collection, streaming data processing, message decoupling, and traffic peak shaving scenarios. You can use the Logstash Kafka connector to connect to Message Queue for Kafka and consume message data from a Message Queue for Kafka topic to downstream big data components or data warehouses via a Logstash pipeline.

<span id="r6Hl1a21"></span>
## Process description

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e257e99e8cb7f16e7f298e120246221f.png) </span>


1. Prepare the data source Message Queue for Kafka topic.

   You need to create an instance in the Message Queue for Kafka console, then create a topic.

   You also need to obtain the instance's access address and the topic name to enter into the Logstash pipeline for connectivity with Message Queue for Kafka.

2. Prepare data destination Cloud Search service index.

   You need to create an instance and obtain its access address in the Cloud Search console.

3. Create a Logstash pipeline.

   Once your data source and destination are ready, you can create a Logstash pipeline in the Cloud Search console.


<span id="H3GCF2wT"></span>
## Precautions

To ensure network access security, all cloud product services used here access via the internal network, so the Message Queue for Kafka Instance and the Cloud Search Instance must be within the same VPC in the same Region.

You can create a virtual private cloud before creating cloud resources. For specific procedures, refer to [Creating VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [Creating subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).

<span id="2XfkmilX"></span>
## Step 1: Prepare Message Queue for Kafka Topic

Before consuming Message Queue for Kafka messages through the Logstash pipeline, complete the following preparation for the Message Queue for Kafka.


1. Create an instance and obtain the instance ID. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/kafka/creating-instance) and [View instance details](https://docs.byteplus.com/en/docs/kafka/viewing-instance-details).

2. Create a topic and obtain the topic name. For detailed operation, see [Create Topic](https://docs.byteplus.com/en/docs/kafka/creating-topic) and [View topic details](https://docs.byteplus.com/en/docs/kafka/viewing-topic-details).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Instance ID: used as the Kafka SASL username when reading message data from the Message Queue for Kafka topic.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Topic name: used to specify the target topic for writing messages in the Logstash pipeline producing messages.   </div>
   


<span id="jhCZgXng"></span>
## Step 2: prepare the data target Cloud Search service index

Before consuming Message Queue for Kafka messages through the Logstash pipeline, you need to prepare a data destination source. This article uses a Cloud Search service index. Follow the steps below to create an instance and obtain its access address.


1. Create a Cloud Search service instance. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-instance).

2. Determine the index schema according to the data format of Message Queue for Kafka, and create the index in Dev Tools. For specific procedures, refer to [Dev Tools](https://docs.byteplus.com/en/docs/cloudsearch/dev_tools). The example statement is as follows.

   ```HTTP
   PUT test_orders
   {
     "mappings": {
       "properties": {
         "k_field": {
           "type": "keyword"
         },
         "i_field": {
           "type": "integer"
         }
       }
     }
   }
   ```
   


<span id="du03FYlm"></span>
## Step 3: create Logstash pipeline


1. Create a Logstash instance in the same region and VPC as the Cloud Search service instance in Step 2. For detailed operations, see [Create a Logstash instance](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_Logstash_instance).

2. Create a Logstash pipeline, referencing the `Input-kafka` and `Output-elasticsearch/opensearch` templates, and modify the templates according to actual conditions. For specific actions, see [Create a pipeline](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_pipeline). Example configuration is as follows.

   ```Ruby
   input {
     kafka {
       # Protocol type PLAINTEXT
       bootstrap_servers => ["kafka******.ivolces.com:****"] # Connection address of the Message Queue for Kafka instance
       client_id => "logstash_client"
       group_id => "logstash_consumer"
       auto_offset_reset => "latest"
       consumer_threads => 5
       decorate_events => true
       topics => ["***_logstash_test"]
       # The topic stores content in JSON format, which will be parsed and written by field into the Cloud Search index
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
       # Keep consistent with source index name
       index => "test_orders"
       document_id => "%{id}"
       # Whether to request only HTTPS links in the `hosts` configuration array
       ssl => false
       # verify the cloud search server certificate when using HTTPS connections
       ssl_certificate_verification => false
       # when ssl_certificate_verification is true, verify the server CA certificate path in .cer or .pem format
       # cacert => "CA certificate path"
     }
   }
   ```
   

3. Save and deploy the pipeline. When the Logstash instance status returns to **Running**, check the logs to verify whether the pipeline is running properly. For specific actions, refer to [Query logs](https://docs.byteplus.com/en/docs/cloudsearch/Query_logs).


<span id="IAQrqc7Z"></span>
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
