---
title: "Clone Collection schemas and data"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Clone_a_Collection_schema_and_data"
---

When you want to reuse an existing collection's schema and data, you can clone collections, schemas, and data to create a new collection with the same schema and retain the data. The cloning scope includes schema, index information, and data. This topic describes how to clone Collection schemas, and data.

<span id="ByLMziEZ"></span>
## Prerequisites


* Created a Milvus for VectorDB instance and completed authorization. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance) and [Authorize to use an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Authorize_to_use_an_instance).

* Collection has been created. For detailed steps, see [Create a collection](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_a_collection).


<span id="IXJSU3se"></span>
## Precautions

Only Dedicated and Serverless instances support cloning collection schema and data.

<span id="5zztZiZ7"></span>
## Procedure


1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. In the top navigation bar, select the project and region for collections management.

3. Select **Collections** in the left navigation bar.

4. On the **Collections** page, select the **Dedicated** or **Serverless** tab, choose the Completed authorized Instance, then click **View**.

5. On the **Collections** page, expand the database containing the target Collection, then click  **... \> Clone collection schema and data** on the right of the target Collection.

6. In the pop\-up dialog, configure the following parameters, then click **OK**.

   
   |Parameter |Description |
   |---|---|
   |Current database |Displays the current database name and cannot be modified. |
   |Target instance type |Same as the source instance type. |
   |Target instance |Select the target instance to clone Collections, Schemas, and Data from the dropdown list. |
   |Authorize to use an instance |Enter the username and password for the target instance. This parameter is hidden if the target instance authorization is completed. |
   |Target database |Select the target database to clone Collections, Schemas, and Data from the dropdown list. |
   |Table mapping |Select the source Collection from the source table dropdown list and enter the target Collection name in the target table to map the Collection from the source database to the target database. You can click **Add map** to map multiple Collections. |
   


<span id="HmNGtHhX"></span>
## Subsequent operations

After cloning the Collection schema and database, you can view the progress and details of the clone task on the database details page. For detailed operation, see [View a database](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/View_a_database).
