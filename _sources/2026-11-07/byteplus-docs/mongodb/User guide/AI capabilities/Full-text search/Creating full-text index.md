---
title: "Creating full-text index"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/Create_full-text_index"
---

Document Database for MongoDB provides full\-text search capabilities, supporting text retrieval based on keywords. Full\-text indexes are fundamental for efficient full\-text retrieval, applicable to scenarios such as in\-site search, product search, and log queries. This topic describes how to create full\-text indexes in the console.

<span id="CaRi1giP"></span>
## Prerequisite


* An instance of MongoDB 8.3 or later has been created, and the search feature has been enabled. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/mongodb/creating_an_instance).

* The instance status is **Running**. For more details about instance status, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Currently, MongoDB 8.3 is in the invitation\-only testing phase. To use the full\-text search feature, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to contact technical staff and apply for access.</div>


<span id="eO8ft20U"></span>
## Procedure


1. Log on to the [MongoDB console](https://console.byteplus.com/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **AI capabilities** tab.

6. On the **Full\-text index** sub\-tab, click **Create index**.

7. On the **Create full\-text index** page, configure the following parameters.



|**Parameter** |**Required** |**Description** |
|---|---|---|
|Search type |Yes |This parameter is fixed as **Full\-text search**. No selection is required. |
|Index name |Yes |Set the index name. The name must meet the following conditions simultaneously:<br><br><br>* Must start with a lowercase English letter.<br><br>* Must end with a lowercase English letter or a number.<br><br>* Can only contain English letters, numbers, underscores (_), and hyphens (\-).<br><br>* The length must be between 3 and 128 characters. For more details, refer to [Constraints and limits](https://docs.byteplus.com/en/docs/mongodb/product-limit#.5Yqf6IO954m55oCn6ZmQ5Yi2).<br><br>* It cannot start with a number or hyphen (\-).<br><br>* Cannot contain spaces, Chinese characters, special characters, or consecutive special symbols.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Within the same instance, the index name must be unique.</div><br> |
|Database name |Yes |Select the database to which the index belongs from the dropdown list.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The database name and table name are both set during database creation. For specific steps, see <a href="https://docs.byteplus.com/en/docs/DBW/database-management-for-mongodb">Database management</a>.</div><br> |
|Collection name |Yes |Select the collection to which the index belongs from the dropdown list.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The database name and table name are both set during database creation. For specific steps, see <a href="https://docs.byteplus.com/en/docs/DBW/database-management-for-mongodb">Database management</a>.</div><br> |



8. After completing the above configuration, click **Next** in the bottom\-right corner to go to the index configuration page.

   1. In the **Configuration method** area, select **JSON editor**.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Full\-text search only supports the JSON editor. The visual editor is currently unavailable. You can use the embedded JSON editor to edit the original index definition.      </div>
      

   2. In the **JSON editor** input box, configure the index fields.

      The console has been pre\-filled with the following configuration, which, by setting mappings.dynamic: true, allows MongoDB to automatically index all fields in the table:

      ```JSON
      {
        "mappings": {
          "dynamic": true
        }
      }
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">When <code>mappings.dynamic</code> is set to <code>true</code>, MongoDB automatically indexes all indexable fields in the table, making any field available for full\-text search. If set to <code>false</code>, you need to explicitly declare the paths of the fields to be indexed in fields.      </div>
      

9. After the index configuration is complete, click **Next** to go to the confirmation page. Confirm the basic information and JSON preview information.

10. After confirmation, click **OK**.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Index creation is an asynchronous operation and takes some time to complete. It is recommended to search only after confirming the index status becomes READY. For more information on index status, see <a href="https://www.mongodb.com/zh-cn/docs/manual/reference/operator/aggregation/listsearchindexes/#mongodb-search-index-statuses">$listSearchIndexes (Aggregation Pipeline Stage)</a>.</div>
