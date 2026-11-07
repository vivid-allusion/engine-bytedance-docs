---
title: "Deleting index"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/Deleting_index"
---

Document Database for MongoDB supports vector and full\-text indexes. When an index is no longer used by your application, you can delete it to free up storage space. This topic describes how to delete vector and full\-text indexes on the console.

<span id="CosvjBwv"></span>
## Prerequisite


* An instance of MongoDB 8.3 or later has been created. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/mongodb/creating_an_instance).

* The instance status is **Running**. For more details about instance status, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

* At least one vector or full\-text index has been created. For specific steps, refer to [Creating vector Index](https://docs.byteplus.com/en/docs/mongodb/create_vector_index) or [Creating full-text index](https://docs.byteplus.com/en/docs/mongodb/create-full-text-index?lang=en). To create a vector index using Auto Embedding, refer to [Creating auto-embedding vector index](https://docs.byteplus.com/en/docs/mongodb/create-auto-embedding-vector-index?lang=en).


<span id="NY1TRdkY"></span>
## Precautions


* Once an index is deleted, it cannot be recovered. Retrieval requests using this index will be affected, so proceed with caution.

* Deleting an index does not affect the original business data in the collection.

* Deleting an auto\-embedding index will not affect the configured API Key and vector model service. To remove an API Key, go to the **AI capabilities** \> **API Key management** page in the MongoDB console.


<span id="csXYDal7"></span>
## Procedure


1. Log on to the [MongoDB console](https://console.byteplus.com/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **AI capabilities** tab.

6. Perform the corresponding operation based on the index type to be deleted:

   * Delete vector index: Under the **Vector index** sub\-tab, locate the target index, and in the **Actions** column on the right, select **Delete**.

   * Delete full\-text index: Under the **Full\-text index** sub\-tab, locate the target index, and in the **Actions** column on the right, select **Delete**.

7. In the pop\-up dialog box, confirm the index to be deleted, and click **Delete**.
