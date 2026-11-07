---
title: "FAQs about products"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/FAQs_about_products"
---

1. **How long does it take for indexes to update after I modify or delete data in VikingDB?** 


VikingDB updates indexes within 3 seconds after you write, modify, or delete data. The maximum delay is 20 seconds.


2. **How does VikingDB charge for usage?** 


VikingDB uses postpaid billing. It is billed hourly based on the usage of all its billing items. For more information, see [Billing](https://docs.byteplus.com/en/docs/VikingDB/Billing_of_a_vector_database).


3. **Can embedding results vary for the same text?** 


Yes. Variations may occur due to inference precision loss. Variations are typically less than 0.1% and do not affect search performance.


4. **Is there a limit on the number of collections?** 


Yes. Currently, each user can create up to 200 collections, up to 200 indexes in total, and up to 100 indexes in a single collection.


5. **When should I use partitions?** 


Partitions are designed to efficiently filter data during retrieval. Use partitions when your retrieval scenario requires filtering specific data types. For example, in image retrieval, if each query targets a specific format such as JPG or PNG, you can create partitions by format.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Each collection supports up to 1,000 partitions. You must specify the target partitions in each query.</div>



6. **Does** **upserting a vector with a duplicate primary key update the existing record?** 


Yes. If the row of data to upsert has the same primary key as an existing row of data in the collection, the existing row of data is overwritten. Otherwise, the new row of data is upserted.


7. **How many rows of data can I write at most at a time?** 


You can write up to 100 rows of data at a time to a specified collection.


8. **Is there a limit on the number of fields in a collection?** 


We recommend you limit the number of fields to 200. For special requirements, contact support.


9. **Can the system update an index in the streaming mode after data insertion?** 


Yes. The system supports streaming updates to the index.

Note: Asynchronous writes do not trigger streaming updates.


10. **Can I get the entire dataset from the vector database via an API?** 


No. The vector database may contain tens or hundreds of millions of records, which cannot be returned through an API. You can use the data export feature to retrieve all records.


11. **How do I confirm whether a record was successfully** **upserted?** 


Each type of request returns a success response if the request succeeds. Some SDKs treat the absence of an error as success. A success response indicates that the record was successfully written.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Asynchronous writes may take several hours to appear in the database.</div>



12. **How do I confirm whether a specific record exists in the vector database?** 


If you know the primary key, search for the record by primary key. If you do not know the primary key, use scalar filtering to search for the record.


13. **What is the difference between HNSW\-Hybrid and HNSW indexes?** 


HNSW\-Hybrid is an HNSW algorithm that supports hybrid indexing. It indexes both dense vectors and sparse vectors in the same collection simultaneously and returns results that consider the similarities of both types during retrieval.

HNSW\-Hybrid applies to use cases that require high search performance and **simultaneous retrieval of dense and sparse vectors**.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Dense vector:</strong> A dense vector is a high\-dimensional vector in which most elements are non\-zero. This structure performs well in scenarios where data is evenly distributed and all dimensions need to be fully utilized. Common use cases include:</div>



* <div data-tips="true" data-tips-type="tip"><strong>Natural language processing (NLP)</strong>: Embedding models represent words as dense vectors, with each dimension containing semantic information. This enables the model to capture semantic relationships between words.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Image processing</strong>: Features extracted by convolutional neural networks (CNNs) are typically dense vectors. They are used in classification and detection tasks to capture both global and local image features.</div>



<div data-tips="true" data-tips-type="tip"><strong>Sparse vector:</strong></div>


<div data-tips="true" data-tips-type="tip">A sparse vector is a high\-dimensional vector in which most elements are zero. Only a small number of dimensions have non\-zero values. This structure performs well in processing large\-scale, high\-dimensional, and sparse data. Common use cases include:</div>



* <div data-tips="true" data-tips-type="tip"><strong>Text analysis</strong>: Bag\-of\-words (BoW) models represent documents as sparse vectors. Each dimension corresponds to a word, and only words that appear in the document have non\-zero values.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Recommendation system</strong>: In a user\-item interaction matrix, a user's ratings can be represented as a vector where each dimension corresponds to an item. Because most users interact with only a few items, the matrix is typically sparse.</div>


14. **What is the difference between Euclidean distance (L2), inner product (IP), and cosine similarity? Which one should I use when creating an index?** 


**Euclidean distance (L2):** 

Euclidean distance measures the distance between two vectors in Euclidean space. A smaller distance indicates higher similarity. The value range is  **[0, +∞)** .

The Euclidean distance is calculated as:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d49b796482f24148ab9e2bbf25dafd19~tplv-goo7wpa0wc-image.image) </span>

where **a = (a(0), a(1),..., a(n\-1))**  and **b = (b(0), b(1),..., b(n\-1))**  are two points in the *n*\-dimensional Euclidean space.

**L2 is effective for continuous data.** 

**Inner product (IP):** 

The inner product measures similarity between two embedding vectors. It is useful when you process unnormalized vectors or when both vector magnitude and direction are relevant. A larger inner product indicates higher similarity. The value range is  **(−∞, +∞)** .

The inner product is calculated as:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16cf0e9f897043b49b78280ad8d3e0e1~tplv-goo7wpa0wc-image.image) </span>

**Cosine similarity:** 

Cosine similarity measures the similarity between two vectors by the cosine of the angle between the two vectors. The two vectors can be thought of as two line segments originating from the same point (such as [0,0,...]) and pointing in different directions.

The value range of cosine similarity is  **[−1, 1]** . An angle closer to 0° results in a similarity closer to **1**. An angle of **90°**  results in a similarity of **0**. An angle closer to **180°**  results in a similarity closer to  **−1**. A higher cosine value indicates a smaller angle between the vectors, signifying greater similarity. \*\* \*\*

Given vectors: **A = (a(0), a(1),..., a(n−1))**  and **B = (b(0), b(1),..., b(n−1))** , cosine similarity is calculated as:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4bf21d3a52cb46f6bb5a222c2abaeb13~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The retrieval score is processed so that a higher score indicates greater similarity to the candidate vector.</div>


Score calculations for different distance types:


|**Distance Type** |**Retrieval Score** |**Score Range** |
|---|---|---|
|Euclidean distance (L2) |1 \- l2_distance |(\-∞, 1] |
|Inner product (IP) |ip_distance |(\-∞, +∞) |
|Cosine similarity |cosine_distance |[\-1, 1] |


The formulas show that **retrieval scores can be negative**, regardless of the distance type.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When creating an index, use the same distance type as used during model training.</div>



15. **Why does a top‑k search return fewer than k results?** 


When scalar filtering, primary key filtering, or post\-processing operators are applied, the number of retrieved results may be less than k.


16. **What is the maximum number of vector dimensions supported in VikingDB?** 


VikingDB supports dimensions from 4 to 4096. The number of dimensions must be a multiple of 4.


17. **What data types are supported for primary keys?** 


Primary keys support int64 and string.


18. **Does VikingDB support horizontal scaling?** 


VikingDB handles scaling automatically, so you do not need to manually manage nodes or storage. To increase query throughput (QPS), you can vertically scale an index by updating its CU setting to access more CPU resources.


19. **How does VikingDB manage data types and precision?** 


Vectors are stored in collections in float32 format to preserve numerical precision. During indexing, you can configure compression parameters to slightly reduce precision in exchange for lower resource usage.


20. **Can I set default values for scalar or vector fields?** 


You can set default values for scalar fields on the collection creation page or by using the default_val parameter in the collection creation API or SDK.

Setting default values for vector fields is not supported.


21. **What is the difference between subindexes and filters?** 


A subindex is a logical partition of a collection.

A filter allows users to specify filtering conditions using a structured syntax. A filter query applied to all partitions filters across the full collection. A filter query applied to a subindex filters only within that subindex. Filtering does not operate on physical storage partitions. It filters data by matching query conditions.


| |**Subindex** |**Filter** |
|---|---|---|
|**Definition** |Logical or physical partition of data |Data filtering language |
|**Filter scope** |Defined at subindex creation |Applied to the selected data range |
|**Use case** |Static and predefined grouping scenarios |Flexible and dynamic query scenarios |



22. **Why does CU usage in billing differ from the CPU resources purchased during index creation?** 


CU usage is based on the greater of CPU or memory consumption, calculated as: CU = MAX(CPU, MEM/8). When memory usage exceeds eight times the number of CPU cores, CU usage is determined by memory consumption divided by 8.

Because memory scales automatically, the memory\-to\-CPU ratio may exceed 8:1, resulting in billed CU usage that is higher than the number of purchased CPU cores.


23. **Does VikingDB support keyword retrieval?** 


Yes. You can perform **keyword retrieval** by using a post\-processing operator after vector retrieval.

Use the `string_match` parameter to apply regular expression filtering to text fields in the results. For example, you can retain results where the title or description field contains specific keywords, or exclude results with special characters, ad terms, or irrelevant content.

For the specific syntax, refer to [Syntax](https://github.com/google/re2/wiki/syntax).

```TypeScript
// Example: Retain only results where the title contains "VikingDB" 
{"op":"string_match", "field":"title", "pattern":"(?i)VikingDB"},
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To enhance keyword retrieval performance during vectorization, use <strong>sparse vectors</strong>. You can adjust the relative importance of semantic matching (dense vectors) and keyword matching (sparse vectors) by using the <code>dense_weight</code> parameter.</div>



24. **How do I prevent a result from appearing too frequently?** 


You can **control result frequency** by using a post\-processing operator after vector retrieval.

Use the `enum_freq_limiter` parameter to limit how many times a specific field value appears in the results. For example, you can use this parameter to prevent a single brand or creator from appearing many times in the results.

```TypeScript
// Example: Limit the number of times a single brand appears in the results to 5 
{"op": "enum_freq_limiter", "field": "brand", "threshold": 5}
```



25. **When using the image\-text embedding model, if only one image is sent in the request, why are there still text tokens in the returned token usage?** 


The image vectorization process uses internal prompt words. Depending on the input format (pure text, pure image, or a combination), the model uses one of three fixed sets of prompt words, which adds a small number of text tokens (approximately 20) to the total.
