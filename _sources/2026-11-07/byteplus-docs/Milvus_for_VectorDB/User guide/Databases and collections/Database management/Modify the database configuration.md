---
title: "Modify the database configuration"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Modify_the_database_configuration"
---

After creating the database, you can modify its configuration according to business needs. This topic describes how to modify configurations.

<span id="ZxjXxLls"></span>
## Prerequisites


* Created a Milvus for VectorDB instance and completed authorization. For specific steps, refer to [Create Instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance) and [Authorize instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Authorize_to_use_an_instance).

* Database created. For specific steps, refer to [Create a database](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_a_database).


<span id="SIdGHkaT"></span>
## Precautions

Only Dedicated instances support modifying the database.

<span id="lnHbW4p4"></span>
## Procedure


1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. In the top navigation bar, select the project and region for collections management.

3. Select **Collections** in the left navigation bar.

4. On the **Collections** page, choose the **Dedicated** tab, select the authorized instance, then click **View**.

5. On the **Collections** page, click the target database, select the **Property** tab, then click **Modify configuration**.

6. Set the running values for the following parameters according to business needs, then click **Submit**.

   
   |Parameter |Description |Value range |
   |---|---|---|
   |database.diskQuota.mb |The disk quota of the current database. Writing data to this database is not allowed after exceeding the quota. |0~2147483647, unit: MB |
   |database.force.deny.reading |Whether to forcibly deny all reading operations on the current database. |* true<br><br>* false |
   |database.force.deny.writing |Whether to forcibly reject all write operations, including insert, delete, import, etc. |* true<br><br>* false |
   |database.max.collections |The maximum number of Collections allowed to be created in the current database. |0~2147483647 |
   |database.replica.number |The number of replicas in the current database. |0~2147483647 |
   |database.resource_groups |The resource group list for the current database. |\- |
