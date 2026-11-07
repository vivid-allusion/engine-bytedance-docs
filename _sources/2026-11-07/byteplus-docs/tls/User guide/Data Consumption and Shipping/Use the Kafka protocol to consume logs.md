---
title: "Use the Kafka protocol to consume logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/use_the_kafka_protocol_to_consume_logs"
---

Torch Log Service (TLS) offers the feature of using the Kafka protocol for consumption to consume a topic as a Kafka topic. This topic describes how to use the Kafka protocol to consume log data.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

TLS allows you to enable the feature of using the Kafka protocol for consumption for a specific topic. After the feature is enabled, the specified topic can be consumed as a Kafka topic and each log entry corresponds to a Kafka message. After your business is connected to TLS using the open\-source Kafka SDK, use Kafka Consumer to consume log data collected to a specific topic in downstream big data components or data repositories. This feature is applicable to stream computing and big data storage scenarios.

When using the Kafka protocol to consume logs, logs can be consumed by consumers and consumer groups. One consumer group can consume multiple topics in the same project, but cannot consume data across projects.

<span id=".6ZmQ5Yi26K-05piO"></span>
## Limits


* The Kafka client version that supports the feature of using the Kafka protocol for consumption ranges from 0.11.x through 2.0.x.

* If the feature of using the Kafka protocol for consumption is enabled, you can consume log data collected to the server during the running period of Kafka Consumer.

* You can use open\-source Kafka SDK for Java to consume log data. For the sample code, refer to [Sample code](https://docs.byteplus.com/docs/tls/use_the_kafka_protocol_to_consume_logs#.56S65L6L5Luj56CB). You can also use the Kafka plug\-in of Spark Streaming or Flink to connect to TLS. For more information, refer to [Use Spark Streaming to consume logs](https://docs.byteplus.com/docs/tls/use_spark_streaming_to_consume_logs) and [Use Flink to consume logs](https://docs.byteplus.com/docs/tls/use_flink_to_consume_logs).

* To secure the transmission of logs, use the SASL_SSL protocol. The username is the project ID and the password is the AccessKey pair of your BytePlus account. For more information, refer to [Sample code](https://docs.byteplus.com/docs/tls/use_the_kafka_protocol_to_consume_logs#.56S65L6L5Luj56CB).

* If a topic has multiple shards, TLS does not guarantee consumption in order. We recommend that you upload logs in load balancing mode.


<span id=".6LS555So6K-05piO"></span>
## Cost information

When you consume logs, read traffic over an internal network or read traffic over the internet is generated.


* Read traffic over an internal network: Assume that you use the Kafka protocol to consume log data in other BytePlus private network services. If the source topic and the consumer client belong to the same Region, you can use a private network to transfer data. In this case, read traffic over an internal network incurs fees. When you use Kafka to consume log data in self\-managed applications in Elastic Compute Service (ECS), you are charged for the traffic of the corresponding private network.

* Read traffic over the internet: When you use the Kafka protocol to consume log data in external applications on the internet, you must transfer data over the internet. In this case, read traffic over the internet is generated. For example, source data is in a specific topic of TLS. When you use Kafka to consume log data in self\-developed applications in self\-managed data centers, read traffic over the internet is generated.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the source topic and the consumer client belong to different Regions, you must transfer data over the internet. In this case, read traffic over the internet is generated.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Before you begin


* Activate TLS, create projects and topics, and collect log data. For more information, refer to [Getting Started Overview](https://docs.byteplus.com/docs/tls/getting_started_overview).

* Make sure that the current account has permission to enable the feature of using the Kafka protocol for consumption, that is, the permission to access the `ConsumeLogs` API. For more information, refer to [Authorizable actions](https://docs.byteplus.com/docs/tls/Authorizable_actions).


<span id="47e5a3be"></span>
## Procedure

<span id=".XzEt5byA5ZCva2Fma2HmtojotLnlip_og70="></span>
### 1 Enable the feature of using the Kafka protocol for consumption

Before you use various tools to consume log data using the Kafka protocol, enable the feature of using the Kafka protocol for consumption for a specific topic.


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Resource management** \> **Project**.

3. On the **Project** page, locate the specified project and click the project name.

4. In the **Log topic** section, find the specified log topic in the log topic list.

   * Click the **Kafka protocol consumption** switch in the log topic list.

   * Click the log topic name and select ... \> **Configure log consumption**.

5. In the pop\-up dialog box, enable Kafka consumption protocol configuration, and then click **OK**. 

   
   |Parameters |Description |
   |---|---|
   |Compression type |Configure the compression type for consumed data; supported options include lz4, snappy, gzip, and no compression. |
   |Consumptionformat |Configure the format of consumed data.<br><br><br>* original content: Consume data in raw format.<br><br>* JSON: Consume data in JSON format; field\-specific consumption is also supported.<br><br>   * Escape mode:<br><br>      * Do not escape: output data as collected by log collection.<br><br>      * Escape: add escape characters to values of top\-level nodes.<br><br>      ```YAML```<br>```      Original log: { "a": "aa", "b": { "b1": "b1b1", "c1": "c1c1" } }```<br>```      Consumption result：```<br>```          No escaping: { "a": "aa", "b": { "b1": "b1b1", "c1": "c1c1" } } ```<br>```          Escaping: { "a": "aa", "b": "{\"b1\":\"b1b1\", \"c1\":\"c1c1\"}" }```<br>```      ```<br>      <br><br>   * Consumable log fields: You can customize fields to consume. By default, all fields are selected. Supported fields are as follows:<br><br>      `__content__`(can not be canceled), `__source__`, `__path__`, `__context_flow__`, `tags`. |
   

   * After successfully enabling the Kafka protocol consumption feature, the details page of this log topic will display consumption parameters like username, hosts, topics. etc. 

   * You can enable the Kafka protocol consumption feature again after it has been disabled for 2 minutes.


<span id=".XzIt6YCa6L-HLWthZmthLeWNj-iurua2iOi0ueaXpeW_lw=="></span>
### 2 Use the Kafka protocol to consume logs

Currently, TLS allows you to use Kafka SDK for Java or the Kafka Connector plug\-in of frameworks such as Spark and Flink to consume log data. Refer to the following table to configure Kafka parameters and refer to the sample code to consume log data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Starting the feature of using the Kafka protocol for consumption takes about 30 seconds. We recommend that you consume logs after you start it 30 seconds later.</div>


<span id=".6YWN572u5pa55byP"></span>
#### Parameters

To use the Kafka protocol to consume logs, configure the following parameters.


|Parameter |Description |
|---|---|
|Connection type |To secure the transmission of logs, use the SASL_SSL protocol. The username is the project ID and the password is the AccessKey pair of your BytePlus account. For more information, refer to [Sample code](https://docs.byteplus.com/docs/tls/use_the_kafka_protocol_to_consume_logs#.56S65L6L5Luj56CB). |
|username |The Kafka Simple Authentication and Security Layer (SASL) username. Set it to the TLS project ID. |
|password |The Kafka SASL user password. Set it to the AccessKey pair of your BytePlus account,<br><br>in the format of `${access-key-id}#${access-key-secret}`, where:<br><br><br>* `${access-key-id}`: Replace it with your AccessKey ID.<br><br>* `${access-key-secret}`: Replace it with your AccessKey secret.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">We recommend that you use the AccessKey ID of an Identity and Access Management (IAM) user who is granted the permission to call <code>ConsumeLogs</code>. For more information, refer to <a href="https://docs.byteplus.com/docs/tls/Authorizable_actions">Authorizable actions</a>.</div><br> |
|hosts |The cluster address for the initial connection. The value is in the `ENDPOINT:PORT_NUMBER` format, such as `tls-ap-southeast-1.ibytepluses.com:9093`.<br><br><br>* The endpoint is the endpoint of TLS in the current Region. Select the correct endpoint based on the Region and network type. For more information, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint).<br><br>* The port number is fixed to 9093.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In hosts, <code>https://</code> is not required for the endpoint.</div><br> |
|topic |Specify the topic ID for consumption using the Kafka protocol, in the format of **`out-log topic ID`**, such as `out-0fdaa6b6-3c9f-424c-8664-fc0d222c****`.<br><br>Alternatively, on the topic details page in the TLS console, view and copy **Kafka protocol consumer topic ID**. |


<span id=".6ZSZ6K-v5L-h5oGv"></span>
#### Error messages

If an error occurs while using the Kafka protocol to upload logs, the error message is returned based on the Kafka error code. For more information, refer to the Kafka [error list](https://kafka.apache.org/20/javadoc/org/apache/kafka/common/errors/package-summary.html?spm=a2c4g.11186623.0.0.79f84e8daAFDQC).

In addition, TLS encapsulates error messages related to authentication and configuration parameters in the Java Kafka error code `SASLAuthenticationException`. The following table describes the error messages:


|Error Message |Description |
|---|---|
|invalid SASL/PLAIN request: expected 3 tokens |The user or password is not specified. Refer to [Configuration methods](https://docs.byteplus.com/docs/tls/use_the_kafka_protocol_to_consume_logs#.6YWN572u5pa55byP) to specify the username or password. |
|invalid SASL/PLAIN request: empty projectId |The user is not specified. Refer to [Configuration methods](https://docs.byteplus.com/docs/tls/use_the_kafka_protocol_to_consume_logs#.6YWN572u5pa55byP) to specify the username or password. |
|invalid SASL/PLAIN request: Password format wrong |The password format is incorrect. Refer to [Configuration methods](https://docs.byteplus.com/docs/tls/use_the_kafka_protocol_to_consume_logs#.6YWN572u5pa55byP) to specify the username or password. |
|invalid SASL/PLAIN request: empty AccessKey |The AccessKey ID is not specified. Refer to [Configuration methods](https://docs.byteplus.com/docs/tls/use_the_kafka_protocol_to_consume_logs#.6YWN572u5pa55byP) to specify the username or password. |
|invalid SASL/PLAIN request: empty SecretKey |The AccessKey secret is not specified. Refer to [Configuration methods](https://docs.byteplus.com/docs/tls/use_the_kafka_protocol_to_consume_logs#.6YWN572u5pa55byP) to specify the username or password. |
|invalid SASL/PLAIN request: Invalid projectId |The specified project ID does not exist. Verify whether the project ID is typed correctly. |
|Not allow consume, please open kafka consumer |The feature of using the Kafka protocol for consumption is not enabled for the specified topic. For more information, refer to [1 Enable the feature of using the Kafka protocol for consumption](https://docs.byteplus.com/docs/tls/use_the_kafka_protocol_to_consume_logs#.XzEt5byA5ZCva2Fma2HmtojotLnlip_og70=). |
|Access Denied. You are not authorized to perform this operation. |The current user has no operation permissions. Verify the user permissions. |


<span id=".56S65L6L5Luj56CB"></span>
#### Sample code

<span id=".6YCa6L-HLWthZmthLWphdmEtc2RrLea2iOi0ueaXpeW_lw=="></span>
##### UseKafka SDK for Java to consume logs

With simple parameter configurations, you can use various Kafka Producer SDKs to consume data collected to TLS. The relevant dependency and sample code for using Kafka SDK for Java to consume logs are as follows:


1. Add the dependency.

   Add the kafka\-clients dependency to the pom.xml file.

   ```xml
   <dependency>
       <groupId>org.apache.kafka</groupId>
       <artifactId>kafka-clients</artifactId>
       <version>2.2.2</version>
   </dependency>
   ```
   

2. Consume logs.

   Refer to the following sample code to consume logs using Kafka SDK for Java.

   ```java
   package org.kafka;
   
   import java.util.*;
   import java.util.concurrent.CountDownLatch;
   
   import org.apache.kafka.clients.CommonClientConfigs;
   import org.apache.kafka.clients.admin.*;
   import org.apache.kafka.clients.consumer.ConsumerRecord;
   import org.apache.kafka.clients.consumer.ConsumerRecords;
   import org.apache.kafka.clients.consumer.KafkaConsumer;
   import org.apache.kafka.common.config.SaslConfigs;
   import org.apache.kafka.common.serialization.StringDeserializer;
   
   
   public class KafkaConsumeTest implements Runnable {
       
       private final KafkaConsumer<String, String> consumer;
       private ConsumerRecords<String, String> msgList;
       private final String topic;
       private static final String GROUPID = "MY_GROUP_ID";
       private KafkaAdminClient adminClient;
       private String consumeName;
       
       public KafkaConsumeTest(String topicName,String consumeName) {
           // consumeName
           this.consumeName = consumeName;
           // projectid
           String userName = "${projectId}";
           // The AccessKey pair of a BytePlus account or an IAM user with the relevant permissions. Security token service (STS) tokens are not supported.
           String passWord = "${access-key-id}#${access-key-secret}";
           Properties props = new Properties();
           props.put("bootstrap.servers", "${hosts}"); //The consumption address. For more information, refer to Parameter description.
           props.put("group.id", GROUPID);// The consumer group name, length of 1 to 256 characters.
           props.put("enable.auto.commit", "true");
           props.put("auto.commit.interval.ms", "1000");
           props.put("session.timeout.ms", "30000");
           props.put("auto.offset.reset", "earliest");
           props.put("key.deserializer", StringDeserializer.class.getName());
           props.put("value.deserializer", StringDeserializer.class.getName());
           props.put(CommonClientConfigs.SECURITY_PROTOCOL_CONFIG, "SASL_SSL");
           props.put(SaslConfigs.SASL_MECHANISM, "PLAIN");
           props.put(SaslConfigs.SASL_JAAS_CONFIG,
                   "org.apache.kafka.common.security.plain.PlainLoginModule " +
                           "required username=\"" + userName + "\" password=\"" + passWord + "\";");
           
           this.consumer = new KafkaConsumer<String, String>(props);
           this.topic = topicName;
           this.consumer.subscribe(Arrays.asList(topic));
           this.adminClient = (KafkaAdminClient) KafkaAdminClient.create(props);
       }
       
       @Override
       public void run() {
           int messageNo = 1;
           System.out.println("---------Start consumption---------");
           try {
               while(true) {
                   msgList = consumer.poll(10);
                   
                   if(null!=msgList&&msgList.count()>0){
                       for (ConsumerRecord<String, String> record : msgList) {
                           System.out.println(this.consumeName+"==="+messageNo+" offset==="+record.offset()+"=======receive: key = " + record.key() + ", value = " +
                                   record.value());
                           messageNo++;
                       }
                   } else{
                       Thread.sleep(10);
                   }
               }
           } catch (Exception e) {
               e.printStackTrace();
           } finally {
               consumer.close();
           }
       }
       
       public static void main(String args[]) throws InterruptedException {
           CountDownLatch countDownLatch = new CountDownLatch(1);
           // ${out-TopicID} is the ID of the topic to be consumed using the Kafka protocol. The format is out+TOPIC_ID, such as out-0fdaa6b6-3c9f-424c-8664-fc0d222c****. 
           KafkaConsumeTest test1 = new KafkaConsumeTest("${out-TopicID}","Consume1");
           Thread thread1 = new Thread(test1);
           thread1.start();
           countDownLatch.await();
       }
   }
   ```
   


<span id=".6YCa6L-HLWthZmthLWdvLXNkay3mtojotLnml6Xlv5c="></span>
##### Use Kafka SDK for Go to consume logs

With simple parameter configurations, you can use various Kafka Producer SDKs to consume data collected to TLS. The relevant dependency and sample code for using Kafka SDK for Go to consume logs are as follows:


1. Run the following command to install Sarama.

   ```plain
   go get github.com/Shopify/sarama@v1.38.1
   ```
   

2. Import the required dependency packages such as Sarama to consume logs.

   Refer to the following sample code to consume logs using Kafka SDK for Go.

   ```go
   package kafka_consume_example
   
   import (
      "context"
      "fmt"
   
      "github.com/Shopify/sarama"
   )
   
   type exampleConsumerGroupHandler struct{}
   
   func (exampleConsumerGroupHandler) Setup(_ sarama.ConsumerGroupSession) error   { return nil }
   func (exampleConsumerGroupHandler) Cleanup(_ sarama.ConsumerGroupSession) error { return nil }
   func (h exampleConsumerGroupHandler) ConsumeClaim(sess sarama.ConsumerGroupSession, claim sarama.ConsumerGroupClaim) error {
      for msg := range claim.Messages() {
         fmt.Printf("Message topic:%q partition:%d offset:%d message:%s\n", msg.Topic, msg.Partition, msg.Offset, msg.Value)
         sess.MarkMessage(msg, "")
         sess.Commit()
      }
      return nil
   }
   
   func ExampleConsumerGroup() {
      config := sarama.NewConfig()
      config.Version = sarama.V2_0_0_0 // specify appropriate version
      config.ApiVersionsRequest = true
      config.Consumer.Return.Errors = true
      config.Net.SASL.Mechanism = "PLAIN"
      config.Net.SASL.Version = int16(0)
      config.Net.SASL.Enable = true
      config.Net.TLS.Enable = true
      config.Consumer.Offsets.Initial = sarama.OffsetNewest
      // projectId
      config.Net.SASL.User = "${projectId}"
      // The AccessKey pair of a BytePlus account or an IAM user with the relevant permissions. Security token service (STS) tokens are not supported.
      config.Net.SASL.Password = "${access-key-id}#${access-key-secret}"
      // The "hosts" indicates the consumption address. For more information, refer to Parameter description. The "my-group" indicates the consumer group name, length of 1 to 256 characters.
           props.put("enable.auto.commit", "true");
      group, err := sarama.NewConsumerGroup([]string{"${hosts}"}, "my-group", config)
      if err != nil {
         panic(err)
      }
      defer func() { _ = group.Close() }()
   
      // Track errors
      go func() {
         for err := range group.Errors() {
            fmt.Println("ERROR", err)
         }
      }()
   
      // Iterate over consumer sessions.
      ctx := context.Background()
      for {
         // ${out-TopicID} is the ID of the topic to be consumed using the Kafka protocol. The format is out+TOPIC_ID, such as out-0fdaa6b6-3c9f-424c-8664-fc0d222c****.
         topics := []string{"${out-TopicID}"}
         handler := exampleConsumerGroupHandler{}
   
         // `Consume` should be called inside an infinite loop, when a
         // server-side rebalance happens, the consumer session will need to be
         // recreated to get the new claims
         err := group.Consume(ctx, topics, handler)
         if err != nil {
            panic(err)
         }
      }
   }
   ```
   


<span id="8151aeff"></span>
## Related actions

<span id="57bc9c29"></span>
### View consumer groups

After consuming log data through the Kafka Java SDK or the Kafka Connector plug\-in of frameworks such as Spark or Flink, you can view consumer group information on the TLS console.


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top navigation bar, select the region where the TLS is located.

3. In the left\-side navigation pane, choose **Data Processing** \> **Log consumption**.

4. In the **Kafka** tab, locate and expand the project to which the target kafka consumer group belongs, and then click the specified kafka consumer group.

5. View the consumption information corresponding to the target consumer group.


<span id="73da8137"></span>
### Reset check points

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Please close the process first before resetting the check points.</div>


After you consume log data through the Kafka Java SDK or the Kafka Connector plug\-in for frameworks like Spark or Flink, you can reset consumption check points on the TLS console. You can also consume historical data by resetting the consumption check point.


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top navigation bar, select the region where the TLS is located.

3. In the left\-side navigation pane, choose **Data Processing** \> **Log consumption**.

4. In the **Kafka** tab, locate and expand the project to which the target kafka consumer group belongs, and then click the specified kafka consumer group.

5. Resets the consumption check point.

   1. In the upper right corner of the **Log Topics List** tab, click **Reset Consumption check point** , or in the **Action** column for the specified Shard, click **Reset Consumption check point**.

   2. Select a reset location.

      
      |Reset position |Description |
      |---|---|
      |**earliest location** |Start consuming the first piece of data on the topic. |
      |**latest location** |Skip all historical data and start consuming directly from the most recently written piece of data on the topic. |
      |**specified time point** |From a specified point in time in the past, the optional time range depends on how long the log topic is stored. |
      

   3. Click **OK** .


<span id="2f4fa339"></span>
### View the monitoring dashboard

After log data consumption through the Kafka Java SDK or the Kafka Connector plug\-in for frameworks like Spark or Flink, you can see trends in consumption group latency and consumption speed on the TLS console.


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top navigation bar, select the region where the TLS is located.

3. In the left\-side navigation pane, choose **Data Processing** \> **Log consumption**.

4. In the **Kafka** tab, locate and expand the project to which the target kafka consumer group belongs, and then click the specified kafka consumer group.

5. In the **Monitor Kanban** tab, view the consumer\-related dashboards.

   The dashboard displays the consumption latency, consumption speed, and related trends of the Kafka consumer group. For more information, please refer to [Visualization of Kafka Protocol Consumption Metrics](https://docs.byteplus.com/docs/tls/Visualization-of-Kafka-Protocol-Consumption-Metrics).
