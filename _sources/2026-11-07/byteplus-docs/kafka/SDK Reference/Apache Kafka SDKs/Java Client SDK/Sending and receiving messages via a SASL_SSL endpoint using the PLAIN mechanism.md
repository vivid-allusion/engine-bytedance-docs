---
title: "Sending and receiving messages via a SASL_SSL endpoint using the PLAIN mechanism"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/Apache-Java-Sending-receiving-messages-SASL_SSL-PLAINuser"
---

Taking the Java client side as an example, this paper introduces how to access the message queue Kafka version through the SASL_SSL access point PLAIN mechanism in the VPC or public network environment, and send and receive messages.

<span id="55bf4a2d"></span>
## Prerequisite

Preparations have been completed. Please refer to [Preparations](https://docs.byteplus.com/en/docs/kafka/Apache-Java-SDK-Preparations) the detailed description.

<span id="3796ce32"></span>
## 1 Install Java dependencies

Java project `pom.xml` Add dependencies. Take Kafka 2.2.2 version as an example.

```XML
<dependency>
    <groupId>org.apache.kafka</groupId>
    <artifactId>kafka-clients</artifactId>
    <version>2.2.2</version>
</dependency>
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-log4j12</artifactId>
    <version>1.7.6</version>
</dependency>
```


<span id="7bdf209d"></span>
## 2 Add configuration file


1. Create message queue Kafka version profile `config.properties`.

   For a detailed description of the profile field, please refer to [Configuration file](https://docs.byteplus.com/en/docs/kafka/Apache-Java-Configuration-file).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Under the PLAIN mechanism, the PLAIN user with the corresponding Topic access permission should be used for SASL authentication. Please refer to <a href="https://docs.byteplus.com/en/docs/kafka/Apache-Java-SDK-Preparations">Preparations</a> the method of obtaining the username and password.   </div>
   

   When accessing through the SASL_SSL access point PLAIN mechanism, the configuration file example is as follows.

   ```YAML
   bootstrap.servers=xxxxx
   security.protocol=SASL_SSL
   topic=my-topic
   consumer.group.id=test
   consumer.auto.offset.reset=earliest
   consumer.enable.auto.commit=false
   client.dns.lookup=use_all_dns_ips
   sasl.mechanism=PLAIN
   sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="xxxx" password="xxxxx";
   ```
   

2. Create profile loader `KafkaConfigurer.java`.

   ```Java
   package com.byteplus.openservice.kafka;
   
   import java.io.FileInputStream;
   import java.io.InputStream;
   import java.util.Properties;
   
   public class KafkaConfigurer {
   
       private static Properties properties;
   
       public synchronized static Properties getKafkaProperties(String path) {
           if (null != properties) {
               return properties;
           }
           //Get content config.properties profile.
           Properties kafkaProperties = new Properties();
           try {
               FileInputStream conf = new FileInputStream(path);
               kafkaProperties.load(conf);
           } catch (Exception e) {
               //If it is not loaded into the file, the program should be exited.
               e.printStackTrace();
           }
           properties = kafkaProperties;
           return kafkaProperties;
       }
   }
   ```
   


<span id="95945444"></span>
## 3 Send a message

<span id="4dc30a4c"></span>
### Implementation method


1. Create a sending message program `ProducerDemo.java`.

2. Compile and run `ProducerDemo.java` Send a message.

3. Check the running results.

   An example of the running result is as follows.

   ```Shell
   Produce ok:sasl-0@0
   Produce ok:sasl-0@1
   Produce ok:sasl-0@2
   Produce ok:sasl-0@3
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Message queue Kafka edition <a href="https://docs.byteplus.com/en/docs/kafka/Apache-Java-SDK-overview">Demo</a> for your quick access, after downloading and decompressing the demo, you can directly execute the following command to send a message.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">   ```Shell
   java -cp bp-kafka-java-demo.jar com.byteplus.openservice.kafka.ProducerDemo ./ssl.config.properties
   ```
      </div>
   

<span id="f0fcd466"></span>
### Example code

The sample code for producing messages through the SASL_SSL access point PLAIN mechanism is as follows, you can also refer to the sample file in the demo `{DemoPath}/src/main/java/com/byteplus/openservice/kafka/ProducerDemo.java`, to implement the relevant business logic.

```Java
package com.byteplus.openservice.kafka;

import java.util.ArrayList;
import java.util.List;
import java.util.Properties;
import java.util.concurrent.Future;

import java.util.concurrent.TimeUnit;
import org.apache.kafka.clients.CommonClientConfigs;
import org.apache.kafka.clients.consumer.ConsumerConfig;
import org.apache.kafka.clients.consumer.ConsumerRecord;
import org.apache.kafka.clients.consumer.ConsumerRecords;
import org.apache.kafka.clients.consumer.KafkaConsumer;
import org.apache.kafka.common.config.SaslConfigs;
import org.apache.kafka.clients.producer.KafkaProducer;
import org.apache.kafka.clients.producer.ProducerConfig;
import org.apache.kafka.clients.producer.ProducerRecord;
import org.apache.kafka.clients.producer.RecordMetadata;
import org.apache.kafka.common.config.SslConfigs;

class Producer {
  
    private static String topic;
    private static Properties props  = new Properties();
    private static KafkaProducer<String, String> producer;

    // Producer constructor.
    public Producer(Properties kafkaProperties) {
        setProps(kafkaProperties);
        setSasl(kafkaProperties);
        setTopic(kafkaProperties);
        newProducer();
    }

    // Please apply in the console before using Topic.
    private void setTopic(Properties kafkaProperties) {
        topic  = kafkaProperties.getProperty("topic");
    }

    // Set up security protocols
    private void setSasl(Properties kafkaProperties) {
        String protocol = kafkaProperties.getProperty("security.protocol");
        props.put(CommonClientConfigs.SECURITY_PROTOCOL_CONFIG, protocol);

        // The configuration of the encryption type and SASL is required.
        if (protocol.equals("SASL_SSL")) {
            props.put(SaslConfigs.SASL_MECHANISM, kafkaProperties.getProperty("sasl.mechanism"));
            props.put(SaslConfigs.SASL_JAAS_CONFIG, kafkaProperties.getProperty("sasl.jaas.config"));
            return;
        }

        throw new IllegalArgumentException("security.protocol is not correct");
    }

    // Set the startup parameters for the producer.
    private void setProps(Properties kafkaProperties) {
        //To set up an access point, please obtain the access point of the corresponding topic through the console.
        props.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, kafkaProperties.getProperty("bootstrap.servers"));

        //Message serializer type.
        props.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringSerializer");
        props.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringSerializer");

        props.put(SslConfigs.SSL_ENDPOINT_IDENTIFICATION_ALGORITHM_CONFIG, "");
        
        //Maximum wait time for a request.
        props.put(ProducerConfig.MAX_BLOCK_MS_CONFIG, 30 * 1000);
        //Internal retry times in client.
        props.put(ProducerConfig.RETRIES_CONFIG, 5);
        // Internal retry interval in client.
        props.put(ProducerConfig.RECONNECT_BACKOFF_MS_CONFIG, 3000);
        //  Set the client's DNS policy.
        props.put(ProducerConfig.CLIENT_DNS_LOOKUP_CONFIG, kafkaProperties.getProperty("client.dns.lookup"));
    }

    // Construct a producer instance.
    private void newProducer() {
        // Construct the Producer object. Note that this object is thread-safe. In general, a Producer object can be used within a process.
        // If you want to improve performance, you can construct a few more objects, but not exceed 5.
        producer  = new KafkaProducer<String, String>(props);
    }

    public void Produce() {
      
        String value = "this is demo message "; //Message content.

        //Getting futures in batches can speed up, but be careful not to be too large in batches.
        List<Future<RecordMetadata>> futures = new ArrayList<Future<RecordMetadata>>(128);
        for (int i =0; i < 100; i++) {
            
            ProducerRecord<String, String> kafkaMessage =  new ProducerRecord<String, String>(topic, value + ": " + i);
            Future<RecordMetadata> metadataFuture = producer.send(kafkaMessage);
            futures.add(metadataFuture);
        }
        producer.flush();
        for (Future<RecordMetadata> future: futures) {
            //Synchronize the results of the Future object.
            try {
                RecordMetadata recordMetadata = future.get();
                System.out.println("Produce ok:" + recordMetadata.toString());
            } catch (Throwable t) {
                t.printStackTrace();
            }
        }
    }
}

public class ProducerDemo {

    public static void main(String args[]) {
        if (args.length < 1) {
            System.out.println("please input config path");
            return;
        }
        
        Producer producer = new Producer(KafkaConfigurer.getKafkaProperties(args[0]));

        try {
            producer.Produce();
        } catch (Exception e) {
            // After the client side retries internally, it still fails to send, and the business has to deal with such errors.
            System.out.println("error occurred");
            e.printStackTrace();
        }
    }


}
```


<span id="ee3e2361"></span>
## 4 Consumer messages

<span id="c7040d50"></span>
### Implementation method


1. Creating a Consumer Subscription Messaging Program `ConsumerDemo.java`.

2. Compile and run `ConsumerDemo.java`Consumption messages.

3. Check the running results.

   An example of the running result is as follows.


```Shell
Consume: ConsumerRecord(topic = sasl, patition = 6, leaderEpoch=0, offset=0, CreateTime = 1637207092476, serialized key size = -1, serialized key size = 24, headers = ReacordHeaders(headers = [], isReadOnly = false), key = null, value = this is demo, message : 0)
Consume: ConsumerRecord(topic = sasl, patition = 6, leaderEpoch=0, offset=0, CreateTime = 1637207092476, serialized key size = -1, serialized key size = 24, headers = ReacordHeaders(headers = [], isReadOnly = false), key = null, value = this is demo, message : 1)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Message queue Kafka version provides a sample demo for you to quickly access. After downloading and decompressing the demo, you can directly execute the following command to consume messages.</div>


<div data-tips="true" data-tips-type="tip">```Shell
java -cp bp-kafka-java-demo.jar com.byteplus.openservice.kafka.ConsumerDemo ./ssl.config.properties
```
</div>


<span id="2a7e3e5c"></span>
### Example code

The sample code for consuming messages through the SASL_SSL access point PLAIN mechanism is as follows, you can also refer to the sample file in the demo `{DemoPath}/src/main/java/com/byteplus/openservice/kafka/ConsumerDemo.java`, to implement the relevant business logic.

```Java
package com.byteplus.openservice.kafka;

import java.util.ArrayList;
import java.util.List;
import java.util.Properties;

import org.apache.kafka.clients.CommonClientConfigs;
import org.apache.kafka.clients.consumer.ConsumerConfig;
import org.apache.kafka.clients.consumer.ConsumerRecord;
import org.apache.kafka.clients.consumer.ConsumerRecords;
import org.apache.kafka.clients.consumer.KafkaConsumer;
import org.apache.kafka.clients.producer.ProducerConfig;
import org.apache.kafka.common.config.SaslConfigs;
import org.apache.kafka.common.config.SslConfigs;

class Consumer {
  
    private static Properties props  = new Properties();

    private KafkaConsumer<String, String> consumer;

    // Consumer constructor.
    public Consumer(Properties kafkaProperties) {
        setProps(kafkaProperties);
        setSasl(kafkaProperties);
        newConsumer();
        subscribed(kafkaProperties);
    }

    // Set up security protocols
    private void setSasl(Properties kafkaProperties) {
        String protocol = kafkaProperties.getProperty("security.protocol");
        props.put(CommonClientConfigs.SECURITY_PROTOCOL_CONFIG, protocol);

        // The configuration of the encryption type and SASL is required.
        if (protocol.equals("SASL_SSL")) {
            props.put(SaslConfigs.SASL_MECHANISM, kafkaProperties.getProperty("sasl.mechanism"));
            props.put(SaslConfigs.SASL_JAAS_CONFIG, kafkaProperties.getProperty("sasl.jaas.config"));
            return;
        }

        throw new IllegalArgumentException("security.protocol is not correct");
    }

    // Set the startup parameters for the consumer.
    private void setProps(Properties kafkaProperties) {
        //Set the startup parameters for the consumer.
        props.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, kafkaProperties.getProperty("bootstrap.servers"));

        props.put(SslConfigs.SSL_ENDPOINT_IDENTIFICATION_ALGORITHM_CONFIG, "");

        //This value can be set according to the actual pull message and customer processing time, etc. The default is 30s.
        props.put(ConsumerConfig.SESSION_TIMEOUT_MS_CONFIG, 30000);
        //Maximum number per poll.
        //// Be careful not to change the value too much. If the poll has too much data and cannot be consumed before the next poll, a load balance will be triggered, resulting in a card.
        props.put(ConsumerConfig.MAX_POLL_RECORDS_CONFIG, 30);
        //Message deserializer type.
        props.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringDeserializer");
        props.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringDeserializer");
        //The consumer group to which the current consumer instance belongs, please use it after applying in the console.
        //Consumer instances belonging to the same group will consume messages together.
        props.put(ConsumerConfig.GROUP_ID_CONFIG, kafkaProperties.getProperty("consumer.group.id"));
        props.put(ConsumerConfig.AUTO_OFFSET_RESET_CONFIG, kafkaProperties.getProperty("consumer.auto.offset.reset"));
        props.put(ConsumerConfig.ENABLE_AUTO_COMMIT_CONFIG, kafkaProperties.getProperty("consumer.enable.auto.commit"));
        // Set the client's DNS policy.
        props.put(ConsumerConfig.CLIENT_DNS_LOOKUP_CONFIG, kafkaProperties.getProperty("client.dns.lookup"));
    }

    // Construct a consumer instance.
    private void newConsumer() {
        consumer = new org.apache.kafka.clients.consumer.KafkaConsumer<String, String>(props);
    }

    // Subscribe topic.
    private void subscribed(Properties kafkaProperties) {
        //Set Topics for Consumer Group Subscriptions.
        List<String> subscribedTopic =  new ArrayList<String>();
        //If the GROUP_ID_CONFIG is the same, the subscribed topic is also recommended to be set to the same.
        //Topics need to be created in the console first.
        subscribedTopic.add(kafkaProperties.getProperty("topic"));
        consumer.subscribe(subscribedTopic);
    }

    // Consume message.
    public void poll() {
        ConsumerRecords<String, String> records = consumer.poll(1000);
        //The data must be consumed before the next poll and the total time must not exceed SESSION_TIMEOUT_MS_CONFIG.
        //It is recommended to create a separate thread pool to consume messages and return results asynchronously.
        for (ConsumerRecord<String, String> record : records) {
            System.out.printf("Consume: %s%n", record.toString());
        }
    }
}

public class ConsumerDemo {
    public static void main(String args[]) {
        if (args.length < 1) {
            System.out.println("please input config path");
            return;
        }

        Consumer consumer = new Consumer(KafkaConfigurer.getKafkaProperties(args[0]));

        //Consume message in infinite loop.
        while (true){
            try {
                consumer.poll();
            } catch (Exception e) {
                try {
                    Thread.sleep(1000);
                } catch (Throwable ignore) {

                }
                e.printStackTrace();
            }
        }
    }
}
```
