---
title: "Creating vector index"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/create_vector_index"
---

Document Database for MongoDB provides vector search capabilities, supporting data retrieval based on semantic similarity. Vector indexes are fundamental for efficient vector retrieval and are suitable for scenarios such as RAG knowledge bases, intelligent Q&A, and similarity recommendations. This topic describes how to enable the index feature and create vector indexes in the console.

## Prerequisite

* An instance of MongoDB 8.3 or later has been created. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/mongodb/creating_an_instance).

* The instance status is **Running**. For more details about instance status, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

> **tip**

> Currently, MongoDB 8.3 is in the invitation\-only testing phase. To use the vector search feature, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical staff and apply for access.

## Background information

MongoDB offers the following two index types, which you can choose based on your business scenarios.

* Vector index

   Retrieves data based on semantic similarity, suitable for AI application scenarios such as RAG knowledge bases, intelligent Q&A, and similar recommendations, enabling integrated storage and retrieval of document and vector data.

* Full\-text index

   Retrieves data based on keyword matching, suitable for document search scenarios such as site search, product retrieval, and log querying, and supports features like fuzzy matching, relevance ranking, and auto\-completion.

## Procedure

### Enable AI capabilities

> **tip**

* > Before creating a vector index, confirm whether the instance has AI capabilities enabled (i.e., whether Mongot nodes have been deployed). You can view this on the instance details page in the **AI capabilities** tab.

   * > **Enabled**: The page displays vector index and full\-text index tabs. You can create a vector index directly without performing the operations in this section. Select a creation method based on the vectorization approach:

      * > Manual: Use your self\-generated vector data. See [Creating vector index](https://docs.byteplus.com/en/docs/mongodb/create_vector_index?lang=en#Kz23Rr0f).

      * > Auto: The system calls the Ark Embedding model to generate vectors. See [Creating auto\-embedding vector index](https://docs.byteplus.com/en/docs/mongodb/Creating_auto-embedding_vector_index?lang=en).

   * > **Disabled**: The page prompts, "This instance currently has no Mongot nodes. **Configure Mongot** to use AI capabilities such as vector index and full\-text index." First, click **Configure Mongot**, then create an index afterwards. This operation only needs to be performed once.

* > AI capabilities take effect immediately after being enabled and cannot be disabled.

1. Log on to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **AI Capabilities** tab.

6. On the **AI capabilities** tab, click **Configure Mongot**.

7. On the **Mongot node configuration** page, configure the following parameters.

|**Parameter** ||**Description** |
|---|---|---|
|Basic information |Instance type |The instance type is automatically recognized by the system, so no selection is required. For more details about instance types, refer to [Product architecture](https://docs.byteplus.com/en/docs/mongodb/about-mongodb#.5Lqn5ZOB5p625p6E). |
|Instance configuration<br><br> ||If the **instance type** is a **replica set**, the following parameters must be configured:<br><br>**Mongot Node**<br><br><br>* **Node specifications**: Select the specifications of the Mongot nodes in the replica set instance. For more details, refer to [Compute node specifications](https://docs.byteplus.com/en/docs/mongodb/product-specification?lang=en#FiurFYyE).<br><br>* **Number of nodes:**  Currently fixed at 2 and cannot be changed.<br><br>* **Storage space:**  Select the storage space for the Mongot node. Unit: GiB, in increments of 10. It is recommended to maintain consistency with the initial configuration of Mongod nodes.<br><br><br>> **tip**<br><br><br><br>* > Mongot nodes are only displayed after **AI capabilities** are enabled.<br><br><br>* > Mongot nodes are deployed using a two\-node high\-availability architecture. The system automatically performs failover, routing traffic to healthy nodes. Ensure that your services have a retry mechanism.<br><br><br>* > To ensure data integrity during storage adjustment or backup and recovery scenarios, and considering the minimum storage differences offered by various specifications, ensure that the storage space entered for this configuration change or recovery is not less than 20 GiB.<br><br><br>* > Under the conditions mentioned above, purchase matching specifications and storage space, in increments of 10 GiB. For the specification and storage range mapping table, refer to [Product specifications](https://docs.byteplus.com/en/docs/mongodb/product-specification).<br><br><br><br>If the **instance type** is a **sharding cluster**, the following parameters need to be configured:<br><br><br>* **Mongot Node**<br><br>   * **Node specifications:**  Select the node specifications for Mongot in the sharding cluster. For more details, refer to [Compute node specifications](https://docs.byteplus.com/en/docs/mongodb/product-specification?lang=en#FiurFYyE).<br><br>   * **Number of nodes in a single shard**: currently fixed at 2.<br><br>   * **Storage space**: Select the storage space for Mongot nodes. Unit: GiB, in increments of 10.<br><br><br>> **tip**<br><br><br>> Mongot nodes are only displayed after **AI capabilities** are enabled.<br> |

8. After the parameters are configured, click **Enable now** in the lower\-right corner. After enablement, you can use AI capabilities such as vector index and full\-text index.

   > **tip**

   * > After clicking **Enable now**, the instance will enter the **Changing configuration** state. This process may take several minutes; wait patiently.

   * > In this state, no other operations are supported on the instance (e.g., viewing instance details, or managing accounts or backups).

### Create vector index

1. Log on to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **AI Capabilities** tab.

6. Under the **Vector index** tab, click **Create index**.

7. On the **Create vector index** page, configure the following parameters.

|**Parameter** ||**Required** |**Description** |
|---|---|---|---|
|Index configuration<br><br> |Search type |Yes |This parameter is fixed as **Vector search**, and you do not need to select it. |
||Embedding method |Yes |Select **Manual** to use vectors already generated or planned to be generated by your own models or APIs.<br><br>> **tip**<br><br><br>> To create a vector index with an **Auto** embedding method, refer to [Creating auto\-embedding vector index](https://docs.byteplus.com/en/docs/mongodb/Creating_auto-embedding_vector_index?lang=en).<br> |
|Index name and data source<br><br> |Index name<br><br> |Yes<br><br> |Set the index name. The name must meet the following conditions simultaneously:<br><br><br>* Must start with a lowercase English letter.<br><br>* Must end with a lowercase English letter or a number.<br><br>* Can only contain English letters, numbers, underscores (_), and hyphens (\-).<br><br>* The length must be between 3 and 128 characters. For more details, refer to [Constraints and limits](https://docs.byteplus.com/en/docs/mongodb/product-limit#.5Yqf6IO954m55oCn6ZmQ5Yi2).<br><br>* It cannot start with a number or hyphen (\-).<br><br>* Cannot contain spaces, Chinese characters, special characters, or consecutive special symbols.<br><br><br>> **warning**<br><br><br>> Within the same instance, the index name must be unique.<br> |
||Database name |Yes |Select the database to which the index belongs from the dropdown list.<br><br>> **tip**<br><br><br>> Both the database name and collection name are set when creating the database. For specific steps, see [Database management](https://docs.byteplus.com/en/docs/DBW/database-management-for-mongodb).<br> |
||Collection name |Yes |Select the collection to which the index belongs from the dropdown list.<br><br>> **tip**<br><br><br>> Both the database name and collection name are set when creating the database. For specific steps, see [Database management](https://docs.byteplus.com/en/docs/DBW/database-management-for-mongodb).<br> |

8. After completing the above configuration, click ** Next** in the bottom\-right corner to go to the index configuration page.

|**Parameter** ||**Required** |**Description** |
|---|---|---|---|
|Configuration |Configuration method |Yes |You can choose the **Visual editor** and **JSON editor** for configuration.<br><br><br>* **Visual editor**<br><br>   * Vector field<br><br><br>Required. Click **Add vector field,**  to configure the following parameters:<br><br><br>      * **Field path**: Set the field path, which specifies the field on which the index needs to be built. For more details, refer to [path](https://www.mongodb.com/docs/atlas/atlas-vector-search/vector-search-type/#:~:text=filter%20Type.-,fields.,path,-String).<br><br>      * **Vector dimensions**: Set the number of vector dimensions enforced by MongoDB vector search during indexing and querying. Value range: 1~8192. For more details, refer to [numDimensions](https://www.mongodb.com/docs/atlas/atlas-vector-search/vector-search-type/#mongodb-vector-search-index-fields:~:text=to%20embedded%20fields.-,fields.,numDimensions,-Int).<br><br>      * **Similarity calculation method**: Select a similarity algorithm from the drop\-down list. The value range is as follows:<br><br>         * **Dot Product (default)** : Measures similarity based on the angle and magnitude between vectors. For more details, refer to [Dot product](https://en.wikipedia.org/wiki/Dot_product).<br><br>         * **Euclidean distance**: Measures the distance between vector endpoints and can be used to measure similarity from different dimensions. For more details, refer to [Euclidean](https://en.wikipedia.org/wiki/Euclidean_distance).<br><br>         * **Cosine similarity**: Measures similarity based on the angle between vectors, and can be used to measure similarity that is not affected by magnitude scaling. For more details, refer to [Cosine](https://en.wikipedia.org/wiki/Cosine_similarity).<br><br>      * **Quantization method**: Select a quantization method from the drop\-down list. Quantization is a technique that reduces the storage space and memory usage of vector search indexes by lowering the precision of vector data. For more details, refer to [Vector quantization](https://www.mongodb.com/docs/atlas/atlas-vector-search/vector-quantization/#vector-quantization).<br><br>   You can choose an appropriate quantization method based on your actual business needs for cost, performance, and precision:<br><br>         * **Binary**: This involves binarizing the numerical information of vectors (Binarization). If your business has high requirements for vector search speed and cost, you can choose the binary quantization method. For more details, refer to [Binary quantization](https://www.mongodb.com/docs/atlas/atlas-vector-search/vector-quantization/#binary-quantization).<br><br>         * **Scalar**: Independently quantizes each dimension (i.e., each value) of the vector. If your business requires high data precision, you can choose the scalar quantization method. For more details, refer to [Scalar quantization](https://www.mongodb.com/docs/atlas/atlas-vector-search/vector-quantization/#scalar-quantization).<br><br>         * **None**: Do not use any quantization methods to compress precision, it can ensure that the vector is completely distortion\-free.<br><br>         > **tip**<br>         <br><br>         > Supports adding multiple vector fields concurrently, with a maximum of 20.<br>         <br><br>   * Filter fields<br><br><br>Optional. Click **Add filter fields** to set the path for pre\-filter fields for the index.<br><br>> **tip**<br><br><br>* > For nested fields, use dot notation to specify the path of the embedded field. You only need to enter the field's key; no need to enter the field type. For example, name and info.age are valid values.<br><br><br>      * > Supports adding multiple filter fields simultaneously, up to 20.<br>      <br><br>* **JSON Editor**<br><br><br>You can configure **field paths**, **vector dimensions**, **similarity calculation methods**, **quantization methods**, and **quantization method paths** in the JSON editor. |

9. After the index configuration is complete, click **Next** to confirm the creation information.

   * Visual Editor, confirm your configured vector fields, filter fields, and JSON preview information.

   * JSON Editor, confirm your edited JSON preview information.

10. After confirming, click **OK** in the lower\-right corner to complete index creation.

11. After creation, view the newly created index in the index list. A status of **Running** indicates successful creation.

> **tip**

> Index creation is an **asynchronous operation** and takes some time to complete. It is recommended to search only after confirming the index status becomes **`READY`**. For more information about the index status, see [$listSearchIndexes (Aggregation Stages)](https://www.mongodb.com/zh-cn/docs/manual/reference/operator/aggregation/listsearchindexes/#mongodb-search-index-statuses).

## Relevant APIs

|**API** |**Description** |
|---|---|
|[CreateDBInstance](https://docs.byteplus.com/en/docs/mongodb/createdbinstance) |Call the CreateDBInstance API to create a MongoDB instance. |
|[DescribeNodeSpecs](https://docs.byteplus.com/en/docs/mongodb/describenodespecs) |Call the DescribeNodeSpecs API to query the list of node specifications supported by MongoDB. |
|[DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) |Call the DescribeDBInstances API to query the basic information of the MongoDB instance. |
|[DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/mongodb/describedbinstancedetail) |Call the DescribeDBInstanceDetail API to query the detailed information of the target MongoDB instance. |
