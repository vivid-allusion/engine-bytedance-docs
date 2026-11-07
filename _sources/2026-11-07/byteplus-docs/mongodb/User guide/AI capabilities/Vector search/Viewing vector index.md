---
title: "Viewing vector index"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/Viewing_index"
---

This topic describes how to view the configuration details of existing vector indexes on the Document Database for MongoDB console.

<span id="xEIqjElO"></span>
## Prerequisite


* You have created a MongoDB 8.3 or later instance and enabled the search feature. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/mongodb/creating_an_instance).

* The instance status is **Running**. For more details about instance status, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

* At least one vector index has been created for the instance. For specific procedures, refer to[ Creating vector index](https://docs.byteplus.com/en/docs/mongodb/create_vector_index?lang=en).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Currently, MongoDB 8.3 is in the invitation\-only testing phase. To use the vector search feature, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to contact technical staff and apply for access.</div>



<span id="t6JSa8TC"></span>
## Procedure


1. Log on to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the name of the target instance to enter the instance details page.

5. Click the **AI capabilities** tab, then select the **Vector index** sub\-tab.

   On the list page, you can view the summary information of all vector indexes for the current instance, including the index name, database, collection, vectorization method, basic vector configuration, and status.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the list is empty, it indicates that no vector indexes of this type have been created for the current instance. Complete the index creation operation first.   </div>
   

6. In the index list, locate the target index and click **View** in the **Actions** column on the right side of that row.

7. In the pop\-up **Index details** panel, the system displays the complete creation configuration of the index in standard JSON format. This panel is for viewing only and does not support direct editing.
