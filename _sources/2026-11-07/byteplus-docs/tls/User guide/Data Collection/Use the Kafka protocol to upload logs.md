---
title: "Use the Kafka protocol to upload logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Use_the_Kafka_protocol_to_upload_logs"
---

Torch Log Service (TLS) allows for uploading log data to the TLS server over the Kafka protocol. It means that you can collect log data using the Kafka Producer SDK and upload the collected log data to TLS over the Kafka protocol. This topic describes how to upload logs to TLS over the Kafka protocol.

<span id="背景信息"></span>
## Background

Kafka, as high\-throughput message middleware, is used as a message pipeline for log collection in various self\-managed scenarios. For example, you use an open\-source collection tool installed on the server of your log source to collect log data, or uses Kafka Producer to write log data. In such scenarios, the collected log data is consumed by downstream applications through the Kafka consumer pipeline. TLS allows for uploading and consuming log data over the Kafka protocol and offers a complete data upstream and downstream service based on the Kafka data pipeline.

When uploading log data over the Kafka protocol, you do not need to manually enable the log upload feature or install a data collection tool on the server of the data source. With simple configuration, you can collect log data and upload the collected log data to TLS using Kafka Producer. TLS offers sample projects in Java and Go languages for your reference. For more information, refer to [Example](https://docs.byteplus.com/docs/tls/Use_the_Kafka_protocol_to_upload_logs#%E7%A4%BA%E4%BE%8B).

When collecting log data using the Kafka protocol, TLS processes log data based on the data format. For valid JSON data, TLS parses it into key\-value pairs. For invalid JSON data, TLS may fail correctly to parse certain fields. For log data in other formats, TLS encapsulates the entire original log text in the `__content__` field as a string.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When using the Kafka protocol for parsing log data in JSON format, a maximum of one field layer is supported. If a log field contains multiple nested layers of elements, the nested elements are collected and saved as a string.</div>


<span id="限制说明"></span>
## Limits


* Supported Kafka versions are from v 0.11.x through v 2.0.x.

* The following compression methods are supported: GZIP, Snappy, and LZ 4.

* To secure the transmission of logs, use the SASL_SSL protocol. Set the username to the TLS project ID and the password to the AccessKey pair of your account. For more information, refer to [Example](https://docs.byteplus.com/docs/tls/Use_the_Kafka_protocol_to_upload_logs#%E7%A4%BA%E4%BE%8B).

* If a topic has multiple shards, TLS does not ensure the sequence of the log entries. We recommend that you enable load balancing for log collection.

* When using the Kafka Producer Batch to package and send data, the size of one Batch cannot exceed 5 MiB, the upper limit of the size of one message is 5 MiB, and the number of messages in one batch request cannot exceed 10,000. The server will perform length checks on the log data written in each Producer request. If the request exceeds the limit, the entire request fails and no log data is successfully written.


<span id="前提条件"></span>
## Before you begin


* Activate TLS, create projects and topics, and collect log data.

* Make sure that the current account has the permissions to upload log data over the Kafka protocol, that is, the permission to call the `PutLogs` API action. For more information, refer to [Authorizable actions](https://docs.byteplus.com/docs/tls/Authorizable_actions).


<span id="f956cc11"></span>
## Parameter description

To use the Kafka protocol to upload log data, you must configure the following parameters.


|**Parameter** |Example |**Description** |
|---|---|---|
|Connection type |`SASL_SSL` |To secure the transmission of logs, use the SASL_SSL protocol. Set the username to the TLS project ID and the password to the AccessKey pair of your account. |
|username |`c8f20efe-405f-4d57-98cf-8c58d890****` |The Kafka Simple Authentication and Security Layer (SASL) username. Set it to the TLS project ID. |
|password |`AKLTYmQzOWUzMWx*******#WVRnM05UWTRaVGhrTUdFNE5EazNZV0kyTjJRME********` |The Kafka SASL user password. Set it to the AccessKey pair of your BytePlus account,<br><br>in the format of `${access-key-id}#${access-key-secret}`, where:<br><br><br>* `${access-key-id}`: Replace it with your AccessKey ID.<br><br>* `${access-key-secret}`: Replace it with your AccessKey secret.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">We recommend that you use the AccessKey pair of an Identity and Access Management (IAM) user, and make sure that the IAM user has the permissions to call the PutLogs API action. For more information, refer to <a href="https://docs.byteplus.com/docs/tls/Authorizable_actions">Authorizable actions</a>.</div><br> |
|hosts |* Public endpoint: `tls-ap-southeast-1.bytepluses.com:9094`<br><br>* Private endpoint: `tls-ap-southeast-1.ibytepluses.com:9094` |The cluster address for initial connection. The value must be in the `Endpoint:Port`format.<br><br><br>* The endpoint is the TLS endpoint for the current Region. Select the correct endpoint based on the Region and network type. For more information, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint).<br><br>* The port number is 9094.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In hosts, <code>https://</code> is not required for the endpoint.</div><br> |
|topic |`20a50a35-304a-4c01-88d2-23349c30****` |Set the value to the TLS topic ID. |


<span id="配置步骤"></span>
## **Procedure**

TLS can automatically generates a configuration for uploading log data over the Kafka protocol. Follow the steps below to complete the basic information configuration and data source configuration. Then, the automatically generated configuration is displayed on the console page for your reference.


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Common Functions** \> **Log Collection**.

4. In the **Data import** pane, select **Kafka protocol writing**.

5. Complete the basic information configuration, then click **Next step**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Project |The project that you want to use to store the log data uploaded over the Kafka protocol. |
   |Topic name |The topic that you want to use to store the log data uploaded over the Kafka protocol. |
   

6. Complete the data source configuration, then click **Next step**.

   
   |**Parameter** |**Description** |
   |---|---|
   |key |The AccessKey pair of your account, including AccessKey ID and AccessKey Secret. Get the AccessKey pair of your account as prompted on the page.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">We recommend that you use the AccessKey pair of an Identity and Access Management (IAM) user, and make sure that the IAM user has the permissions to call the PutLogs API action. For more information, refer to <a href="https://docs.byteplus.com/docs/tls/Authorizable_actions">Authorizable actions</a>.</div><br> |
   |Network connection method |The type of the network that you want to use to access TLS and upload logs. Valid values: **Intranet** and **Public network**. If you use a private network, make sure that the data source can access TLS over a private network. |
   |Log compression method |The compression method for compressing original log data. Valid values: gzip, snappy, and lz4. |
   |Kafka production side |The log data source type. You can use the open\-source Kafka SDK or Logstash to upload logs over the Kafka protocol. |
   |Result preview |TLS automatically generates a sample based on your parameter configurations for your reference.<br><br><br>* Open\-source Kafka SDK: TLS copies the values of the configuration items and uses them as the values of the corresponding parameters in the open\-source Kafka SDK configuration. For complete sample code, refer to [Example](https://docs.byteplus.com/docs/tls/Use_the_Kafka_protocol_to_upload_logs#%E7%A4%BA%E4%BE%8B).<br><br>* Logstash: TLS automatically generates a Kafka plug\-in configuration for Logstash and tests the connectivity of the plug\-in. For more information, refer to [Upload logs using Logstash](https://docs.byteplus.com/docs/tls/Use_the_Kafka_protocol_to_upload_logs#%E9%80%9A%E8%BF%87-logstash-%E4%B8%8A%E4%BC%A0%E6%97%A5%E5%BF%97). |
   

7. Configure indexes, then click **Submit**.

   After you configure indexes, the log data collected from the source server can be queried and analyzed based on the indexes. For more information, refer to [Configure indexes](https://docs.byteplus.com/docs/tls/Configure-indexes-2).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After completing the task configuration, the configured tasks will not be displayed in the task list. You can open the target topic to view the data.   </div>
   

<span id="示例"></span>
## Example

<span id="通过-logstash-上传日志"></span>
### Upload logs using Logstash

Logstash has a built\-in Kafka output plug\-in called logstash_output_kafka that enables data collection over the Kafka protocol. In scenarios where a log collection and analysis system is built with an Elasticsearch, Logstash, and Kibana (ELK) stack, you can upload log data to TLS over the Kafka protocol only by modifying the Logstash configuration file.

After the TLS console automatically generates a sample Logstash Kafka plug\-in configuration, use the sample code to test the connectivity of the plug\-in. For more information on parameters such as `${hosts}`, refer to the description of

**Result preview** in the [Procedure](https://docs.byteplus.com/docs/tls/Use_the_Kafka_protocol_to_upload_logs#%E9%85%8D%E7%BD%AE%E6%AD%A5%E9%AA%A4) section.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Kafka sends and receives messages through the SASL_SSL endpoint because TLS uses the SASL_SSL connection protocol.</div>


* <div data-tips="true" data-tips-type="tip">Supported Logstash versions are from v 7.12 through v 8.8.1.</div>


* <div data-tips="true" data-tips-type="tip">We recommend that you test the connectivity of the plug\-in with the following configuration during the testing phase. For the production environment, you must remove the stdout output configuration.</div>


* <div data-tips="true" data-tips-type="tip">For log data in JSON format, we recommend that you set the log output format to JSON (codec =\> json) in the configuration. Otherwise, the uploaded data may be incomplete. TLS automatically parses and structures JSON log data.</div>



<span id="通过-kafka-java-sdk-上传日志"></span>
### Upload log data using Kafka SDK for Java

With simple parameter configuration, you can use a Kafka Producer SDK to collect log data and upload the collected log data to TLS over the Kafka protocol. The required dependencies and sample code for uploading log data using Kafka SDK for Java are as follows:


1. Add the dependency.

   Add the kafka\-clients dependency to the pom.xml file.

   ```xml
   <dependency>
       <groupId>org.apache.kafka</groupId>
       <artifactId>kafka-clients</artifactId>
       <version>2.2.2</version>
   </dependency>
   ```
   

2. Upload logs.

   The following sample code is used to upload log data using Kafka SDK for Java.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Before executing the following sample code, you must correctly configure the parameters such as <code>userName</code> based on the description of <strong>Result preview</strong> in the <a href="https://docs.byteplus.com/docs/tls/Use_the_Kafka_protocol_to_upload_logs#%E9%85%8D%E7%BD%AE%E6%AD%A5%E9%AA%A4">Procedure</a> section.   </div>
   

   ```java
   package org.kafka;
   
   import org.apache.kafka.clients.CommonClientConfigs;
   import org.apache.kafka.clients.producer.*;
   import org.apache.kafka.common.config.SaslConfigs;
   
   import java.util.Properties;
   import java.util.concurrent.ExecutionException;
   import java.util.concurrent.Future;
   import java.util.concurrent.TimeUnit;
   import java.util.concurrent.TimeoutException;
   
   public class ProducerBatchDemo {
       public static void main(String[] args) throws InterruptedException, ExecutionException, TimeoutException {
           Properties props = new Properties();
           String userName = "${projectId}";
           //The AccessKey pair of a BytePlus account or an IAM user with the relevant permissions. Security token service (STS) tokens are not supported.
           String passWord = "${AK}#${SK}";
           props.put("bootstrap.servers", "${hosts}");
           props.put("acks", "1"); // NoResponse 0;WaitForLocal 1;WaitForAll -1
           props.put("retries", 5);
           props.put("linger.ms", 100);
           props.put(ProducerConfig.COMPRESSION_TYPE_CONFIG, "lz4"); // Specify a compression method.
           props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
           props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");
           props.put(CommonClientConfigs.SECURITY_PROTOCOL_CONFIG, "SASL_SSL");
           props.put(SaslConfigs.SASL_MECHANISM, "PLAIN");
           props.put(SaslConfigs.SASL_JAAS_CONFIG,
                   "org.apache.kafka.common.security.plain.PlainLoginModule " +
                           "required username=\"" + userName + "\" password=\"" + passWord + "\";");
           // 1. Create a producer object.
           Producer<String, String> producer = new KafkaProducer<String, String>(props);
   
           // 2. Call the send method.
           for (int i = 0; i < 1000; i++) {
               // Kafka SDK for Java does not differ the process of sending a single message or sending multiple messages in batches. You must specify batch.size, linger.ms, and buffer.memory in the configuration file to distinguish the sending method.
               Future<RecordMetadata> meta = producer.send(new ProducerRecord<String, String>("${topicId}", "testMessageValue-" + i));
               RecordMetadata recordMetadata = meta.get(100, TimeUnit.SECONDS);
               // By default, the returned offset is -1.
               System.out.println("partition=" + recordMetadata.partition() + "offset = " + recordMetadata.offset());
           }
           // 3. Close the producer.
           System.out.println("The Kafka Producer sends data asynchronously. We recommend that you wait for 10s before closing the process to ensure all data is successfully sent. Otherwise, the uploaded data may be incomplete.");
           Thread.sleep(10000);
           producer.close();
       }
   }
   ```
   


<span id="通过-kafka-go-sdk-上传日志"></span>
### Upload log data using Kafka SDK for Go

With simple parameter configuration, you can use a Kafka Producer SDK to collect log data and upload the collected log data to TLS over the Kafka protocol. The required dependencies and sample code for uploading log data using Kafka SDK for Go are as follows:


1. Run the following command to install Sarama.

   ```plain
   go get github.com/Shopify/sarama@v1.38.1
   ```
   

2. Import the required dependency packages such as Sarama and upload log data.

   The following sample code is used to upload log data using Kafka SDK for Go.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Before executing the following sample code, you must correctly configure the parameters such as <code>User</code> based on the description of <strong>Result preview</strong> in the <a href="https://docs.byteplus.com/docs/tls/Use_the_Kafka_protocol_to_upload_logs#%E9%85%8D%E7%BD%AE%E6%AD%A5%E9%AA%A4">Procedure</a> section.   </div>
   

   ```go
   package kafka_produce_example
   
   import (
       "fmt"
       "time"
   
       "github.com/Shopify/sarama"
   )
   
   func ExampleProduce() {
       config := sarama.NewConfig()
       config.Version = sarama.V2_0_0_0 // specify appropriate version
       config.ApiVersionsRequest = true
       config.Net.SASL.Mechanism = "PLAIN"
       config.Producer.Return.Successes = true
       config.Net.SASL.Version = int16(0)
       config.Net.SASL.Enable = true
       // projectId
       config.Net.SASL.User = "${projectId}"
       // The AccessKey pair of a BytePlus account or an IAM user with the relevant permissions. Security token service (STS) tokens are not supported.
       config.Net.SASL.Password = "${access-key-id}#${access-key-secret}"
       config.Producer.RequiredAcks = sarama.WaitForLocal
       config.Producer.Compression = sarama.CompressionLZ4
   
       config.Net.TLS.Enable = true
   
       // hosts indicates the producer address. For more information, refer to the parameter description section.
       asyncProducer, err := sarama.NewAsyncProducer([]string{"${hosts}"}, config)
       if err != nil {
          fmt.Println("new producer error:" + err.Error())
          panic(err)
       }
   
       msg := &sarama.ProducerMessage{
          // ${topicID} indicates the ID of TLS topic, such as "0fdaa6b6-3c9f-424c-8664-fc0d222c****".
          Topic: "${topicID}",
          Value: sarama.StringEncoder("test"),
       }
       asyncProducer.Input() <- msg
       go func() {
          for {
             select {
             case msg := <-asyncProducer.Successes():
                if msg != nil {
                   // By default, the returned offset is -1.
                   fmt.Printf("send response; partition:%d, offset:%d\n", msg.Partition, msg.Offset)
                }
             case msg := <-asyncProducer.Errors():
                if msg != nil {
                   fmt.Println("producer send error:" + msg.Error())
                }
             }
          }
       }()
   
       time.Sleep(time.Minute)
       _ = asyncProducer.Close()
   }
   ```
   


<span id="错误信息"></span>
## Error messages

If an error occurs while using the Kafka protocol to upload logs, the error message is returned based on the Kafka error code. For more information, refer to the Kafka [error list](https://kafka.apache.org/20/javadoc/org/apache/kafka/common/errors/package-summary.html?spm=a2c4g.11186623.0.0.79f84e8daAFDQC).

Besides, in Kafka SDK for Java, TLS encapsulates authentication and parameter error information in the `SASLAuthenticationException`. The following table describes the error messages:


|**Error Message** |**Description** |
|---|---|
|invalid SASL/PLAIN request: expected 3 tokens |The user or password is not specified. Configure the parameter based on the description of **Result preview** in the [Procedure](https://docs.byteplus.com/docs/tls/Use_the_Kafka_protocol_to_upload_logs#%E9%85%8D%E7%BD%AE%E6%AD%A5%E9%AA%A4) section. |
|invalid SASL/PLAIN request: empty projectId |The user is not specified. Configure the parameter based on the description of **Result preview** in the [Procedure](https://docs.byteplus.com/docs/tls/Use_the_Kafka_protocol_to_upload_logs#%E9%85%8D%E7%BD%AE%E6%AD%A5%E9%AA%A4) section. |
|invalid SASL/PLAIN request: Password format wrong |The password format is incorrect. Configure the parameter based on the description of **Result preview** in the [Procedure](https://docs.byteplus.com/docs/tls/Use_the_Kafka_protocol_to_upload_logs#%E9%85%8D%E7%BD%AE%E6%AD%A5%E9%AA%A4) section. |
|invalid SASL/PLAIN request: empty AccessKey |The AccessKey ID is not specified. Configure the parameter based on the description of **Result preview** in the [Procedure](https://docs.byteplus.com/docs/tls/Use_the_Kafka_protocol_to_upload_logs#%E9%85%8D%E7%BD%AE%E6%AD%A5%E9%AA%A4) section. |
|invalid SASL/PLAIN request: empty SecretKey |The AccessKey secret is not specified. Configure the parameter based on the description of **Result preview** in the [Procedure](https://docs.byteplus.com/docs/tls/Use_the_Kafka_protocol_to_upload_logs#%E9%85%8D%E7%BD%AE%E6%AD%A5%E9%AA%A4) section. |
|invalid SASL/PLAIN request: Invalid projectId |The specified project ID does not exist. Verify whether the project ID is typed correctly. |
|Access Denied. You are not authorized to perform this operation. |The current user has no operation permissions. Verify the user permissions. |
