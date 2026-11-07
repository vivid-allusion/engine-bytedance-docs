---
title: "Confluent Avro"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Confluent_Avro"
---

Avro Schema Registry (`avro-confluent`) format enables you to read records serialized by `io.confluent.kafka.serializers.KafkaAvroSerializer` and write records that can be deserialized by `io.confluent.kafka.serializers.KafkaAvroDeserializer`.

When reading (deserializing) records in this format, the Avro writer schema is retrieved from the configured Confluent Schema Registry based on the schema version id encoded in the record, while the reader schema is inferred from the table schema.

When writing (serializing) records in this format, the Avro schema is inferred from the table schema and used to retrieve the schema id to be encoded with the data. We retrieve the schema id under the configured subject in the Confluent Schema Registry. The subject is specified through the `avro-confluent.subject` parameter.

Avro Schema Registry format can only be used with Apache Kafka SQL Connector or Upsert Kafka SQL Connector.

<span id="329893a7"></span>
## How to Create a Table Using Avro\-Confluent Format

Here is an example of creating a table using Kafka connectors and Confluent Avro format.

An example of a table using raw UTF\-8 strings as Kafka's key and Avro records registered in the Schema Registry as Kafka's values:

```SQL
CREATE TABLE user_created (

  -- This column maps to the original UTF-8 key from Kafka.
  the_kafka_key STRING,
  
  -- Columns mapped to certain Avro fields within the Kafka value.
  id STRING,
  name STRING,
  email STRING

) WITH (

  'connector' = 'kafka',
  'topic' = 'user_events_example1',
  'properties.bootstrap.servers' = 'localhost:9092',

  -- Use the UTF-8 string as Kafka keys by mapping to the 'the_kafka_key' column in the table.
  'key.format' = 'raw',
  'key.fields' = 'the_kafka_key',

  'value.format' = 'avro-confluent',
  'value.avro-confluent.url' = 'http://localhost:8082',
  'value.fields-include' = 'EXCEPT_KEY'
)
```


We can write data to a Kafka table like this:

```SQL
INSERT INTO user_created
SELECT
  -- Copy the user ID into the column mapped to the Kafka key.
  id as the_kafka_key,

  -- All the values
  id, name, email
FROM some_table
```


Examples of tables where Kafka's key and value are registered as Avro records in the Schema Registry:

```SQL
CREATE TABLE user_created (
  
  -- This column maps to the Avro field 'id' in the Kafka key.
  kafka_key_id STRING,
  
  -- Columns mapped to specific Avro fields within the Kafka value.
  id STRING,
  name STRING, 
  email STRING
  
) WITH (

  'connector' = 'kafka',
  'topic' = 'user_events_example2',
  'properties.bootstrap.servers' = 'localhost:9092',

  -- Note: Due to hash partitioning, schema upgrades in the context of Kafka keys are rarely backward or forward compatible.
  'key.format' = 'avro-confluent',
  'key.avro-confluent.url' = 'http://localhost:8082',
  'key.fields' = 'kafka_key_id',

  -- In this case, we expect both the Kafka key and value Avro schemas to include the 'id' field.
  -- => Add a prefix to the columns in the table associated with Kafka key fields to avoid conflicts.
  'key.fields-prefix' = 'kafka_key_',

  'value.format' = 'avro-confluent',
  'value.avro-confluent.url' = 'http://localhost:8082',
  'value.fields-include' = 'EXCEPT_KEY',
   
  -- Since Flink 1.13, subjects have a default value but can be overridden:
  'key.avro-confluent.subject' = 'user_events_example2-key2',
  'value.avro-confluent.subject' = 'user_events_example2-value2'
)
```


Using the upsert\-kafka connector, example of a table where Kafka's value is registered as Avro records in the Schema Registry:

```SQL
CREATE TABLE user_created (
  
  -- This column is mapped to the original UTF-8 key from Kafka.
  kafka_key_id STRING,
  
  -- Columns mapped to certain Avro fields within the Kafka value.
  id STRING, 
  name STRING, 
  email STRING, 
  
  -- The upsert-kafka connector requires a primary key to define the upsert behavior.
  PRIMARY KEY (kafka_key_id) NOT ENFORCED

) WITH (

  'connector' = 'upsert-kafka',
  'topic' = 'user_events_example3',
  'properties.bootstrap.servers' = 'localhost:9092',

  -- UTF-8 strings used as Kafka keys.
  -- In this case, we do not specify 'key.fields' because it is determined by the table’s primary key.
  'key.format' = 'raw',
  
  -- In this example, we expect both the Kafka key and value Avro schemas to include the 'id' field.
  -- => Add a prefix to the columns in the table associated with Kafka key fields to avoid naming conflicts.
  'key.fields-prefix' = 'kafka_key_',

  'value.format' = 'avro-confluent',
  'value.avro-confluent.url' = 'http://localhost:8082',
  'value.fields-include' = 'EXCEPT_KEY'
)
```


<span id="632ca207"></span>
## Format Parameters


|Parameter |Required |Default |Type |Description |
|---|---|---|---|---|
|<span id="45f1e147"></span><br>##### format |Required |(none) |String |Specify the format to use, should be `'avro-confluent'`. |
|<span id="194f3dc2"></span><br>##### avro\-confluent.basic\-auth.credentials\-source |Optional |(none) |String |Specify the basic authentication credentials source for Schema Registry. |
|<span id="19fecb5a"></span><br>##### avro\-confluent.basic\-auth.user\-info |Optional |(none) |String |Specify the basic authentication user information for Schema Registry. |
|<span id="d9cc9433"></span><br>##### avro\-confluent.bearer\-auth.credentials\-source |Optional |(none) |String |Specify the bearer authentication credentials source for Schema Registry. |
|<span id="7b58f67d"></span><br>##### avro\-confluent.bearer\-auth.token |Optional |(none) |String |Specify the bearer authentication token for Schema Registry. |
|<span id="3efeeb3b"></span><br>##### avro\-confluent.properties |Optional |(none) |Map |Property mapping that is forwarded to the Schema Registry. This is very useful for options that are not formally exposed through Flink configuration options.<br><br>> **Important** Flink options have higher priority. |
|<span id="468abff4"></span><br>##### avro\-confluent.ssl.keystore.location |Optional |(none) |String |Specify the location of the SSL keystore. |
|<span id="aeadce93"></span><br>##### avro\-confluent.ssl.keystore.password |Optional |(none) |String |Specify the password for the SSL keystore. |
|<span id="a160c676"></span><br>##### avro\-confluent.ssl.truststore.location |Optional |(none) |String |Specify the location of the SSL truststore. |
|<span id="a3cedfbf"></span><br>##### avro\-confluent.ssl.truststore.password |Optional |(none) |String |Specify the password for the SSL truststore. |
|<span id="79527302"></span><br>##### avro\-confluent.subject |Optional |(none) |String |Specify the Confluent Schema Registry subject, and register the schema used during serialization under that subject. By default, if you use kafka and upsert\-kafka connectors as the value or key format, use\-value or\-key as the default subject name. For the filesystem connector, the subject option must be used when it is used as a result table. |
|<span id="8f2d2897"></span><br>##### avro\-confluent.url |Required |(none) |String |Specify the URL of the Confluent Schema Registry used for fetching or registering schemas. |


<span id="f1294f98"></span>
## Data Type Mapping

Currently, Apache Flink infers the Avro reader schema during deserialization and the Avro writer schema during serialization from the table schema. Explicitly defining the Avro schema is not supported yet. Therefore, the table below lists the type mappings from Flink types to Avro types.


|Flink SQL data type |Avro Data Types |Avro Logical Types |
|---|---|---|
|CHAR / VARCHAR / STRING |string | |
|`BOOLEAN` |`boolean` | |
|`BINARY / VARBINARY` |`bytes` | |
|`DECIMAL` |`fixed` |`decimal` |
|`TINYINT` |`int` | |
|`SMALLINT` |`int` | |
|`INT` |`int` | |
|`BIGINT` |`long` | |
|`FLOAT` |`float` | |
|`DOUBLE` |`double` | |
|`DATE` |`int` |`date` |
|`TIME` |`int` |`time-millis` |
|`TIMESTAMP` |`long` |`timestamp-millis` |
|`ARRAY` |`array` | |
|`MAP`<br><br>(Key must be of type string/char/varchar) |`map` | |
|`MULTISET`<br><br>(Elements must be of type string/char/varchar) |`map` | |
|`ROW` |`record` | |


Besides the types listed here, Flink also supports reading/writing nullable types. Flink maps nullable types to Avro `union(something, null)`, where `something` is the Avro type converted from Flink types.
