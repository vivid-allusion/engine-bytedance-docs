---
title: "Creating auto-embedding vector index"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/Creating_auto-embedding_vector_index"
---

The auto\-embedding vector index automatically generates vectors by calling the Ark Embedding model, eliminating the need for manual vector data maintenance. This topic describes how to create an auto\-embedding vector index on the MongoDB console.

<span id="4Ed2tnhJ"></span>
## Prerequisite


* You have created a MongoDB 8.3 or later instance and enabled the search feature. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/mongodb/creating_an_instance).

* The instance status is **Running**. For more details about instance status, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

* You have enabled the vector model service on the Ark console and obtained an API Key. For specific steps, refer to [Getting Ark API Key](https://docs.byteplus.com/en/docs/mongodb/data_backup?lang=en).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Currently, MongoDB 8.3 is in the invitation\-only testing phase. To use the auto\-embedding vector search feature, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to contact technical staff and apply for access.</div>


<span id="bKs7P01X"></span>
## Procedure


1. Log on to the [MongoDB console](https://console.byteplus.com/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **AI Capabilities** tab.

6. Under the **Vector index** sub\-tab, click **Createindex**.

7. On the **Create vector index** page, configure the following parameters.



|**Parameter** ||**Required** |**Description** |
|---|---|---|---|
|Index configuration |Search type |Yes |This parameter is fixed as **vector search**,and you do not need to select it. |
||Embedding method<br><br> |Yes<br><br> |Select **Auto**, meaning MongoDB calls the Ark Embedding model to automatically generate vectors and write them to the index.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If the current instance has not yet configured an API Key, go to the <strong>API Key management</strong> tab to fill it out. For specific steps, see <a href="https://docs.byteplus.com/en/docs/mongodb/Getting_Ark_API_Key?lang=en">Getting Ark API key</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">During API Key verification, the instance will enter the <strong>Configuration modifying</strong> status. After the instance recovers to the <strong>Running</strong> state, you can continue to create indexes.</div><br><br><br>* <div data-tips="true" data-tips-type="default">To create a vector index with a <strong>manual</strong> embedding method, see <a href="https://docs.byteplus.com/en/docs/mongodb/create_vector_index?lang=en">Creating vector index</a>.</div><br> |
|Index name and data source |Index name |Yes |Set the index name. The name must meet the following conditions simultaneously:<br><br><br>* Must start with a lowercase English letter.<br><br>* Must end with a lowercase English letter or a number.<br><br>* Can only contain English letters, numbers, underscores (_), and hyphens (\-).<br><br>* The length must be between 3 and 128 characters. For more details, refer to [Constraints and limits](https://docs.byteplus.com/en/docs/mongodb/product-limit#.5Yqf6IO954m55oCn6ZmQ5Yi2).<br><br>* It cannot start with a number or hyphen (\-).<br><br>* Cannot contain spaces, Chinese characters, special characters, or consecutive special symbols.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Within the same instance, the index name must be unique.</div><br> |
||Database name |Yes |Select the database to which the index belongs from the dropdown list.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The database name and table name are both set during database creation. For specific steps, see <a href="https://docs.byteplus.com/en/docs/DBW/database-management-for-mongodb">Database management</a>.</div><br> |
||Collection name |Yes |Select the collection to which the index belongs from the dropdown list.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Both the database name and collection name are set when creating the database. For specific steps, see <a href="https://docs.byteplus.com/en/docs/DBW/database-management-for-mongodb">Database management</a>.</div><br> |



8. After completing the above configuration, click ** Next** in the bottom\-right corner to go to the index configuration page.



|**Parameter** ||**Required** |**Description** |
|---|---|---|---|
|Index field configuration<br><br> |Field\-level vectorization configuration |Yes<br><br> |**Field configuration**<br><br><br>* **Source text field**: Required. Sets the path for the source text field, specifying which field the index should be built on. For more details, refer to [path](https://www.mongodb.com/docs/atlas/atlas-vector-search/vector-search-type/#:~:text=filter%20Type.-,fields.,path,-String).<br><br>* **Embedding model**: Required. Select an embedding model from the dropdown list. Currently, only **doubao\-embedding\-vision\-251215** is supported.<br><br>* **Vector Dimension**: Required. Sets the number of vector dimensions that MongoDB vector search enforces during indexing and querying. Currently, only 1024 and 2048 are supported. For more details, refer to [numDimensions](https://www.mongodb.com/docs/atlas/atlas-vector-search/vector-search-type/#mongodb-vector-search-index-fields:~:text=to%20embedded%20fields.-,fields.,numDimensions,-Int).<br><br>* **Similarity algorithm**: Required. Select a similarity algorithm from the dropdown list. The value range is as follows:<br><br>   * **Dot Product**: Measures similarity based on the angle and magnitude between vectors. For more details, refer to [Dot product](https://en.wikipedia.org/wiki/Dot_product).<br><br>   * **Euclidean distance**: Measures the distance between vector endpoints and can be used to measure similarity from different dimensions. For more details, refer to [Euclidean](https://en.wikipedia.org/wiki/Euclidean_distance).<br><br>   * **Cosine similarity**: Measures similarity based on the angle between vectors, and can be used to measure similarity that is not affected by magnitude scaling. For more details, refer to [Cosine](https://en.wikipedia.org/wiki/Cosine_similarity).<br><br>* **Quantization method**: Optional. Select a quantization method from the dropdown list. Quantization is a technique that reduces the storage space and memory usage of vector search indexes by lowering the precision of vector data. Currently, only **Float** is supported. For more details, refer to [Vector quantization](https://www.mongodb.com/docs/atlas/atlas-vector-search/vector-quantization/#vector-quantization).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Within the same index, different text fields can be associated with distinct embedding models, vector dimensions, similarity algorithms, and quantization methods.</div><br><br><br>* <div data-tips="true" data-tips-type="default">It supports adding multiple field configurations simultaneously.</div><br> |
|Scalar filter field |Field path |No |Optional. Click **Add filter field** to set the path for the scalar filter field of the index.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">For nested fields, use dot notation to specify the path of the embedded field. You only need to enter the field's key; no need to enter the field type. For example, name and info.age are valid values.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can add multiple filter fields simultaneously, up to 20.</div><br> |



9. After the index configuration is complete, click **Next** to confirm creation information such as basic information and auto embedding field configurations.

10. After confirming, click **OK** to complete the index creation.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Index creation is an <strong>asynchronous operation</strong> and takes some time to complete. It is recommended to search only after confirming the index status becomes <strong><code>READY</code></strong>. For more information about the index status, see <a href="https://www.mongodb.com/zh-cn/docs/manual/reference/operator/aggregation/listsearchindexes/#mongodb-search-index-statuses">$listSearchIndexes (Aggregation Stages)</a>.</div>
