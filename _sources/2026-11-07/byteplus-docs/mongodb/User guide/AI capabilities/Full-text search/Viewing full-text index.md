---
title: "Viewing full-text index"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/Viewing_full-text_index"
---

This topic describes how to view the configuration details of existing full\-text indexes on the Document Database for MongoDB console.

<span id="hSEutNVf"></span>
## Prerequisite


* You have created a MongoDB 8.3 or later instance and enabled the search feature. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/mongodb/creating_an_instance).

* The instance status is **Running**. For more details about instance status, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

* At least one full\-text index has been created for the instance. For specific steps, see [Creating full-text index](https://docs.byteplus.com/en/docs/mongodb/create-full-text-index?lang=en).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Currently, MongoDB 8.3 is in the invitation\-only testing phase. To use the full\-text search feature, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to contact technical staff.</div>


<span id="OfauhTgy"></span>
## Procedure


1. Log on to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the name of the target instance to enter the instance details page.

5. Click the **AI capabilities** tab, and then select the **Full\-text index** sub\-tab.

   On the list page, you can view an overview of all full\-text indexes for the current instance, including the index name, database name, table name, index definition, and status.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the list is empty, it indicates that no full\-text indexes have been created for the current instance. Complete the index creation operation first.   </div>
   

6. In the index list, locate the target index and click **View** in the **Actions** column on the right.

7. In the pop\-up **Index details** panel, the system displays the complete creation configuration of the index in standard JSON format. This panel is for viewing only and does not support direct editing.
