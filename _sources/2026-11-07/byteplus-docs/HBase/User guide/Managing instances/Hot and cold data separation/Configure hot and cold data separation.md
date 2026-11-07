---
title: "Configure hot and cold data separation"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Configure_hot_and_cold_data_separation"
---

To separate hot and cold data, data needs to be stored based on time boundaries. This article describes how to set the hot and cold separation time boundary points.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Capacity storage has been enabled for the instance. For more information, see [Enabling Capacity storage](https://docs.byteplus.com/en/docs/HBase/Enabling_Capacity_storage).

* Connected to the HBase instance:

   * Connect instances through the HBase Shell, see [Connecting to the instance using the HBase Shell](https://docs.byteplus.com/en/docs/HBase/Connecting_to_the_instance_using_the_HBase_Shell).

   * Connect instances through Java API, see [Connecting to the instance using the Java API](https://docs.byteplus.com/en/docs/HBase/Connecting_to_the_instance_using_the_Java_API).


<span id=".6K6-572u5Ya354Ot5YiG56a75pe26Ze05YiG55WM54K5"></span>
## Set the hot and cold separation time boundary point 

By adjusting `COLD_BOUNDARY`, you can set the hot and cold separation time boundary point in seconds. The values are as follows:


* A value greater than 0 indicates that data before this point in time is stored in cold storage. For example, if the value is set to 86400 seconds (24 hours), data written 24 hours ago will be automatically archived to cold storage.

* Setting the value to `-1`, `0`, or removing the attribute, disables hot and cold data separation.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After modifying the hot/cold separation boundary or canceling hot/cold separation, you need to wait until the next compaction is completed (a random number between 3.5 and 10.5 days) before data can be migrated according to the new hot/cold separation boundary. If you want to migrate data immediately, you can execute <code>major_compact 'tableName'</code> or <code>major_compact 'regionName'</code> in the HBase command line. For more information about the <code>major_compact</code> command, run <code>help "major_compact"</code> to view details.</div>


<span id="hbase-shell"></span>
### HBase Shell


* Create a hot and cold separation table and set the hot and cold separation time boundary points.

   Example: Create table `ch_table` and set the hot/cold separation time boundary to 86400 seconds (24 hours). This means that data written 24 hours ago will be automatically archived to Capacity storage.

   ```sql
   hbase(main):002:0> create 'ch_table', {NAME=>'f', COLD_BOUNDARY=> 86400}
   ```
   

   Parameter description:

   * `NAME`: The column family that requires hot and cold separation.

   * `COLD_BOUNDARY`: The boundary point between cold and hot separation, unit: second (s).

* Set the hot/cold separation time boundary for an existing table, or modify the hot/cold separation time boundary.

   ```sql
   hbase(main):003:0> alter 'ch_table', {NAME=>'f', COLD_BOUNDARY=> 86400}
   ```
   

* Cancel the separation of hot and cold data.

   ```sql
   hbase(main):004:0> alter 'ch_table', {NAME=>'f', COLD_BOUNDARY=> -1}
   ```
   


<span id="hbase-java-api"></span>
### HBase Java API


* Create a hot and cold separation table and set the hot and cold separation time boundary points.

   ```java
   Admin admin = connection.getAdmin();
   TableName tableName = TableName.valueOf("ch_table");
   HTableDescriptor descriptor = new HTableDescriptor(tableName);
   HColumnDescriptor cf = new HColumnDescriptor("f");
   cf.setValue(COLD_BOUNDARY, "86400");
   descriptor.addFamily(cf);
   admin.createTable(descriptor);
   ```
   

* Set the hot/cold separation time boundary for an existing table, or modify the hot/cold separation time boundary.

   ```java
   HTableDescriptor descriptor = admin
       .getTableDescriptor(tableName);
   HColumnDescriptor cf = descriptor.getFamily("f".getBytes());
   cf.setValue(COLD_BOUNDARY, "86400");
   admin.modifyTable(tableName, descriptor);
   ```
   

* Cancel the separation of hot and cold data.

   ```java
   HTableDescriptor descriptor = admin
       .getTableDescriptor(tableName);
   HColumnDescriptor cf = descriptor.getFamily("f".getBytes());
   cf.setValue(COLD_BOUNDARY, -1);
   admin.modifyTable(tableName, descriptor);
   ```
   


<span id="vWYvbDF0"></span>
## Data writing

The hot and cold separation table is exactly the same as the normal table data writing method, and the data writing timestamp uses the current time. Data is first stored in hot storage when writing. Over time, if the current time of the data \- write time \> the threshold specified by `COLD_BOUNDARY`, it will be archived to cold storage after major_compact.

<span id="NuvZ15kQ"></span>
## Data reading

Hot and cold data are stored in the same table, so only one table needs to be interacted with when reading data. You can set `HOT_ONLY` directly in the `Get/Scan` command to query only hot data. You can also set `TimeRange` to limit the data time range. HBase automatically compares the set `TimeRange` with `COLD_BOUNDARY` to decide whether to query hot data, cold data, or both hot and cold data. If neither is set, the result of the merged cold data and hot data is accessed in parallel. The query cold data latency is higher than the hot data latency, and the query throughput will be limited by cold storage.

<span id=".6ZqP5py65p-l6K-i77yIZ2V077yJ"></span>
### Random query (Get)

<span id="hbase-shell"></span>
#### HBase Shell


* Specify `HOT_ONLY` to query only hot data.

   ```sql
   hbase(main):001:0> get 'ch_table', 'row1', {HOT_ONLY=>true}
   ```
   

* `HOT_ONLY` is not specified, and cold and hot data are queried at the same time.

   ```sql
   hbase(main):002:0> get 'ch_table', 'row1'
   ```
   

* Specify `TimeRange` (Unix timestamp, unit in milliseconds (ms)), and the system will compare `TimeRange` and `COLD_BOUNDARY`, and decide whether to query hot data, cold data or simultaneously query hot data and cold data.

   ```sql
   hbase(main):003:0> get 'ch_table', 'row1', {TIMERANGE => [0, 1568203111265]}
   ```
   


<span id="hbase-java-api"></span>
#### **Does HBase** **Java API**


* Specify `HOT_ONLY` to query only hot data.

   ```java
   get = new Get("row1".getBytes());
   get.setAttribute(HOT_ONLY, Bytes.toBytes(true));
   ```
   

* `HOT_ONLY` is not specified, and cold and hot data are queried at the same time.

   ```java
   Get get = new Get("row1".getBytes());
   System.out.println("result: " + table.get(get));
   ```
   

* Specify `TimeRange` (Unix timestamp, unit in milliseconds (ms)), and the system will compare `TimeRange` and `COLD_BOUNDARY`, and decide whether to query hot data, cold data or simultaneously query hot data and cold data.

   ```java
   get = new Get("row1".getBytes());
   get.setTimeRange(0, 1568203111265)
   ```
   


<span id=".6IyD5Zu05p-l6K-i77yIc2Nhbu-8iQ=="></span>
### Range query (Scan)

<span id="hbase-shell"></span>
#### HBase Shell


* Specify `HOT_ONLY` to query only hot data.

   ```sql
   hbase(main):001:0> scan 'ch_table',  {STARTROW =>'row1', STOPROW=>'row9', HOT_ONLY=>true}
   ```
   

* `HOT_ONLY` is not specified, and cold and hot data are queried at the same time.

   ```sql
   hbase(main):002:0> scan 'ch_table',  {STARTROW =>'row1', STOPROW=>'row9'}
   ```
   

* Specify `TimeRange` (Unix timestamp, unit in milliseconds (ms)), and the system will compare `TimeRange` and `COLD_BOUNDARY`, and decide whether to query hot data, cold data or simultaneously query hot data and cold data.

   ```sql
   hbase(main):003:0> scan 'ch_table',  {STARTROW =>'row1', STOPROW=>'row9', TIMERANGE => [0, 1568203111265]}
   ```
   


<span id="hbase-java-api"></span>
#### HBase Java API


* Specify `HOT_ONLY` to query only hot data.

   ```java
   scan = new Scan();
   scan.setAttribute(HOT_ONLY, Bytes.toBytes(true));
   ```
   

* `HOT_ONLY` is not specified, and cold and hot data are queried at the same time.

   ```java
   Scan scan = new Scan();
   ResultScanner scanner = table.getScanner(scan);
   for (Result result : scanner) {
       System.out.println("scan result:" + result);
   }
   ```
   

* Specify `TimeRange` (Unix timestamp, unit in milliseconds (ms)), and the system will compare `TimeRange` and `COLD_BOUNDARY`, and decide whether to query hot data, cold data or simultaneously query hot data and cold data.

   ```java
   scan = new Scan();
   scan.setTimeRange(0, 1568203111265);
   ```
