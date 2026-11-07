---
title: "Consuming Avro subscription data via Kafka"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Consuming_Avro_subscription_data_via_Kafka"
---

DTS supports using Kafka clients to consume BytePlus Proto subscription data via RocketMQ. This topic uses subscribing to an RDS for MySQL instance as an example to describe how to use the Go, Java and Python languages to consume Canal format data.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The client used to subscribe to and consume data needs to specify the Kafka version number of the server. The version number must be 2.2.x (for example, 2.2.2). You can specify the Kafka version number in the example code. The specific parameters are shown in the following table.

   
   |**Runtime language** |**Description** |
   |---|---|
   |Go |Use the parameter `config.Version` in the code example to specify the Kafka version number of the server. |
   |Python |Specify the server's Kafka version number through the parameter `api_version` in the example code. |
   |Java |Specify the server's Kafka version number through the parameter `version` in the `maven pom.xml` file. |
   

* Install the runtime language environment as required.

   
   |**Runtime language** |**Description** |
   |---|---|
   |Go |To install [Go](https://go.dev/), Go 1.13 or above is required. You can run `go version` to view the Go version. |
   |Python |1. To install [Python](https://www.python.org/), Python 2.7 or above is required. You can run `python --version` to view the Python version.<br><br>2. Run the following commands in sequence to install pip dependencies.<br><br>   ```python```<br>```   pip install kafka-python```<br>```   pip install avro```<br>```   ```<br>    |
   |Java |1. Install [Java](https://www.oracle.com/java/technologies/downloads/). Java 1.8 or later is required. You can run `java -version` to view the Java version.<br><br>2. Install [maven](https://maven.apache.org/). Maven 3.8 or later is required. You can run` mvn -version` to view the Maven version.<br><br>3. In IDEA software, click **Create New Project** to create a Project.<br><br>4. Add the following dependencies to the project object model file `pom.xml` in the newly created Project. This example uses Kafka version 2.2.2. At the same time, you can also modify the version of `kafka-clients` in the `pom.xml` file to another version.<br><br>   ```xml```<br>```   <dependency>```<br>```     <groupId>org.apache.kafka</groupId>```<br>```     <artifactId>kafka-clients</artifactId>```<br>```     <version>2.2.2</version>```<br>```   </dependency>```<br>```   <dependency>```<br>```     <groupId>org.apache.avro</groupId>```<br>```     <artifactId>avro</artifactId>```<br>```     <version>1.8.2</version>```<br>```   </dependency>```<br>```   ```<br>    |
   


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5YWz6IGULWthZmthLeWSjOiuoumYheS7u-WKoQ=="></span>
### **Associating Kafka with a subscription task**

This topic uses the macOS operating system as an example to describe how to associate Kafka with a subscription task.


1. Log in to the [DTS console](https://console.byteplus.com/dts) to create and configure a data subscription channel. For more information, refer to [Subscription solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_subscription_solutions).

2. Add a new consumer group in the destination data subscription channel. For details, refer to [Create new consumer group](https://docs.byteplus.com/en/docs/DTS/adding_a_consumer_group).

3. Select a consumption example as required.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The directories of Python and Java consumption examples contain Demo files.   </div>
   

   The directories of the Python and Java consumption examples are as follows:

   * [Python consumption example directory](https://github.com/volcengine/volc-sdk-python/tree/main/volcengine/example/dts/subscription/avro)

      ```python
      .
              ├── dts_kafka_consumer_demo.py    # Consume Kafka messages
              ├── deserializer.py               # Deserialize Avro format data
              ├── record_printer.py             # Print the deserialized Avro data
              └── record.avsc                   # Schema file
      ```
      

   * [Java consumption example directory](https://github.com/volcengine/volc-sdk-java/tree/main/example/src/main/java/com/volcengine/example/dts/avro)

      ```shell
      .
              ├── DTSKafkaConsumerDemo.java     # 消费Kafka消息
              ├── AvroDeserializer.java         # 反序列化Avro格式数据
              ├── AvroRecordPrinter.java        # 打印反序列化后的Avro数据
              ├── record.avsc                   # schema 文件
              └── avro                          # schema 生成的文件
      ```
      

   * The Go consumption example is as follows.

      ```go
      package main
      
      import (
         "bytes"
         "context"
         "fmt"
         "strings"
         "sync"
      
         "github.com/twpayne/go-geom/encoding/wkb"
         "github.com/twpayne/go-geom/encoding/wkt"
         "github.com/Shopify/sarama"
         "your path of code generated by avro compilation/avro"
      )
      
      func main() {
         config := sarama.NewConfig()
         brokers := "your brokers addrress"
         topic := "your topic"
         group := "your group"
         username := "your username"
         password := "your password"
      
         config.Consumer.Offsets.Initial = sarama.OffsetNewest
         config.Net.SASL.Enable = true
         config.Net.SASL.User = username
         config.Net.SASL.Password = password
      
         cons, err := sarama.NewConsumerGroup(strings.Split(brokers, ","), group, config)
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
               fmt.Printf("consume failde, err=%v", err)
            }
         }
      }
      
      type Handler struct {
         format         string
         topic          string
         partitionCount map[int32]int
         totalCount     int
         mu             sync.Mutex
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
         for msg := range claim.Messages() {
            record, err := avro.DeserializeRecord(bytes.NewReader(msg.Value))
            if err != nil {
               panic(err)
            }
            printRecord(&record)
            session.MarkMessage(msg, "")
            session.Commit()
         }
         return nil
      }
      
      func printRecord(record *avro.Record) {
         fmt.Printf("Operation[%s] ObjectName[%s] SourceTimestamp[%v] Id[%v]\n",
            record.Operation.String(), record.ObjectName.String, record.SourceTimestamp, record.Id)
         switch record.Operation {
         case avro.OperationDDL:
            fmt.Printf("DDL[%s] \n", record.AfterImages.String)
         case avro.OperationINSERT:
            for i := 0; i < len(record.AfterImages.ArrayUnionNullIntegerCharacterDecimalFloatTimestampDateTimeTimestampWithTimeZoneBinaryGeometryTextGeometryBinaryObjectTextObjectEmptyObject); i++ {
               after, err := getValue(record.AfterImages.ArrayUnionNullIntegerCharacterDecimalFloatTimestampDateTimeTimestampWithTimeZoneBinaryGeometryTextGeometryBinaryObjectTextObjectEmptyObject[i])
               if err != nil {
                  panic(err)
               }
               fmt.Printf("Field[%s] After[%s]\n", record.Fields.ArrayField[i].Name, after)
            }
         case avro.OperationUPDATE:
            for i := 0; i < len(record.AfterImages.ArrayUnionNullIntegerCharacterDecimalFloatTimestampDateTimeTimestampWithTimeZoneBinaryGeometryTextGeometryBinaryObjectTextObjectEmptyObject); i++ {
               before, err := getValue(record.BeforeImages.ArrayUnionNullIntegerCharacterDecimalFloatTimestampDateTimeTimestampWithTimeZoneBinaryGeometryTextGeometryBinaryObjectTextObjectEmptyObject[i])
               if err != nil {
                  panic(err)
               }
               after, err := getValue(record.AfterImages.ArrayUnionNullIntegerCharacterDecimalFloatTimestampDateTimeTimestampWithTimeZoneBinaryGeometryTextGeometryBinaryObjectTextObjectEmptyObject[i])
               if err != nil {
                  panic(err)
               }
               fmt.Printf("Field[%s] Before[%s] After[%s]\n", record.Fields.ArrayField[i].Name, before, after)
            }
         case avro.OperationDELETE:
            for i := 0; i < len(record.BeforeImages.ArrayUnionNullIntegerCharacterDecimalFloatTimestampDateTimeTimestampWithTimeZoneBinaryGeometryTextGeometryBinaryObjectTextObjectEmptyObject); i++ {
               before, err := getValue(record.BeforeImages.ArrayUnionNullIntegerCharacterDecimalFloatTimestampDateTimeTimestampWithTimeZoneBinaryGeometryTextGeometryBinaryObjectTextObjectEmptyObject[i])
               if err != nil {
                  panic(err)
               }
               fmt.Printf("Field[%s] Before[%s]\n", record.Fields.ArrayField[i].Name, before)
            }
         }
      }
      
      func getValue(in *avro.UnionNullIntegerCharacterDecimalFloatTimestampDateTimeTimestampWithTimeZoneBinaryGeometryTextGeometryBinaryObjectTextObjectEmptyObject) (string, error) {
         if in == nil {
            return "null", nil
         }
      
         switch in.UnionType {
         case avro.UnionNullIntegerCharacterDecimalFloatTimestampDateTimeTimestampWithTimeZoneBinaryGeometryTextGeometryBinaryObjectTextObjectEmptyObjectTypeEnumInteger:
            return in.Integer.Value, nil
         case avro.UnionNullIntegerCharacterDecimalFloatTimestampDateTimeTimestampWithTimeZoneBinaryGeometryTextGeometryBinaryObjectTextObjectEmptyObjectTypeEnumCharacter:
            return string(in.Character.Value), nil
         case avro.UnionNullIntegerCharacterDecimalFloatTimestampDateTimeTimestampWithTimeZoneBinaryGeometryTextGeometryBinaryObjectTextObjectEmptyObjectTypeEnumDecimal:
            return fmt.Sprintf("%s", in.Decimal.Value), nil
         case avro.UnionNullIntegerCharacterDecimalFloatTimestampDateTimeTimestampWithTimeZoneBinaryGeometryTextGeometryBinaryObjectTextObjectEmptyObjectTypeEnumFloat:
            return fmt.Sprintf("%v", in.Float.Value), nil
         case avro.UnionNullIntegerCharacterDecimalFloatTimestampDateTimeTimestampWithTimeZoneBinaryGeometryTextGeometryBinaryObjectTextObjectEmptyObjectTypeEnumTimestamp:
            return fmt.Sprintf("%v.%v", in.Timestamp.Timestamp, in.Timestamp.Millis), nil
         case avro.UnionNullIntegerCharacterDecimalFloatTimestampDateTimeTimestampWithTimeZoneBinaryGeometryTextGeometryBinaryObjectTextObjectEmptyObjectTypeEnumDateTime:
            var year, month, day, hour, minute, second int32
            if in.DateTime.Year != nil {
               year = in.DateTime.Year.Int
            }
            if in.DateTime.Month != nil {
               month = in.DateTime.Month.Int
            }
            if in.DateTime.Day != nil {
               day = in.DateTime.Day.Int
            }
            if in.DateTime.Hour != nil {
               hour = in.DateTime.Hour.Int
            }
            if in.DateTime.Minute != nil {
               minute = in.DateTime.Minute.Int
            }
            if in.DateTime.Second != nil {
               second = in.DateTime.Second.Int
            }
            if year != 0 {
               return fmt.Sprintf("%v-%v-%v %v:%v:%v", year, month, day, hour, minute, second), nil
            }
            return fmt.Sprintf("%v:%v:%v", hour, minute, second), nil
         case avro.UnionNullIntegerCharacterDecimalFloatTimestampDateTimeTimestampWithTimeZoneBinaryGeometryTextGeometryBinaryObjectTextObjectEmptyObjectTypeEnumTimestampWithTimeZone:
            var year, month, day, hour, minute, second int32
            if in.TimestampWithTimeZone.Value.Year != nil {
               year = in.TimestampWithTimeZone.Value.Year.Int
            }
            if in.TimestampWithTimeZone.Value.Month != nil {
               month = in.TimestampWithTimeZone.Value.Month.Int
            }
            if in.TimestampWithTimeZone.Value.Day != nil {
               day = in.TimestampWithTimeZone.Value.Day.Int
            }
            if in.TimestampWithTimeZone.Value.Hour != nil {
               hour = in.TimestampWithTimeZone.Value.Hour.Int
            }
            if in.TimestampWithTimeZone.Value.Minute != nil {
               minute = in.TimestampWithTimeZone.Value.Minute.Int
            }
            if in.TimestampWithTimeZone.Value.Second != nil {
               second = in.TimestampWithTimeZone.Value.Second.Int
            }
            if year != 0 {
               return fmt.Sprintf("%v-%v-%v %v:%v:%v+%v", year, month, day, hour, minute, second, in.TimestampWithTimeZone.Timezone), nil
            }
            return fmt.Sprintf("%v:%v:%v", hour, minute, second), nil
      
         case avro.UnionNullIntegerCharacterDecimalFloatTimestampDateTimeTimestampWithTimeZoneBinaryGeometryTextGeometryBinaryObjectTextObjectEmptyObjectTypeEnumBinaryGeometry:
            return getReadableGeometry(in.BinaryGeometry.Value)
            //return fmt.Sprintf("%s", string(in.BinaryGeometry.Value)), nil
         case avro.UnionNullIntegerCharacterDecimalFloatTimestampDateTimeTimestampWithTimeZoneBinaryGeometryTextGeometryBinaryObjectTextObjectEmptyObjectTypeEnumTextGeometry:
            return getReadableGeometry([]byte(in.TextGeometry.Value))
            //return fmt.Sprintf("%s", in.TextGeometry.Value), nil
         case avro.UnionNullIntegerCharacterDecimalFloatTimestampDateTimeTimestampWithTimeZoneBinaryGeometryTextGeometryBinaryObjectTextObjectEmptyObjectTypeEnumBinaryObject:
            return fmt.Sprintf("%s", string(in.BinaryObject.Value)), nil
         case avro.UnionNullIntegerCharacterDecimalFloatTimestampDateTimeTimestampWithTimeZoneBinaryGeometryTextGeometryBinaryObjectTextObjectEmptyObjectTypeEnumTextObject:
            return fmt.Sprintf("%s", in.TextObject.Value), nil
         case avro.UnionNullIntegerCharacterDecimalFloatTimestampDateTimeTimestampWithTimeZoneBinaryGeometryTextGeometryBinaryObjectTextObjectEmptyObjectTypeEnumEmptyObject:
            return fmt.Sprintf("%s", in.EmptyObject.String()), nil
         }
         return "", fmt.Errorf("invalid value for *UnionNullIntegerCharacterDecimalFloatTimestampDateTimeTimestampWithTimeZoneBinaryGeometryTextGeometryBinaryObjectTextObjectEmptyObject")
      }
      
      func getReadableGeometry(raw []byte) (string, error) {
         if len(raw) < 4 {
            return "", fmt.Errorf("not a valid geometry %v", raw)
         }
         geomObj, err := wkb.Unmarshal(raw[4:])
         if err != nil {
            return "", err
         }
      
         wktObj, err := wkt.Marshal(geomObj)
         if err != nil {
            return "", err
         }
         return wktObj, nil
      }
      ```
      

4. Generate the Schema code in Go.

   When consuming Avro\-formatted data in Go, you need to run the following command to download the code generation tool and generate the Schema code.

   1. Download the code generation tool: `go install github.com/actgardner/gogen-avro/v10/cmd/...@latest`.

   2. Run `mkdir avro && gogen-avro ./avro record.avsc` to generate the code.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To view the Go message format, refer to <a href="https://github.com/volcengine/volc-sdk-golang/tree/main/example/dts/data-subscription-demo/avro">Go protocol format</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When consuming Avro\-formatted data in Java and Python, you do not need to generate Schema structure code.   </div>
   



&nbsp;

5. Modify demo file parameters.

   
   |**Name** |**Description** |**Example** |
   |---|---|---|
   |`GROUP` |Consumer group name |`285fef6b91754d0bbaab32e4976c****:test_dtssdk` |
   |`USER` |Kafka username. |`test_user` |
   |`PASSWORD` |Kafka users Password. |`Test@***` |
   |`TOPIC` |The topic of the target DTS data subscription channel. |`d73e98e7fa9340faa3a0d4ccfa10****` |
   |`BROKERS` |Private network address of the target DTS data subscription channel. |`kafka-cndvhw9ves******.``kafka.ivolces.com:9092` |
   


<span id=".6L-Q6KGM5rWL6K-V"></span>
### **Running test**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This topic takes the database <code>test</code> and table <code>demo</code> as examples.</div>


* <div data-tips="true" data-tips-type="tip">Select the appropriate JSON data based on the target language.</div>


1. In the source database, execute the following command to create a table named `demo`.

   ```plain
   CREATE TABLE demo (id_t INT);
   ```
   

   The expected output for Go, Java, and Python is as follows:

   ```shell
   Operation[DDL] ObjectName[test] SourceTimestamp[1710848558] Id[1710782319849000034]
   DDL[CREATE TABLE demo (id_t INT)]
   ```
   

2. Run the following command to insert a piece of data into the `demo` table:

   ```plain
   INSERT INTO demo (id_t) VALUES (1);
   ```
   

   The expected output for Go, Java, and Python is as follows:

   ```go
   Operation[INSERT] ObjectName[test.demo] SourceTimestamp[1710848859] Id[1710782319849000035]
   Field[id_t] After[1]
   ```
