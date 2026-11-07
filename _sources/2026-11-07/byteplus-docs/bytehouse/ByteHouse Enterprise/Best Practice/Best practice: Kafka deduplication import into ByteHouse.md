---
title: "Best practice: Kafka deduplication import into ByteHouse"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/best-practice-kafka-deduplication-import-into-bytehouse"
---

This article introduces the procedure of using Kafka deduplication import to ByteHouse through a use scenario of "real\-time monitoring of factory workshop temperature and humidity data collection."

The factory sets up thermal sensors in key workshops to collect various sensor data such as temperature and humidity, and sends them to ByteHouse for analysis. Through aggregate and detailed queries, issues like the average, extreme values, trends, alert event statistics, and specific event details, data verification and accuracy, and response to maintenance needs can be addressed.

<span id="a8ae2e4f"></span>
# Data example


|Table name |Data source |Example data |The meaning of data |
|---|---|---|---|
|Heat sensor data table<br><br>(Fact table)<br><br>Generate 1000 push messages an hour<br><br>Involved data spans three years from 2021 to 2023<br><br>**Hope to retain the latest line of data Every hour for each ID.**  |Kafka |```SQL```<br>```{```<br>```    "sensorId": "sensor1031984076491",```<br>```    "timestamp": "2023-12-01T00:00:20",```<br>```    "temperature": 31.68,```<br>```    "humidity": 55.09,```<br>```    "heading": "SW",```<br>```    "alertFlags": [```<br>```        "humidityDrop"```<br>```    ],```<br>```    "gpsLatitude": -20.510689,```<br>```    "gpsLongitude": 42.272274```<br>```}```<br> |* `sensorId` (String): Sensor ID.<br><br>* `timestamp` (DateTime): The timestamp of data recording.<br><br>* `temperature` (Float64): Current temperature reading, in Celsius.<br><br>* `humidity` (Float64): Current humidity reading, in percent.<br><br>* `heading`: Sensor orientation, is an enumeration value.<br><br>* `alertFlags` (Array(String)): Alert flags, for example ["overheat", "humidityDrop"].<br><br>* `gpsLatitude`,`gpsLongitude` (Float64): Latitude and longitude. |


<span id="cbbbcf88"></span>
# Steps

<span id="8decd6e2"></span>
## Step 1: Prepare the Kafka Environment


1. Prepare a Kafka cluster, ensuring network communication between the two (e.g., within the same VPC).

2. Create a new Topic:

   * Name the sensor specifically for subscribing to `heat_sensor_data`.

   * Data is consumed into ByteHouse via a correspondence relationship of `ParitionNum%ByteHouseShardCount`, recommending that the **Partition number should be an integer multiple of ByteHouse shard number** for balanced data distribution into shards. For example, if there are 4 shards, it is recommended to choose 4, 8 or other multiples of shards. An example with 8 items.

3. Data is written into Kafka.


<span id="5f1b9f97"></span>
## Step 2: Create a new database table


* We need a local ByteHouse table (also known as a table in the MergeTree family) to store the fact table data received by Kafka. Named `heat_sensor_data_local`.

* We also need a distributed table for receiving query requests, named `heat_sensor_data`.


<span id="6ac7f1f9"></span>
### Create a new library

We can create a new database through the ByteHouse Console.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f0e6aed42f349fd977ec67ab3e9fb37~tplv-goo7wpa0wc-image.image) </span>

Or create via SQL in the client:

```SQL
CREATE DATABASE sensor ON CLUSTER bytehouse_test 
```


<span id="00daec16"></span>
### Create local and distributed tables


1. Select a table engine, please refer to the description below. Considering the requirement to **keep only the latest row of data per ID every hour,**  we use HaUniqueMergeTree.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When selecting the MergeTree family table engine, judge whether deduplication is needed? Or is it because the data in the column is inconsistent, requiring partial column updates?   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Yes: use HaUniqueMergeTree.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">No: use HaMergeTree.   </div>
   

2. Perform data mapping. Below is an example of JSON data based on import, with important areas marked.


```JSON
{    
    "sensorId": "sensor1031984076491", //String
    "timestamp": "2023-12-01T00:00:20", //DateTime
    "temperature": 31.68,//Float64
    "humidity": 55.09,//Float64
    "heading": "SW", //The field is a constant. It is recommended to use LowCadinality. LowCadinality is automatically encoded, which makes queries faster.
    "alertFlags": ["humidityDrop"],//Therefore, in this scenario, there are only two possibilities, namely ["overheat", "humidityDrop"]. It can be expanded into two bool fields, and then the subsequent SQL queries can be simpler.
    "gpsLatitude": -20.510689,
    "gpsLongitude": 42.272274
}
```



3. Consider data distribution

   Based on performance considerations, the HaUniqueMergeTree engine can only deduplicate within a shard. This means that no matter how the data is written, the data with the same unique key must be inserted into the same shard.

   Data is imported into ByteHouse via Kafka and is ultimately routed to ByteHouse shards based on Partition_num%shard_count. For example, in this scenario with 2 shards, if there are 4 upstream partitions, partition 3 will be inserted into shard 1.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2a628ab87d14d9db7bed0c784ad5f17~tplv-goo7wpa0wc-image.image) </span>

   Based on the two points above, the upstream must ensure that Kafka partitions are based on a unique key (sensorId), resulting in all rows with the same sensorId falling into the same shard to successfully deduplicate. (This issue does not exist with engines that do not deduplicate like HaMergeTree).

4. Confirm selection of key fields for other tables.

   * Sorting key: Choose the field that is most frequently queried, which in this example is clearly sensorId.

   * Unique key: In this example, it is desired to retain one record per ID per hour, but there is no field indicating the hour. Therefore, we can use a materialized column approach (MATERIALIZED COLUMN) to create a new column hour, generated from datetime every time data is imported, setting the unique key as `(sensorId, hour)`.

   * Shard key: In this scenario, there is an automatic mapping relationship between Kafka's Partition and shards, hence no shard key is set.

   * Partition key: Time fields such as timestamp are recommended, but with a unit of days (otherwise, a partition would be created every second).

   * TTL: TTL should be set based on the partition key, configure it for 3 years here as required.

5. Choice of Nullable:

   * sensorId and timestamp are sorting and partition keys, and it is necessary to ensure that they are not empty, otherwise performance will decline.

   * Conversely, other fields are recommended to be empty (unless it can be 100% ensured that they are not empty) to prevent import errors caused by empty fields.

6. Other Precautions

   * It is recommended to keep the field names exactly the same as those in the JSON to facilitate automatic matching during subsequent import tasks.

   * Important Table Settings:

      * `index_granularity`, the granularity of the index, the smaller the value the faster the single row query, and the larger the value the faster the batch query; it's recommended to use the default 8192.

      * `partition_level_unique_keys`: Level of deduplication

         * 1: (Default) Partition granularity deduplication: Data is unique within the partition, this setting is not recommended to be adjusted (but be aware of this restriction in business terms).

         * 0: Whole table granularity deduplication: Data is unique across the entire table, which will result in more memory usage and many scenarios such as cold storage not being supported. Therefore, unless strongly required by the business, it is not recommended.

      * `enable_disk_based_unique_key_index`: Location of the unique key index:

         * The unique_key_index on disk will cause a 30% decrease in import performance.

         * By default, the unique_key_index is in memory, but it will consume some memory overhead. Be sure to monitor memory usage (see "DataRanger's Technical Support").

7. Based on the above requirements, the SQL is generated as follows:

   ```SQL
   CREATE TABLE sensor.heat_sensor_data_unique_local ON CLUSTER bytehouse_test (
       sensorId String,
       timestamp DateTime,
       hour DateTime MATERIALIZED toStartOfHour(timestamp),
       temperature Nullable(Float64),
       humidity Nullable(Float64),
       heading LowCadinality(Nullable(String)),
       overheat Nullable(Bool), 
       humidityDrop Nullable(Bool),
       gpsLatitude Nullable(Float64),
       gpsLongitude Nullable(Float64)
   ) ENGINE = HaUniqueMergeTree()
   UNIQUE KEY (sensorId, hour)
   ORDER BY sensorId
   PARTITION BY toDate(timestamp)
       TTL timestamp + INTERVAL 3 YEAR
   SETTINGS index_granularity = 8192;
   
   -- Create a distributed table
   CREATE TABLE sensor.heat_sensor_data_unique ON CLUSTER bytehouse_test AS sensor.heat_sensor_data_unique_local ENGINE = Distributed(bytehouse_test, sensor, heat_sensor_data_unique_local);
   ```
   


<span id="29c10a54"></span>
## Step 3: Configure Kafka import task

<span id="ce8905ae"></span>
### Create data source


1. Go to `Data Management and Query>Data Import>Data Source>(top right of the middle column) create data source`.

2. Select the source type as Kafka.

3. Fill in the source name.

4. Fill in the Kafka broker list. Note that different access points must be filled in for different security protocols.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For sensitive internal network security, adopt sasl_ssl; for lower security requirements, using sasl_plaintext is more efficient.   </div>
   

5. Enter the username and password.

6. Click Confirm to verify the connection with Kafka. If the verification passes, the data source will be successfully created.


<span id="0c4375e7"></span>
### Create a new import task


1. Enter the `Console>Data Management and Query>Data Import>Data Source>Details`, then click the `New Import Task` button.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/910103d7292342e5a1115bf00731c8e7~tplv-goo7wpa0wc-image.image) </span>

2. Enter the task name, select the import type as Kafka, and choose the TOPIC (sensor).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3779ce733064422a4be3d517e476f49~tplv-goo7wpa0wc-image.image) </span>

3. Advanced Key Settings

   * We recommend setting the Group Name manually for easier identification during operational tasks, such as bytehouse_sensor_data_consumer.

   * Automatically reset Offset, and choose the Kafka format and delimiter according to individual requirements.

   * It's recommended to input "2" for the number of consumers. If performance is inadequate, you can increase it later (up to a maximum of core count/2).

   * The recommended BlockSize is the default 65536. If you have high real\-time requirements, you can reduce them by half.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fdb141a026f04987b411f0100fa97a4d~tplv-goo7wpa0wc-image.image) </span>

4. Select the target database table:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2645b9ac124440992e9132c2abc1665~tplv-goo7wpa0wc-image.image) </span>

5. Edit mappings between source columns and target columns

   * For scenarios with data in Kafka, selecting "Data Mapping" will sample and analyze a record from the Kafka Topic.

   * For scenarios without data, one can choose JSON and fill in a JSON example for matching.

      Be sure to select "Existing Coverage" as the overwrite method.

      If the target table name and JSON field names are the same, they will automatically match; if different, editing will be required.

      The 'hour' column is a materialized column, not needed for import, and can be deleted by clicking on the right side of the row. There may also be some columns that do not need to be imported into the database, and they can be deleted in this way as well.


Meanwhile, the following common scenarios require special handling and need data conversion from source columns to target columns through import formulas.

<span id="a5aeb7a6"></span>
#### Example of import formulas


* Extraction of Array data:


In this example, the "alertFlags" field only contains the values "overheat" and "humidityDrop", so the data should be extracted into two Boolean columns for overheat and humidityDrop respectively. If "overheat" is present in the array, then set overheat = True.

Therefore, set the overheat column (and similarly the humidityDrop column) as follows:


* Source column: overheat (fill in according to the target column)

* Source data type: Bool (choose according to the target column type)

* Source expression: `has(alertFlags,"overheat")`


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/265dcb8e52184726aae567ea251e19a2~tplv-goo7wpa0wc-image.image" width="581px" /></div>



* JSON multi\-level nesting processing:


For example, if "gpsLatitude" is nested in a mapFloat, it should be extracted to a gpsLatitude column:

```SQL
"mapFloat": {
    "gpsLatitude": -20.510689,
    "gpsLongitude": 42.272274
}
```


Fill in according to the following rules:


* Source column: gpsLatitude (fill in according to the target column)

* Source data type: Float64 (choose according to the target column type)

* Source Expression: `JSONExtract(_content, 'data', 'temperature' ,'Float64')` (Refer to [JSONExtractKeysAndValues(json[, indices_or_keys…], Value_type)](https://docs.byteplus.com/docs/bytehouse/json-functions#jsonextractkeysandvalues-json-indices-or-keys%E2%80%A6-value-type))

* Timestamp Processing:

   1. Timezone: Handle through the expression `toTimezone(timestamp,)` if the import data's timezone and the cluster's timezone are inconsistent.

      * Source Column: timestamp (fill in according to the target column)

      * Source Data Type: DateTime

      * Source Expression: `toTimezone(timestamp, 'Asia/Shanghai')`

   2. Unparsable: Sometimes, the timestamp format might have unparsable formats, such as "2024\-01\-16T12:00:00Z" (timestamp contains the UTC mark) and others. If conversion is possible, this can be tested in the SQL editor with toDateTime(?). If conversion is not possible, you can use the expression `parseDateTimeBestEffortOrNull(timestamp)`.

      * Source Column: timestamp (fill in according to the target column)

      * Source Data Type: **String**

      * Source Expression: `parseDateTimeBestEffortOrNull(timestamp)`

* Special Value Processing:

   * If the source column is Null, but the current field is Not null, use `assumeNotNull(x)`;

   * If the original column is "N/A", it should be converted to empty, use `nullif(x, 'N/A')`;

   * For other references, please refer to the SQL Reference Part of various functions in the Products Manual, and make corresponding adjustments in accordance with the "Log".

6. Submit tasks.

   Submit tasks, Wait. You can also Click **Executions \> Execution ID \> Log** to view the log left by the import, and if there is any data written successfully or failed, it will be recorded in the log. For example,

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2de82533a02f4d2794121a158a9e9fd1~tplv-goo7wpa0wc-image.image) </span>


<span id="fcf587a5"></span>
### Test data

```SQL
select sensorId, timestamp from sensor.heat_sensor_data_unique order by desc limit 10;
```


Run the above command, if data can already be queried, then it indicates the import was successful.
