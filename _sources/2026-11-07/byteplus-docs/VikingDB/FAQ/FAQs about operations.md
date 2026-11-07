---
title: "FAQs about operations"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/FAQs_about_operations"
---

<span id="FAQs about operations"></span>
# FAQs about operations


1. **What affects the recall rate in VikingDB?** 


The recall rate mainly depends on the index configuration:


* For a **FLAT index**, the recall rate is 100%.

* An **HNSW index** supports quantization. For example, by converting float to int8, you can reduce memory usage from 4 bytes to 1 byte. This improves performance by up to 40%, with only a 2% to 3% loss in precision.

* **Search parameters** also affect the recall rate. For example, by increasing the sef parameter, you can raise the number of nodes searched in the graph, which improves recall but decreases query performance.

2. **Why does the number of records on the frontend differ from the number of records written?** 


For performance reasons, the system estimates the number of records by sampling. This introduces a margin of error but does not affect usage.


3. **Can I create an index before inserting data into a collection?** 


Yes. You can create an index before inserting data. Once the index is built, newly written data becomes searchable in real time.


4. **Why are fewer results returned than the limit set in a query?** 


This may occur in two cases:

The collection contains fewer records than the specified limit.

There are not enough records that meet the filter criteria.


5. **Why is the HNSW\-Hybrid algorithm not available during index creation?** 


The HNSW\-Hybrid algorithm is only available if the collection includes sparse vectors.

To enable it, use the bge\-m3 model to convert text fields into sparse vectors, or add sparse_vector fields to import sparse vectors.
