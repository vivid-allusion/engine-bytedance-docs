---
title: "Clone a collection schema"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Clone_a_collection_schema"
---

When you want to reuse the schema of an existing collection, you can clone the collection schema to create a new collection with the same schema without copying data. The cloning scope includes schema and index information. This topic describes how to clone a collection schema.

<span id="ByLMziEZ"></span>
## Prerequisites


* Created a Milvus for VectorDB instance and completed authorization. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance) and [Authorize to use an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Authorize_to_use_an_instance).

* Collection has been created. For specific steps, refer to [Create collection](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_a_collection).


<span id="IXJSU3se"></span>
## Procedure


1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. In the top navigation bar, select the project and region for collections management.

3. Select **Collections** in the left navigation bar.

4. On the **Collections** page, choose the **Dedicated**, **Serverless**, or **On\-Demand** tab, select the authorized instance, then click **view**.

5. On the **Collections** page, expand the database containing the target Collection, then select   **... \> Clone collection schema** on the right of the target Collection.

6. In the **Clone collection schema** dialog, configure the following parameters, then click **OK.** 

   
   |Parameter |Description |
   |---|---|
   |Database name |Select the database where the collection will be created from the dropdown list. |
   |Collection Name |Enter the name of the collection. Naming rules are as follows:<br><br><br>* Cannot start with a number or underscore (_).<br><br>* The length must be between 1 and 64 characters.<br><br>* Can only contain letters, digits, and underscores (_). |
   |Remarks (optional) |Enter remarks for the collection. Supports up to 255 characters. |
   |Shard Num |Set the number of shards. The recommended number of shards depends on the expected write volume and concurrency level. A general reference standard is 1 shard per 100 million expected rows of data. Increasing the number of shards may improve data ingestion speed but will also increase resource consumption. |
