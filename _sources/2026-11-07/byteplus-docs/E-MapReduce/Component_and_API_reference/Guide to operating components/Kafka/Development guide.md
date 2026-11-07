---
title: "Development guide"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/kafka_development_guide"
---

<span id="java-依赖库"></span>
## **Java dependencies**

```xml
<dependency>
    <groupId>org.apache.kafka</groupId>
    <artifactId>kafka-clients</artifactId>
    <version>2.2.0</version>
</dependency>
```


<span id="发送消息"></span>
## **Send messages**

```java
//View the corresponding endpoint information in the console String server = "xxx.";
//Topic of the message, applied for in the console String topic = "this is your topic.";
//Test message content String value = "this is test message value.";
//Number of messages to send int count = 100;
Properties properties = new Properties();
properties.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, server);
properties.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, StringSerializer.class);
properties.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, StringSerializer.class);
KafkaProducer<String, String> producer = new KafkaProducer<>(properties);
try {
    for (int i = 0; i < count; i++) {
        RecordMetadata recordMetadata = producer.send(new ProducerRecord<>(topic, value + i++))
                .get(5, TimeUnit.SECONDS);
        logger.info("recordMetadata topic={}, partition={}, offset={}, count = {}.",
                recordMetadata.topic(),
                recordMetadata.partition(),
                recordMetadata.offset(),
                i);
    }
} catch (Throwable e) {
    logger.error("produce error", e);
}
producer.flush();
producer.close();
```


<span id="消费消息"></span>
## **Consume messages**

```java
//View the corresponding endpoint information in the console String server = "xxx.";
//Topic of the message, applied for in the console String topic = "this is your topic.";
//Consumer group, applied for in the console String group = "this is your group.";
//Offset reset strategy: earliest, latest, none String offsetReset = "earliest";
Properties properties = new Properties();
properties.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, server);
properties.put(ConsumerConfig.GROUP_ID_CONFIG, group);
properties.put(ConsumerConfig.AUTO_OFFSET_RESET_CONFIG, offsetReset);
properties.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class);
properties.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class);

KafkaConsumer<String, String> consumer = new KafkaConsumer<String, String>(properties);
List<String> topicList = Lists.newArrayList(topic);
consumer.subscribe(topicList);
while (true) {
    try {
        ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(500));
        for (ConsumerRecord<String, String> record : records) {
            logger.info("consumed record, topic={}, partition={}, offset={}, key={}, value={}",
                    record.topic(),
                    record.partition(),
                    record.offset(),
                    record.key(),
                    record.value());
        }
    } catch (Exception e) {
        logger.error("consume error", e);
    }
}
```
