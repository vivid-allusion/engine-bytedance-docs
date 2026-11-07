---
title: "View collection details"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/View_collection_details"
---

After creating a collection, you can view the details of the collection. This topic describes how to view collection details.

## Prerequisites

* Created a Milvus for VectorDB instance and completed authorization. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance) and [Authorize to use an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Authorize_to_use_an_instance).

* Collection has been created. For specific steps, refer to [Create collection](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_a_collection).

## Procedure

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. In the top navigation bar, select the project and region for collections management.

3. Select **Collections** in the left navigation bar.

4. On the **Collections** page, select the **Dedicated**, **Serverless**, or **On\-Demand** tab, choose an authorized instance, then click **view**.

5. On the **Collections** page, click the target database, select the target Collection, then view the Collection details on the right side, which include the following tabs.

   |Tab |Description |
   |---|---|
   |Schema |Display basic schema information, including consistency, creation time, number of shards, Mmap settings (supported only by Dedicated edition instances), Entities (approximately), time zone (supported only by version 2.6 and 3.0 instances), Collection type (supported only by On\-Demand edition instances), replicas, description, and field details. You can click **View configurations** to see configuration information for each field. Version 2.6 and 3.0 instances also support adding scalar fields.<br><br>> **tip**<br><br><br>> Milvus version 3.0 currently requires whitelist access; to use it, please [submit a ticket](https://console.byteplus.com/workorder/create/?step=2&SubProductID=P00000255) for approval.<br> |
   |Vector search |Provide query operations on the Collection based on vector similarity. You can enter or generate query vectors, select a vector field and similarity metric, and combine conditions such as TopK, similarity range, scalar filter expressions, and partition filtering to complete the vector search request. |
   |Data overview |Display data in the Collection. You can filter data by expression, display fields, and consistency.<br><br>You can also click **Insert sample data** and enter the number of sample data rows to insert randomly generated data matching the Collection Schema into the Collection for testing and development scenarios.<br><br>> **tip**<br><br><br><br>* > Data overview is visible after the collection is loaded. For detailed operations, refer to [Load and release a collection](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Load_and_release_a_collection).<br><br><br>* > Insert up to 100 sample data entries at a time.<br> |
   |API Playground |Provide APIs for adding, deleting, updating, and querying data. The following APIs are currently supported: Insert Data, Search Data, Hybrid Search Data, Get Data, Upsert Data, and Delete Data.<br><br>> **tip**<br><br><br>> Read operations such as Get, Query, and Search require the Collection to be loaded and visible. For detailed operations, refer to [Load and release a collection](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Load_and_release_a_collection).<br><br><br>You can also click to generate client code for calling APIs on other platforms. The currently supported platforms are: shell\-curl, Go, Java \- OkHttp, and Python. |
   |Segment |Display Segment details, including Segment ID, Level, Partition ID, persistent segment status, lines, query node ID, and query segment status. You can click **Compact** or **Flush** to execute compression or flush operations. For specific operations, see [Compress Collection](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Compress_a_collection) and [Persist Collection](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Persist_a_collection_to_disk). |
   |Partition |Displays the partition list in the Collection, including Partition ID, Partition name, Entities (approximately), Creation time, and actions. You can click **Create partition** to create a new partition. Version 2.6 instances also support loading and releasing partitions based on usage to save memory.<br><br>> **tip**<br><br><br>> External Collection is not included in this tab.<br> |
   |Property |Displays the current Collection configuration, which you can modify according to business needs. For detailed instructions, see [Modify Collection Configuration](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Modify_collection_configuration).<br><br>> **tip**<br><br><br>> External Collection does not include this tab.<br> |
   |Monitoring |Displays current collection monitoring data, including read request QPS, read failures, average read latency, Search request VPS, write failures, P99 write latency, insert request VPS, upsert request VPS, index file storage size, partition count (supported only in Dedicated instance collections), binlog storage size, and data count (supported only in Dedicated instance collections).<br><br>By default, monitoring data from the past 1 hour is shown; you can view data up to the past month. You can customize the viewing time range on the page’s time window, accurate to the minute. The maximum time range interval is 14 days. The Milvus for VectorDB version also offers quick options for 3 hours, 6 hours, 12 hours, 1 day, 3 days, and 7 days.<br><br>If you check **chart linkage**, when hovering over any monitoring chart to view the specific value of that item at a certain time, the exact values of other items under the current monitoring category at that time will also display synchronously in their corresponding charts. |
