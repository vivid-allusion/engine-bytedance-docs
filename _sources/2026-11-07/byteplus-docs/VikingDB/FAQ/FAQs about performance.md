---
title: "FAQs about performance"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/FAQs_about_performance"
---

1. **What factors affect CPU usage?** 


QPS: Higher queries per second increase CPU load, as more requests are processed concurrently.

A large topk value increases the computational and sorting workload.

DSL: A complex DSL increases CPU usage due to more complex parsing and execution logic.


2. **Does concurrent data insertion affect query performance?** 


No. VikingDB uses a compute\-storage separation architecture. Data insertion does not affect query performance.


3. **What are the data write throughput limits?** 


Synchronous writes are limited to 1,000 records per second while asynchronous writes are limited to 10,000 records per second. If vectorization is required, consider token rate limits as well.


4. **Do I need to refresh the index to query newly inserted, deleted, or updated data?** 


No. The latest data is immediately available for query without a refresh.


5. **Does database size affect query performance when searching a specific subindex?** 


No. If a subindex is specified, VikingDB searches only within that subindex.


6. **Why does the estimated QPS shown on the index creation page differ from the actual measured QPS?** 


The QPS shown on the index creation page is an estimate based on the configured CU. However, the CPU usage of a single request is closely related to request parameters such as the limit value and filter conditions. CPU consumption varies across use cases, which can lead to significant differences in achievable QPS under the same CU configuration.


7. **How can I estimate resource usage based on the business scenario?** 


We recommend consulting with the product solution team for guidance. An automatic resource estimation feature will be available in the future.


8. **What is the data volume limit for a single collection? At what scale does search performance degrade?** 


There is no limit on the number of records in a single collection.

Search performance may be affected when the data volume exceeds one million records. The extent of the impact depends on factors such as vector dimension, filter conditions, index type, and quantization method.


9. **How many replicas serve queries, and how are compute resources allocated?** 


VikingDB provides at least two service replicas. Compute resources are distributed evenly across replicas based on traffic.


10. **Why is a search request rate\-limited with error code 1000029 ("Request limit reached") even when CU usage is below the limit?** 


This may occur if the request does not follow the expected usage pattern, causing the collection or index interface to be rate\-limited.

Initialize the index and collection only once. Do not reinitialize them with every search request.
