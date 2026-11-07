---
title: "Consuming Volcano Engine Proto subscription data via Kafka"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Consuming_Proto_subscription_data_via_Kafka"
---

DTS supports using Kafka clients to consume BytePlus Proto subscription data via RocketMQ. This topic uses subscribing to an RDS for MySQL instance as an example to describe how to use the Go, Java and Python languages to consume Canal format data.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have installed [protoc](https://github.com/protocolbuffers/protobuf/releases). We recommend using protoc 3.18 or a higher version.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can run <code>protoc -version</code> to check the protoc version.   </div>
   

* The client used to subscribe to and consume data needs to specify the Kafka version number of the server. The version number must be 2.2.x (for example, 2.2.2). You can specify the Kafka version number in the example code. The specific parameters are shown in the following table.

   
   |**Runtime language** |**Description** |
   |---|---|
   |Go |Use the parameter `config.Version` in the code example to specify the Kafka version number of the server. |
   |Python |Specify the server's Kafka version number through the parameter `api_version` in the example code. |
   |Java |Specify the server's Kafka version number through the parameter `version` in the `maven pom.xml` file. |
   

* Install the runtime language environment as required.

   
   |**Runtime language** |**Description** |
   |---|---|
   |**Go** |To install [Go](https://go.dev/), Go 1.13 or above is required. You can run `go version` to view the Go version. |
   |**Python** |1. To install [Python](https://www.python.org/), Python 2.7 or above is required. You can run `python --version` to view the Python version.<br><br>2. Run the following commands in sequence to install pip dependencies.<br><br>   ```python```<br>```   pip install kafka-python```<br>```   ```<br>   <br><br>   ```python```<br>```   pip install protobuf```<br>```   ```<br>   <br><br>   ```python```<br>```   pip install python-snappy```<br>```   ```<br>    |
   |**Java** |1. Install [Java](https://www.oracle.com/java/technologies/downloads/). Java 1.8 or later is required. You can run `java -version` to view the Java version.<br><br>2. Install [maven](https://maven.apache.org/). Maven 3.8 or later is required. You can run` mvn -version` to view the Maven version.<br><br>3. In IDEA software, click **Create New Project** to create a Project.<br><br>4. Add the following dependencies to the project object model file `pom.xml` in the newly created Project. This example uses Kafka version 2.2.2. At the same time, you can also modify the version of` kafka-clients` in the `pom.xml` file to another version.<br><br>   ```xml```<br>```   <dependency>```<br>```     <groupId>org.apache.kafka</groupId>```<br>```     <artifactId>kafka-clients</artifactId>```<br>```     <version>2.2.2</version>```<br>```   </dependency>```<br>```   <dependency>```<br>```     <groupId>com.github.daniel-shuy</groupId>```<br>```     <artifactId>kafka-protobuf-serde</artifactId>```<br>```     <version>2.2.0</version>```<br>```   </dependency>```<br>```   <dependency>```<br>```     <groupId>org.xerial.snappy</groupId>```<br>```     <artifactId>snappy-java</artifactId>```<br>```     <version>1.1.8.4</version>```<br>```   </dependency>```<br>```   <dependency>```<br>```     <groupId>com.google.protobuf</groupId>```<br>```     <artifactId>protobuf-java</artifactId>```<br>```     <version>3.22.2</version>```<br>```   </dependency>```<br>```   ```<br>    |
   


<span id=".5YWz6IGULWthZmthLeWSjOiuoumYheS7u-WKoQ=="></span>
## Associate Kafka with the subscription task

This topic uses the macOS operating system as an example to describe how to associate Kafka with a subscription task.


1. Log in to the [DTS console](https://console.byteplus.com/dts) to create and configure a data subscription channel. For more information, refer to [Subscription solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_subscription_solutions).

2. Add a new consumer group in the destination data subscription channel. For details, refer to [Create new consumer group](https://docs.byteplus.com/en/docs/DTS/adding_a_consumer_group).

3. Select a [Java consumption example ](https://github.com/volcengine/volc-sdk-java/tree/main/example/src/main/java/com/volcengine/example/dts/volc)or a [Python consumption example](https://github.com/volcengine/volc-sdk-python/tree/main/volcengine/example/dts/subscription/volc) as required. The directories of the Python and Java consumption examples are as follows:

   ```mixin-react
   const list = [
       {
       "lang": "Python 语言",
       "text": `.
   ├── dts_kafka_consumer_demo.py    # 消费 Demo 文件
   ├── volc.proto                    # BytePlus格式文件
   └── volc_pb2.py                   # 编译 Volc.proto 后的生成的 Python 文件
     `},
     {
       "lang": "Java 语言",
       "text": `.
   ├── DTSKafkaConsumerDemo.java    # 消费 Demo 文件
   ├── Volc.java                    # 编译 Volc.proto 后的生成的 Java 文件
   └── Volc.proto                   # BytePlus格式文件
   `, 
     },
   ]
   return (<PreCodeTabs list={list} />);
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The Go language contains only one Demo file.   </div>
   

4. Modify the Demo file as required. The specific code is as follows.

   
   |**Name** |**Description** |**Example** |
   |---|---|---|
   |`GROUP` |Consumer group name |`285fef6b91754d0bbaab32e4976c****:test_dtssdk` |
   |`USER` |Kafka username. |`test_user` |
   |`PASSWORD` |Kafka users Password. |`Test@Pwd` |
   |`TOPIC` |The topic of the target DTS data subscription channel. |`d73e98e7fa9340faa3a0d4ccfa10****` |
   |`BROKERS` |Private network address of the target DTS data subscription channel. |`kafka-cndvhw9ves******.kafka.ivolces.com:9092` |
   

   ```mixin-react
   const list = [
     {
       "lang": "Go 语言",
       "text": `package main
   
   import (
      "context"
      "fmt"
      "log"
      "strings"
      "sync"
   
      "github.com/Shopify/sarama"
      proto "github.com/volcengine/volc-sdk-golang/example/dts/data-subscription-demo/proto"
      protobuf "google.golang.org/protobuf/proto"
   )
   
   type Handler struct {
      topic          string
      partitionCount map[int32]int
      totalCount     int
      mu             sync.Mutex
   }
   
   type Config struct {
      username string
      password string
      topic    string
      group    string
      brokers  string
   }
   
   var (
      c Config
   )
   
   func init() {
      c.brokers = "your brokers addrress"
      c.topic = "your topic"
      c.group = "your group"
      c.username = "your username"
      c.password = "your password"
   }
   
   func (h *Handler) Setup(session sarama.ConsumerGroupSession) error {
      fmt.Println("setup")
      return nil
   }
   
   func (h *Handler) Cleanup(sarama.ConsumerGroupSession) error {
      fmt.Println("clean up")
      return nil
   }
   
   func (h *Handler) ConsumeClaim(session sarama.ConsumerGroupSession, claim sarama.ConsumerGroupClaim) error {
      fmt.Println("ConsumeClaim")
      for m := range claim.Messages() {
         h.handleMsg(m)
         session.MarkMessage(m, "")
         session.Commit()
      }
      return nil
   }
   
   func (h *Handler) handleMsg(msg *sarama.ConsumerMessage) {
      h.mu.Lock()
      defer h.mu.Unlock()
      h.totalCount++
      h.partitionCount[msg.Partition]++
      entry := &proto.Entry{}
      if err := protobuf.Unmarshal(msg.Value, entry); err != nil {
         panic(err)
      }
      fmt.Println("-------------- handle message --------------")
      fmt.Printf("get message EventType:%v\n", entry.EntryType.String())
      switch entry.GetEntryType() {
      case proto.EntryType_DDL:
         event := entry.GetDdlEvent()
         fmt.Printf("ddl %v\n", event.Sql)
      case proto.EntryType_DML:
         event := entry.GetDmlEvent()
         cols := event.ColumnDefs
         for _, row := range event.Rows {
            var before, after []string
            for i, col := range row.BeforeCols {
               before = append(before, fmt.Sprintf("%+v[%+v]", cols[i].GetName(), col.GetValue()))
            }
            for i, col := range row.AfterCols {
               after = append(after, fmt.Sprintf("%+v[%+v]", cols[i].GetName(), col.GetValue()))
            }
            fmt.Printf("get row before=%v after=%v\n", before, after)
         }
      }
      fmt.Printf("fetch message partition=%v key=%v\n", msg.Partition, string(msg.Key))
      fmt.Printf("count partition-count=%v total-count=%v\n", h.partitionCount, h.totalCount)
   }
   
   func main() {
      fmt.Printf("config: %+v", c)
      config := sarama.NewConfig()
      config.Net.SASL.User = c.username
      config.Net.SASL.Password = c.password
      config.Net.SASL.Enable = true
      config.Consumer.Offsets.Initial = sarama.OffsetNewest
      config.Version = sarama.V2_2_2_0
      topic := c.topic
      group := c.group
      addr := strings.Split(c.brokers, ",")
      cons, err := sarama.NewConsumerGroup(addr, group, config)
      if err != nil {
         panic(err)
      }
      defer cons.Close()
      handler := &Handler{
         topic:          topic,
         partitionCount: make(map[int32]int),
      }
      for {
         err = cons.Consume(context.Background(), []string{handler.topic}, handler)
         if err != nil {
            log.Fatalln(err)
         }
      }
   }
   `,
       "selected": true,
     },
     {
       "lang": "Python 语言",
       "text": `
   from kafka import KafkaConsumer
   
   import volc_pb2
   
   if __name__ == '__main__':
           brokers = "your brokers address"
           topic = "your topic"
           group = "your group"
           username = "your username"
           password = "your password"
   
           # create consumer
           consumer = KafkaConsumer(
                   topic,
                   group_id=group,
                   # init consume offset
                   auto_offset_reset='latest',
                   enable_auto_commit=True,
                   # set up SASL authentication
                   security_protocol="SASL_PLAINTEXT",
                   sasl_mechanism="PLAIN",
                   sasl_plain_username=username,
                   sasl_plain_password=password,
                   api_version=(2, 2, 2),
                   bootstrap_servers=brokers.split(','))
   
           for message in consumer:
                   msg = volc_pb2.Entry()
                   msg.ParseFromString(message.value)
                   print(msg)
   `,
       "selected": true,
     },
     {
       "lang": "Java 语言",
       "text": `package dts.sub.volc;
   
   import com.github.daniel.shuy.kafka.protobuf.serde.KafkaProtobufDeserializer;
   import org.apache.kafka.clients.consumer.ConsumerRecord;
   import org.apache.kafka.clients.consumer.ConsumerRecords;
   import org.apache.kafka.clients.consumer.KafkaConsumer;
   import org.apache.kafka.common.serialization.StringDeserializer;
   
   import java.time.Duration;
   import java.util.Arrays;
   import java.util.Properties;
   
   public class DTSKafkaConsumerDemo {
       private final String topic;
       private final Properties props;
   
       public DTSKafkaConsumerDemo(String brokers, String topic, String group, String username, String password) {
           this.topic = topic;
           // 配置 sasl 认证
           String jaasTemplate = "org.apache.kafka.common.security.scram.ScramLoginModule required username=\"%s\" password=\"%s\";";
           String jaasCfg = String.format(jaasTemplate, username, password);
           // 配置 kafka 参数
           props = new Properties();
           props.put("bootstrap.servers", brokers);
           props.put("group.id", group);
           props.put("enable.auto.commit", "true");
           props.put("auto.commit.interval.ms", "1000");
           props.put("auto.offset.reset", "latest");
           props.put("session.timeout.ms", "30000");
           props.put("security.protocol", "SASL_PLAINTEXT");
           props.put("sasl.mechanism", "PLAIN");
           props.put("sasl.jaas.config", jaasCfg);
       }
   
       public void consume() throws java.lang.Exception {
           // init kafka consumer
           KafkaConsumer<String, Volc.Entry> consumer =
                   new KafkaConsumer<String, Volc.Entry>(props,new StringDeserializer(),new KafkaProtobufDeserializer<>(Volc.Entry.parser()));
           // subscribe topic
           consumer.subscribe(Arrays.asList(topic));
           // Loop consuming messages
           while (true) {
               ConsumerRecords<String, Volc.Entry> records = consumer.poll(Duration.ofSeconds(1));
               for (ConsumerRecord<String, Volc.Entry> record : records) {
                   // simply printed here
                   System.out.println(record);
               }
           }
       }
   
       public static void main(String[] args)throws java.lang.Exception  {
           // set your kafka brokers address
           String brokers = "your brokers address";
           // set your kafka username and password
           String username = "yout username";
           String password = "your password";
           // set your kafka topic 和 group
           String topic = "your topic";
           String group = "your group";
           DTSKafkaConsumerDemo c = new DTSKafkaConsumerDemo(brokers,topic,group, username, password);
           // start consume
           c.consume();
       }
   }
   `, 
     },
   ]
   return (<PreCodeTabs list={list} />);
   ```
   


<span id=".6L-Q6KGM5rWL6K-V"></span>
### Running test

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This topic takes the database <code>test</code> and table <code>demo</code> as examples.</div>


* <div data-tips="true" data-tips-type="tip">Select the appropriate JSON data based on the target language.</div>


1. In the source database, execute the following command to create a table named `demo`.

   ```mysql
   CREATE TABLE demo (id_t INT);
   ```
   

   Expected output:

   ```mixin-react
   const list = [
     {
       "lang": "Go语言和Python语言",
       "text": `
   src_type:MySQL
   entry_type:DDL
   timestamp:1639057424
   server_id:"105198****"
   database:"test"
   table:"demo"
   ddl_event:{sql:"create table demo (id_t int)"}`,
       "selected": true,
     },
     {
       "lang": "Java语言",
       "text": `
   ConsumerRecord(topic = d73e98e7fa9340faa3a0d4ccfa10****, partition = 0, leaderEpoch = 0, offset = 117, CreateTime = 1639120364271, serialized key size = 9, serialized value size = 67, headers = RecordHeaders(headers = [], isReadOnly = false), key = test.demo, value = src_type: MySQL
   entry_type: DDL
   timestamp: 1639120364
   server_id: "1051985825"
   database: "test"
   table: "demo"
   ddl_event {
     sql: "create table demo (Id_t int)"
   }
   )
   `, 
     },
   ]
   return (<PreCodeTabs list={list} />);
   ```
   

2. Run the following command to insert a piece of data into the `demo` table:

   ```mysql
   INSERT INTO demo (id_t) VALUES (1);
   ```
   

   Expected output:

   ```mixin-react
   const list = [
     {
       "lang": "Go 语言和 Python 语言",
       "text": `
   src_type:MySQL
   entry_type:DML
   timestamp:1639057434
   server_id:"105198****"
   database:"test"
   table:"demo"
   dml_event:{
           type:INSERT
           table_id:"148"
           column_defs:{
                   index:1
                   type:INTEGER
                   OriginType:"int"
                   name:"id_t"
                   is_nullable:true
                   is_unsigned:false
           }
           rows:{
                   after_cols:{
                           is_null:false
                           int64_value:1
                   }
           }
   }`,
       "selected": true,
     },
     {
       "lang": "Java语言",
       "text": `
   ConsumerRecord(topic = d73e98e7fa9340faa3a0d4ccfa10****, partition = 0, leaderEpoch = 0, offset = 118, CreateTime = 1639120462650, serialized key size = 9, serialized value size = 73, headers = RecordHeaders(headers = [], isReadOnly = false), key = test.demo, value = src_type: MySQL
   entry_type: DML
   timestamp: 1639120462
   server_id: "1051985825"
   database: "test"
   table: "demo"
   dml_event {
         type: INSERT
         table_id: "149"
         column_defs {
                   index: 1
                 type: INTEGER
                 OriginType: "int"
                 name: "Id_t"
                 is_nullable: true
                 is_unsigned: false
         }
         rows {
                 after_cols {
                 is_null: false
               int64_value: 1
                 }
         }
   }
   )`, 
     },
   ]
   return (<PreCodeTabs list={list} />);
   ```
