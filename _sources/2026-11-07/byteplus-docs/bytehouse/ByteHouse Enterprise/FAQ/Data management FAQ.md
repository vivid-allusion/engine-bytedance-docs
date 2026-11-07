---
title: "Data management FAQ"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/data-management-faq"
---

<span id="q1：ttl-的设置是什么级别的粒度？"></span>
## Q1: What level of granularity does the TTL setting apply to?

ByteHouse Enterprise Edition supports TTL (time to live) settings at three granularities: table, partition, and row level.


|TTL Type |Description |Configuration method |
|---|---|---|
|Table level |Applies to all data in the entire table, suitable for scenarios requiring a unified expiration rule for the full table data. |Configure through the ByteHouse console. For more configuration details, refer to [Create a new database/table](https://docs.byteplus.com/docs/bytehouse/create-a-new-database-table). |
|Partition level |Allows settings for specific partitions of the table, providing finer lifecycle management and enabling independent expiration policies for different partitions. |Set manually by writing DDL statements after connecting to ByteHouse via clients like CLI or JDBC.<br><br><br>* For TTL configuration details, refer to [TTL](https://docs.byteplus.com/docs/bytehouse/ttl).<br><br>* For detailed steps on connecting a client to a ByteHouse cluster, see [Connection](https://docs.byteplus.com/en/docs/bytehouse/connection). |
|Row level |Acts on single rows based on the time value in a specific column (for example, the `event_time` column), offering the finest control granularity. Suitable for scenarios where expiration depends on each record's specific time attribute. ||


<span id="df0b37ba"></span>
## Q2: When using the ClickHouse Community Edition , data skew occurs after importing Kafka data nodes. Can ByteHouse avoid this issue, and how to configure it?

Data skew may be caused by the Community Edition Kafka engine's dynamic Partition allocation: when the mapping between Kafka partitions and ClickHouse nodes changes dynamically, some nodes may process too much partition data, causing uneven load. The ByteHouse [HaKafka](https://docs.byteplus.com/docs/bytehouse/hakafka) engine (modified engine based on the community edition) uses static Partition allocation to avoid skew caused by dynamic allocation.

If you need to import Kafka data into ByteHouse, it is recommended to use the [Streaming import](https://docs.byteplus.com/docs/bytehouse/streaming-import) function in the ByteHouse Enterprise Edition console. The system will enable static partition allocation by default, effectively preventing node data skew without additional configuration.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The static allocation of the HaKafka engine is based on the partition data distribution of the Kafka source. If upstream Kafka has partition data skew (such as some partitions having much larger data volumes than others), node load imbalance may still occur after import. Therefore, confirm that the data distribution across each upstream Kafka partition is balanced before using stream import.</div>


<span id="8652a9b0"></span>
## Q3: When writing via JDBC using insert\-select, if writing fails, is there any data loss?

Yes, partial data was successfully written, which poses a risk of data loss. This is because ByteHouse's `INSERT INTO ... SELECT ...` operation does not guarantee atomicity.

If a write failure occurs, retrying the following methods is suggested to ensure data consistency:


*  **(Recommended) Option 1: Create the target table using the HaUniqueMergeTree engine**

   Using the HaUniqueMergeTree table is suggested. This engine supports an automatic deduplication mechanism based on unique keys, ensuring data accuracy and consistency even if retries cause repeated writes. Therefore, when a write failure occurs on a HaUniqueMergeTree table, simply retry without additional duplicate data handling.

   For the HaUniqueMergeTree table creation method, please refer to [HaUniqueMergeTree](https://docs.byteplus.com/docs/bytehouse/hauniquemergetree).

* **Option 2: Truncate the target table and retry**

   If the target table is not suitable for HaUniqueMergeTree, truncate the target table and retry. Examples are as follows:

   1. Before retrying the write operation, run the `TRUNCATE TABLE target_table` command to empty the data in the target table (including the part already written when it failed).

      ```SQL
      TRUNCATE TABLE example_table; 
      ```
      

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">This operation will clear all existing data in the target table (including any partially successfully written data), so it is only recommended when the data can be fully regenerated and the intermediate state is not dependent. Carefully evaluate its impact on business operations.      </div>
      

   2. Re\-execute the complete `INSERT INTO ... SELECT ...` statement.

      ```SQL
      INSERT INTO example_table SELECT * FROM example_table 
      ```
      


<span id="9e2730eb"></span>
## Q4: Does ByteHouse support async insert (asynchronous write)?

ByteHouse does not currently support the async insert function of ClickHouse community version, but similar functionality can be achieved through batch writes via WAL (Write\-Ahead Log).

<span id="70866076"></span>
## Q5: Does ByteHouse support monitoring changes to S3 or TOS via S3 Queue?

ByteHouse Enterprise supports external table import from S3 or data querying, but currently does not support monitoring changes to S3 or TOS for real\-time data import into ByteHouse.
