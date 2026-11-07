---
title: "Sending and receiving messages via the default endpoint"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/Apache-Go-Sending-receiving-messages-default"
---

This article takes the Go client side as an example to introduce how to access the message queue Kafka version through the default access point (PLAINTEXT) in the VPC environment and send and receive messages.

<span id="c1239d44"></span>
## Prerequisite

Preparations have been completed. Please refer to [Preparations](https://docs.byteplus.com/en/docs/kafka/Apache-Go-Preparations) the detailed description.

<span id="f64a1955"></span>
## 1 Add configuration file

Create message queue Kafka version profile `config.json`For a detailed description of the profile field, please refer to [SDK configuration](https://docs.byteplus.com/en/docs/kafka/Apache-Go-SDK-configuration).

When using the default access point, the configuration file example is as follows.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Please fill in the relevant parameters according to the comment prompts and delete the comment.</div>


```json
{
  "bootstrap.servers": "xxxxx", // Modify the configuration to set the default access point for the instance.
  "topic": "xxxx", // Modify the configuration to the name of the topic to be sent.
  "consumer": {
    "group.id": "xxxx" // Modify to the name of the specified consumer group.
  }
}
```


<span id="2e4c682f"></span>
## 2 Send a message

<span id="172b7781"></span>
### Implementation method


1. Create a message sender `producer.go`.

2. Compile and run `producer.go` Send a message.

3. Check the running results.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Message queue Kafka edition Demo for your quick access, after downloading and decompressing the demo, you can directly execute the following command to send and consume messages.</div>


<div data-tips="true" data-tips-type="tip">```Plain Text
go run -mod=vendor {DemoPath}/kafka_demo_main.go
```
</div>


<span id="eb6bd72b"></span>
### Example code

The sample code for producing messages through the default access point is as follows, or you can refer to the sample file in the demo `{DemoPath}/client/producer.go`, to implement the relevant business logic.

```go
package client

import (
   "fmt"
   "github.com/confluentinc/confluent-kafka-go/kafka"
)

func RunProduce(config *KafkaConf) error {
   // Get producer configuration object
   configMap := &kafka.ConfigMap{
      "bootstrap.servers": config.BootstrapServers,
      "security.protocol": config.Protocol,
      "acks":              config.Producer.Acks,
      "batch.size":        config.Producer.BatchSize,
   }

   if config.Debug {
      // Enable debug
      configMap.SetKey("debug", "ALL")
   }

   if config.Sasl.Enabled {
      //  Set SASL configurations     
      configMap.SetKey("sasl.mechanism", config.Sasl.Mechanism)
      configMap.SetKey("sasl.username", config.Sasl.UserName)
      configMap.SetKey("sasl.password", config.Sasl.Password)
   }


   // Create a new producer
   producer, err := kafka.NewProducer(configMap)
   if err != nil {
      return err
   }

   // Handle sender results
   go callBack(producer)()

   // Get sender channel
   sendChannel := producer.ProduceChannel()

   // Send 10 messages
   for count := 0; count < 10; count++ {
      // Construct one message
      msg := &kafka.Message{
         // Topic-partition that message is send to
         TopicPartition: kafka.TopicPartition{
            // Topic name
            Topic: &config.Topic,
            // Partition number. A fixed partition or an auto-selected(kafka.PartitionAny) partition can be set
            Partition: kafka.PartitionAny,
         },
         // Message value. Can be a nil object
         Value: []byte(fmt.Sprintf("Bytedance test msg %d", count)),
         // Message key. Can be a nil object. By default, messages will be sent to the same partition if theirs partitions are set to PartitionAny and keys are same.
         Key: []byte(fmt.Sprintf("Bytedance test key %d", count)),
         // Message attributes. Can be a nil object.
         Headers: []kafka.Header{
            {Key: "service", Value: []byte("kafka")},
            {Key: "version", Value: []byte("2.2.0")},
         },
      }

      // Send message to sender channel
      sendChannel <- msg
   }

   // Flush all messages to server before producer closing.
   producer.Flush(10000)
   // Close producer at last.
   producer.Close()
   return nil
}

// Callback method for sender results. This will never be called if Producer.Acks is equals with 0.
func callBack(p *kafka.Producer) func() {
   return func() {
      for event := range p.Events() {
         switch eType := event.(type) {
         case *kafka.Message:
            // Handler sender result
            if eType.TopicPartition.Error != nil {
               // Handle sender error
               fmt.Printf("Delivery failed: %v\n", eType.TopicPartition.Error)
            } else {
               // Handle sender success
               fmt.Printf("Delivered message to topic %s [%d] at offset %v\n",
                  *eType.TopicPartition.Topic, eType.TopicPartition.Partition, eType.TopicPartition.Offset)
            }
         }
      }
   }
}
```


<span id="b40d916f"></span>
## 3 Consumer messages

<span id="a2b6b60d"></span>
### Implementation method


1. Creating a Consumer Subscription Messaging Program `consumer.go`.

2. Compile and run `consumer.go` Consumption messages.

3. Check the running results.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Message queue Kafka version provides sample demos for you to quickly access. After downloading and unzipping the demo, you can directly execute the following commands to send and consume messages.</div>


<div data-tips="true" data-tips-type="tip">```Plain Text
go run -mod=vendor {DemoPath}/kafka_demo_main.go
```
</div>


<span id="73bf5bfe"></span>
### Message consumption example code

The sample code for consuming messages through the default access point is as follows, or you can refer to the sample file in the demo `{DemoPath}/client/consumer.go`, to implement the relevant business logic.

```go
package client

import (
   "fmt"
   "github.com/confluentinc/confluent-kafka-go/kafka"
   "strconv"
)

func RunConsumer(config *KafkaConf) error {
   // Get consumer configuration object
   configMap := &kafka.ConfigMap{
      "bootstrap.servers":  config.BootstrapServers,
      "security.protocol":  config.Protocol,
      "group.id":           config.Consumer.GroupId,
      "auto.offset.reset":  config.Consumer.AutoOffsetRest,
      "enable.auto.commit": strconv.FormatBool(config.Consumer.AutoCommit),
   }

   if config.Debug {
      // Enable debug
      if err := configMap.SetKey("debug", "ALL"); err != nil {
         return err
      }
   }

   if config.Sasl.Enabled {
      // Set SASL configurations
      configMap.SetKey("sasl.mechanism", config.Sasl.Mechanism)
      configMap.SetKey("sasl.username", config.Sasl.UserName)
      configMap.SetKey("sasl.password", config.Sasl.Password)
   }

   // Create a new consumer
   consumer, err := kafka.NewConsumer(configMap)
   if err != nil {
      return err
   }

   // Subscribe topics
   err = consumer.SubscribeTopics([]string{config.Topic}, nil)
   if err != nil {
      return err
   }

   // Read 10 messages
   for count := 0; count < 10; {
      // Retrieve message from server. Poll method should be called by period.
      event := consumer.Poll(1000)
      switch msg := event.(type) {
      case *kafka.Message:
         // Handle one message.
         // NOTICE: message handler SHOULD NOT take too longer time that would make consumer failed.
         handleMessage(msg)
         count++
      }
   }

   if !config.Consumer.AutoCommit {
      // Commit consumer offsets manually.
      tps, err := consumer.Commit()
      if err != nil {
         fmt.Printf("Commit offsets failed. %s\n", err.Error())
      } else {
         fmt.Printf("Offset commited: \n")
         for _, tp := range tps {
            fmt.Printf("\t%s-%d: %d", *tp.Topic, tp.Partition, tp.Offset)
         }
      }
   }

   // Close consumer at last.
   return consumer.Close()
}

// Handle one message.
func handleMessage(msg *kafka.Message) {
   fmt.Printf("Consumed a message from topic %s [%d] at offset %d. key: (%s), value: (%s), Headers: ",
      *msg.TopicPartition.Topic, msg.TopicPartition.Partition, msg.TopicPartition.Offset, msg.Key, msg.Value)
   if msg.Headers != nil {
      fmt.Printf("(")
      for _, header := range msg.Headers {
         fmt.Printf("%s->%s,", header.Key, header.Value)
      }
      fmt.Printf(")")
   }
   fmt.Printf("\n")
}
```
