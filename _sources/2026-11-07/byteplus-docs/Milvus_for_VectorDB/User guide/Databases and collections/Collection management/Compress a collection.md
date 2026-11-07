---
title: "Compress a collection"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Compress_a_collection"
---

You can compress collections as needed to merge small segments, clear delete flags, reduce fragmentation, and improve query efficiency. This topic describes how to compress a collection.

<span id="jtSsW3oh"></span>
## Prerequisites


* Created a Milvus for VectorDB instance and completed authorization. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance) and [Authorize to use an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Authorize_to_use_an_instance).

* Collection has been created. For detailed steps, see [Create a collection](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_a_collection).


<span id="gI8h53w4"></span>
## Precautions


* The compression operation may take some time, especially for large data sets. It is recommended to run compaction during periods of low system activity or planned maintenance to minimize disruption.

* External Collection does not support persistence.


<span id="4ea43Ye0"></span>
## Procedure


1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. In the top navigation bar, select the project and region for collections management.

3. Select **Collections** in the left navigation bar.

4. On the **Collections** page, choose the **Dedicated**, **Serverless**, or **On\-Demand** tab as needed, select the authorized instance, then click **view**.

5. On the **Collections** page, expand the database containing the target Collection, then click the target Collection.

6. In the right panel, select the **Segment** tab, then click **Compact**.

7. In the popup dialog, click **OK**.
