---
title: "Consuming Canal Proto subscription data via Kafka"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Consuming_Canal_Proto_subscription_data_via_RocketMQ"
---

Database Transmission Service (DTS) supports using Kafka clients to consume Canal Proto subscription data. This topic uses subscribing to an RDS for MySQL instance as an example to describe how to use the Go, Java and Python languages to consume Canal Proto format data.

<span id="prerequisites"></span>
## Prerequisites


* The client used to subscribe to and consume data needs to specify the Kafka version number of the server. The version number must be 2.2.x (for example, 2.2.2). You can specify the Kafka version number in the example code. The specific parameters are shown in the following table.



|**Runtime language** |**Instructions** |
|---|---|
|Go |Specify the server's Kafka version number through the parameter `config.Version` in the code example. |
|Python |Specify the server's Kafka version number through the parameter `api_version` in the example code. |
|Java |Specify the server's Kafka version number through the parameter `version` in the `maven pom.xml`file. |



* Install the runtime language environment as required.

   
   |**Runtime language** |**Instructions** |
   |---|---|
   |**Go** |Install [Go](https://go.dev/), Go 1.13 or later is required. You can run `go version` to view the Go version. |
   |**Python** |1. Install [Python](https://www.python.org/), Python 2.7 or later is required. You can run `python --version` to view the Python version.<br><br>2. Run the following commands in sequence to install pip dependencies.<br><br>   ```python```<br>```   pip install kafka-python```<br>```   ```<br>   <br><br>   ```python```<br>```   pip install protobuf```<br>```   ```<br>   <br><br>   ```python```<br>```   pip install python-snappy```<br>```   ```<br>    |
   |**Java** |1. Install [Java](https://www.oracle.com/java/technologies/downloads/). Java 1.8 or later is required. You can run `java -version` to view the Java version. |
   ||2. Install [maven](https://maven.apache.org/). Maven 3.8 or later is required. You can run`mvn -version` to view the Maven version.<br><br>3. In IDEA software, click **Create New Project** to create a Project.<br><br>4. Add the following dependencies to the project object model file `pom.xml` in the newly created Project. This example uses Kafka version 2.2.2. At the same time, you can also modify the version of`kafka-clients` in the `pom.xml` file to another version.<br><br>   ```xml```<br>```   <dependency>```<br>```     <groupId>org.apache.kafka</groupId>```<br>```     <artifactId>kafka-clients</artifactId>```<br>```     <version>2.2.2</version>```<br>```   </dependency>```<br>```   <dependency>```<br>```     <groupId>com.github.daniel-shuy</groupId>```<br>```     <artifactId>kafka-protobuf-serde</artifactId>```<br>```     <version>2.2.0</version>```<br>```   </dependency>```<br>```   <dependency>```<br>```     <groupId>org.xerial.snappy</groupId>```<br>```     <artifactId>snappy-java</artifactId>```<br>```     <version>1.1.8.4</version>```<br>```   </dependency>```<br>```   <dependency>```<br>```     <groupId>com.google.protobuf</groupId>```<br>```     <artifactId>protobuf-java</artifactId>```<br>```     <version>3.22.2</version>```<br>```   </dependency>```<br>```   ```<br>    |
   


<span id="procedure"></span>
## Procedure

<span id="download-and-compile-protobuf"></span>
### Download and compile ProtoBuf

When running the demo of the corresponding language, you need to complete the download and compilation of Protocol Buffers (also known as ProtoBuf) files in line with the following steps.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic uses the ProtoBuf defined by BytePlus as an example.</div>



1. Download the [ProtoBuf](https://github.com/volcengine/volc-sdk-golang/blob/main/example/dts/data-subscription-demo/canal/canal.proto) file.

2. Compile the downloaded `canal.proto` file into code of the corresponding language. The compilation method is as follows:

   * Go language

      Since the DTS developers have helped you compile the `ProtoBuf` file into Go code, you do not need to compile it again. Refer to [Protocol Buffer Basics: Go](https://developers.google.com/protocol-buffers/docs/gotutorial) for more information about compilation.

   * Python language

      When your language is Python, run the following command to compile the `ProtoBuf` file into Python language code to get the `canal_pb2` file. For more information about compilation, refer to [Protocol Buffer Basics: Python](https://developers.google.com/protocol-buffers/docs/pythontutorial).

      ```python
      protoc -I=. --python_out=. canal.proto
      ```
      

   * Java language

      When your language is Java, run the following command to compile the `ProtoBuf` file into Java language code to get the `canal.Canal` file. For more information about compilation, refer to [Protocol Buffer Basics: Java](https://developers.google.com/protocol-buffers/docs/javatutorial).

      `java`

      `protoc -I=.` `--java_out=.` `canal.proto`


<span id="associating-kafka-with-a-subscription-task"></span>
### Associating Kafka with a subscription task

This topic uses the macOS operating system as an example to describe how to associate Kafka with a subscription task.


1. Log in to the [DTS console](https://console.byteplus.com/dts) to create and configure a data subscription channel. For details, refer to [Subscription solution overview](https://docs.byteplus.com/en/docs/6390/79180#%E8%AE%A2%E9%98%85%E6%96%B9%E6%A1%88%E6%A6%82%E8%A7%88.)

2. Add a new consumer group in the destination data subscription channel. For details, refer to [Create new consumer group](https://docs.byteplus.com/en/docs/6390/133828).

3. Edit the`.zshrc` file, configure the following environment variable information, and complete the authentication to call the SDK to consume message data.

   
   |**Parameter** |**Description** |**Sample** |
   |---|---|---|
   |`GROUP` |Consumer group name |`285fef6b91754d0bbaab32e4976c****:test_dtssdk` |
   |`USER` |Kafka username. |`test_user` |
   |`PASSWORD` |Kafka users Password. |`Test@Pwd` |
   |`TOPIC` |The topic of the target DTS data subscription channel. |`d73e98e7fa9340faa3a0d4ccfa10****` |
   |`BROKERS` |Private network address of the target DTS data subscription channel. |`kafka-cndvhw9ves******.kafka.ivolces.com:9092` |
   

4. Select a demo example as needed.


```mixin-react
const list = [ 
  { 
    "lang": "Go", 
    "text": ` 
package main 

import ( 
   "context" 
   "fmt" 
   "log" 
   "os" 
   "strings" 
   "sync" 

   "github.com/Shopify/sarama" 
   "github.com/volcengine/volc-sdk-golang/example/dts/data-subscription-demo/canal" 
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
   addr     string 
} 

var ( 
   c Config 
) 

func init() { 
   c.addr = os.Getenv("BROKERS") 
   c.topic = os.Getenv("TOPIC") 
   c.group = os.Getenv("GROUP") 
   c.username = os.Getenv("USER") 
   c.password = os.Getenv("PASSWORD") 
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
      h.handleCanalMsg(m) 
      session.MarkMessage(m, "") 
      session.Commit() 
   } 
   return nil 
} 
func (h *Handler) handleCanalMsg(msg *sarama.ConsumerMessage) { 
   h.mu.Lock() 
   defer h.mu.Unlock() 
   h.totalCount++ 
   h.partitionCount[msg.Partition]++ 

   entry := &canal.Entry{} 
   if err := protobuf.Unmarshal(msg.Value, entry); err != nil { 
      panic(err) 
   } 

   fmt.Println("-------------- handle message --------------") 
   fmt.Printf("ServerID:%v\n", entry.GetHeader().GetServerId()) 
   fmt.Printf("Timestamp:%v\n", entry.GetHeader().GetExecuteTime()) 
   fmt.Printf("Database:%v\n", entry.GetHeader().GetSchemaName()) 
   fmt.Printf("Table:%v\n", entry.GetHeader().GetTableName()) 
   if entry.GetEntryType() != canal.EntryType_TRANSACTIONBEGIN && 
      entry.GetEntryType() != canal.EntryType_TRANSACTIONEND { 
      rowChange := &canal.RowChange{} 
      if err := protobuf.Unmarshal(entry.GetStoreValue(), rowChange); err != nil { 
         panic(err) 
      } 

      fmt.Printf("EventType:%v\n", rowChange.GetEventType().String()) 
      if rowChange.GetIsDdl() { 
         fmt.Printf("DDL:%s\n", rowChange.GetSql()) 
      } else { 
         for _, row := range rowChange.GetRowDatas() { 
            var before, after []string 
            for _, col := range row.BeforeColumns { 
               before = append(before, fmt.Sprintf("%s[%s(%s)]", col.GetName(), col.GetValue(), col.GetMysqlType())) 
            } 
            for _, col := range row.AfterColumns { 
               after = append(after, fmt.Sprintf("%s[%s(%s)]", col.GetName(), col.GetValue(), col.GetMysqlType())) 
            } 
            fmt.Printf("RowDatas:before=%v after=%v\n", before, after) 
         } 
      } 

   } 
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
   addr := strings.Split(c.addr, ",") 
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
    "lang": "Python", 
    "text": ` 
from kafka import KafkaConsumer 
import canal_pb2 
import os 


if __name__ == '__main__': 
# Create a Kafka consumer 
    consumer = KafkaConsumer( 
# Set the Kafka topic and consumer group 
        os.getenv('TOPIC'), 
        group_id=os.getenv('GROUP'), 
# Initialize the message offset 
        auto_offset_reset='latest', 
        enable_auto_commit=True, 
# Set up SASL authentication 
        security_protocol="SASL_PLAINTEXT", 
        sasl_mechanism="PLAIN", 
# Set the consumer group account and password 
        sasl_plain_username=os.getenv('USER'), 
        sasl_plain_password=os.getenv('PASSWORD'), 
        api_version=(2, 2, 2), 
# Set the Kafka address 
        bootstrap_servers=os.getenv('BROKERS').split(',')) 

    for message in consumer: 
# Consumption message 
        msg = canal_pb2.Entry() 
        msg.ParseFromString(message.value) 
        print(msg) 
        if msg.entryType == canal_pb2.ROWDATA: 
            event = canal_pb2.RowChange() 
            event.ParseFromString(msg.storeValue) 
            print(event) 
`, 
    "selected": true, 
  }, 
  { 
    "lang": "Java", 
    "text": ` 
package org.example; 
import canal.Canal; 
import com.github.daniel.shuy.kafka.protobuf.serde.KafkaProtobufDeserializer; 
import org.apache.kafka.clients.consumer.ConsumerRecord; 
import org.apache.kafka.clients.consumer.ConsumerRecords; 
import org.apache.kafka.clients.consumer.KafkaConsumer; 
import org.apache.kafka.common.serialization.StringDeserializer; 
import java.time.Duration; 
import java.util.Arrays; 
import java.util.Properties; 

import static canal.Canal.EntryType.ROWDATA; 

public class App { 
    private final String topic; 
    private final Properties props; 

    public App(String brokers,String topic,String group, String username, String password) { 
        this.topic = topic; 
// Configure sasl authentication 
        String jaasTemplate = "org.apache.kafka.common.security.scram.ScramLoginModule required username=\"%s\" password=\"%s\";"; 
        String jaasCfg = String.format(jaasTemplate, username, password); 
// Configure kafka parameters 
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
// Create a kafka consumer 
        KafkaConsumer<String, Canal.Entry> consumer = 
                new KafkaConsumer<>(props, new StringDeserializer(), new KafkaProtobufDeserializer<>(Canal.Entry.parser())); 
// Subscription topic 
        consumer.subscribe(Arrays.asList(topic)); 
// Consume messages in a loop 
        while (true) { 
            ConsumerRecords<String, Canal.Entry> records = consumer.poll(Duration.ofSeconds(1)); 
            for (ConsumerRecord<String, Canal.Entry> record : records) { 
              Canal.Entry entry =  record.value(); 
              System.out.printf("sourceType:%s\nentryType:%s\nexecuteTime:%s\nschemaName:%s" + 
                              "\ntableName:%s%n", entry.getHeader().getSourceType(), entry.getEntryType(), 
                      entry.getHeader().getExecuteTime(), entry.getHeader().getSchemaName(), 
                      entry.getHeader().getTableName()); 
              if (entry.getEntryType() ==  ROWDATA) { 
                  Canal.RowChange event = Canal.RowChange.parseFrom(entry.getStoreValue()); 
                  System.out.println(event); 
              } 
          } 
        } 
    } 

    public static void main(String[] args)throws java.lang.Exception  { 
// Set the Kafka address 
        String brokers = System.getenv("BROKERS"); 
// Set the Kafka consumption group Account and Password 
        String username = System.getenv("USER"); 
        String password = System.getenv("PASSWORD"); 
// Set the Kafka topic and group 
        String topic = System.getenv("TOPIC"); 
        String group = System.getenv("GROUP"); 
        App c = new App(brokers,topic,group, username, password); 

        c.consume(); 
    } 
} 
`, 
  }, 
] 
return (<PreCodeTabs list={list} />);
```


<span id="run-test"></span>
### Run test

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This topic takes the database <code>test</code> and table <code>demo</code> as examples.</div>


* <div data-tips="true" data-tips-type="tip">Select the appropriate JSON data based on the target language.</div>


1. In the source database, execute the following command to create a table named `demo`.

   ```mysql
   CREATE TABLE demo (id_t INT);
   ```
   

   Expected output as follows:

   ```mixin-react
   const list = [ 
     { 
   "lang": "Go", 
       "text": ` 
   sourceType:MYSQL 
   entryType:ROWDATA 
   executeTime:1692793679 
   schemaName:test 
   tableName:demo 
   EventType:CREATE 
   DDL:CREATE TABLE demo (id_t INT) 
   `, 
       "selected": true, 
     }, 
     { 
   "lang": "Python", 
       "text": ` 
   sourceType:MYSQL 
   entryType:ROWDATA 
   executeTime:1692791754 
   schemaName:test 
   tableName:demo 
   eventType: CREATE 
   isDdl: true 
   sql: "CREATE TABLE demo (id_t INT)" 
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
   "lang": "Go", 
       "text": ` 
   sourceType:MYSQL 
   entryType:ROWDATA 
   executeTime:1692793748 
   schemaName:test 
   tableName:demo 
   EventType:INSERT 
   RowDatas:before=[] after=[id_t[1(int)]]`, 
       "selected": true, 
     }, 
     { 
   "lang": "Python and Java", 
       "text": ` 
   sourceType:MYSQL 
   entryType:ROWDATA 
   executeTime:1692792163 
   schemaName:test 
   tableName:demo 
   eventType: INSERT 
   isDdl: false 
   rowDatas { 
     afterColumns { 
       index: 1 
       name: "id_t" 
       updated: true 
       isNull: false 
       value: "1" 
       mysqlType: "int" 
     } 
   }`, 
     }, 
   ] 
   return (<PreCodeTabs list={list} />);
   ```
