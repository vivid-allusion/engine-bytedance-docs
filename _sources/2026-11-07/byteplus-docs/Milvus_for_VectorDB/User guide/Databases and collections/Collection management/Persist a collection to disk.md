---
title: "Persist a collection to disk"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Persist_a_collection_to_disk"
---

You can persist a collection when you need to write data from memory to persistent storage. This topic describes how to persist a collection.

<span id="tSAfWMvH"></span>
## Prerequisites


* Created a Milvus for VectorDB instance and completed authorization. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance) and [Authorize to use an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Authorize_to_use_an_instance).

* Collection has been created. For detailed steps, see [Create a collection](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_a_collection).


<span id="27gSzGTs"></span>
## Precautions


* It is recommended to persist at the end of an insertion session to prevent data fragmentation.

* For large datasets, flushing to disk may take some time.

* External Collection is not supported for flushing to disk.


<span id="27gSzGTs"></span>
## Procedure


1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. In the top navigation bar, select the project and region for collections management.

3. Select **Collections** in the left navigation bar.

4. On the **Collections** page, select the **Dedicated**, **Serverless**, or **On\-Demand** tab as needed, choose an Authorized instance, then click **view**.

5. On the **Collections** page, expand the database containing the target collection, then click the target collection.

6. In the right panel, select the **Segment** tab, then click **Flush**.

7. In the popup dialog, click **OK**.
