---
title: "Editing vector index"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/Editing_vector_index"
---

A vector index is the foundation for implementing MongoDB vector search, and its configuration directly affects retrieval effectiveness, storage cost, and query performance. When business requirements change, you can adjust relevant parameters by editing the index configuration. This topic describes how to edit a vector index on the console.

<span id="q8heASkK"></span>
## Prerequisite


* You have created a MongoDB 8.3 or later instance and enabled the search feature. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/mongodb/creating_an_instance).

* The instance status is **Running**. For more details about instance status, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

* At least one vector index has been created for the instance. For specific procedures, refer to [Creating vector index](https://docs.byteplus.com/en/docs/mongodb/create_vector_index).


<span id="IrZ0sIhw"></span>
## Precautions


* Currently, only indexes with a manual embedding method are supported for editing.

* Index names, database names, and table names are not editable at this time.


<span id="NSTAaKay"></span>
## Procedure


1. Log on to the [MongoDB console](https://console.byteplus.com/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **AI capabilities** tab.

6. On the index list under the **Vector index** sub\-tab, find the target index, then click **Edit** in the **Actions** column on the right.

7. In the pop\-up **Edit vector index** panel, modify the following parameters as required by your business.



|**Parameter** ||**Required** |**Description** |
|---|---|---|---|
|Configuration |Configuration method<br><br> |Yes |You can choose the **Visual editor** and **JSON editor** for configuration.<br><br><br>* **Visual editor**<br><br>   * Vector field<br><br><br>Required. Click **Add vector field,**  to configure the following parameters:<br><br><br>      * **Field path**: Set the field path, which specifies the field on which the index needs to be built. For more details, refer to [path](https://www.mongodb.com/docs/atlas/atlas-vector-search/vector-search-type/#:~:text=filter%20Type.-,fields.,path,-String).<br><br>      * **Vector dimensions**: Set the number of vector dimensions enforced by MongoDB vector search during indexing and querying. Value range: 1~8192. For more details, refer to [numDimensions](https://www.mongodb.com/docs/atlas/atlas-vector-search/vector-search-type/#mongodb-vector-search-index-fields:~:text=to%20embedded%20fields.-,fields.,numDimensions,-Int).<br><br>      * **Similarity calculation method**: Select a similarity algorithm from the drop\-down list. The value range is as follows:<br><br>         * **Dot Product (default)** : Measures similarity based on the angle and magnitude between vectors. For more details, refer to [Dot product](https://en.wikipedia.org/wiki/Dot_product).<br><br>         * **Euclidean distance**: Measures the distance between vector endpoints and can be used to measure similarity from different dimensions. For more details, refer to [Euclidean](https://en.wikipedia.org/wiki/Euclidean_distance).<br><br>         * **Cosine similarity**: Measures similarity based on the angle between vectors, and can be used to measure similarity that is not affected by magnitude scaling. For more details, refer to [Cosine](https://en.wikipedia.org/wiki/Cosine_similarity).<br><br>      * **Quantization method**: Select a quantization method from the drop\-down list. Quantization is a technique that reduces the storage space and memory usage of vector search indexes by lowering the precision of vector data. For more details, refer to [Vector quantization](https://www.mongodb.com/docs/atlas/atlas-vector-search/vector-quantization/#vector-quantization).<br><br>   You can choose an appropriate quantization method based on your actual business needs for cost, performance, and precision:<br><br>         * **Binary**: This involves binarizing the numerical information of vectors (Binarization). If your business has high requirements for vector search speed and cost, you can choose the binary quantization method. For more details, refer to [Binary quantization](https://www.mongodb.com/docs/atlas/atlas-vector-search/vector-quantization/#binary-quantization).<br><br>         * **Scalar**: Independently quantizes each dimension (i.e., each value) of the vector. If your business requires high data precision, you can choose the scalar quantization method. For more details, refer to [Scalar quantization](https://www.mongodb.com/docs/atlas/atlas-vector-search/vector-quantization/#scalar-quantization).<br><br>         * **None**: Do not use any quantization methods to compress precision, it can ensure that the vector is completely distortion\-free.<br><br>         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div><br>         <br><br>         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Supports adding multiple vector fields concurrently, with a maximum of 20.         </div><br>         <br><br>   * Filter fields<br><br><br>Optional. Click **Add filter fields** to set the path for pre\-filter fields for the index.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip</div><br><br><br>* <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">For nested fields, use dot notation to specify the path of the embedded field. You only need to enter the field's key; no need to enter the field type. For example, name and info.age are valid values.</div><br><br><br>      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Supports adding multiple filter fields simultaneously, up to 20.      </div><br>      <br><br>* **JSON Editor**<br><br><br>You can configure the **field path**, **vector dimension**, **similarity calculation method**, **quantization method**, and **filtering field path** in the JSON editor. |



8. After making changes, click **OK**.
