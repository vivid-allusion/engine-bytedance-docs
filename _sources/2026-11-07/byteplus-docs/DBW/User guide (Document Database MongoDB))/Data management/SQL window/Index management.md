---
title: "Index management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/index-management-for-mongodb"
---

This topic describes how to visually create, and delete indexes in the command execution window of the Database Workshop (DBW) console to achieve full lifecycle management of indexes.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance for Document Database for MongoDB has been created and its `root` account password has been set. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/mongodb/creating_an_instance).

* A collection has been created. For operations, refer to [Creating a collection](https://docs.byteplus.com/en/docs/DBW/collection-management-for-mongodb).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Deleting or modifying collections in the system database is not supported.

* Deleting the default index `_id_` in the `collection` is not supported.

* Creating or deleting an index consumes certain CPU resources. To reduce the impact of creating or deleting an index on your instance, we suggest taking the following measures:

   * Create or delete indexes during off\-peak hours.

   * Enable the Background option to create indexes in the background, avoiding operation blocking caused by index creation.

* When creating or deleting indexes, the index change operations are executed serially, that is, the creation, modification, or deletion of the previous index must be completed on all nodes before proceeding to the next index creation or deletion operation.


<span id=".5Yib5bu657Si5byV"></span>
## Create an index

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is not recommended to create an index in the system database.</div>



1. Log on to the [data interaction platform for Document Database for MongoDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-documentdb-for-mongodb).

2. On the top menu bar of the **Data interaction platform** page, click the icon after Database and select the target database.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span>icon after the database, select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Collection**, right\-click the index, and select **Create index**.

4. On the **Create index@Database** tab, configure the index parameters.

   
   |**Parameter** ||**Description** |
   |---|---|---|
   |**Index information** |**Database** |Displays the database name of the current index without requiring configuration. |
   ||**Owning collection** |Displays the collection name of the current index without requiring configuration. |
   ||**Index name** |Custom index name. The naming rules are as follows:<br><br><br>* The length must be within 64 characters, and can not be empty.<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-). |
   ||**Key** |* Create key<br><br>   Click **Create**. In the Key name column, **set the name of the key. In the ** **Sort ** column, set the order of the keys. The current sort supports the `asc`, `desc`, and `hashed` options.<br><br>* Delete key<br><br>   Check the target key and click **Delete**. |
   |**Advanced configuration** |**Background** |Check whether to use Background to avoid blocking other operations during index creation. Checked by default. |
   ||**Unique** |Check the Unique option to create a unique index. If duplicate records exist, they will be rejected. |
   ||**Sparse** |Check whether to enable Sparse. If the field data does not exist, the index is not enabled. After selection, documents that do not include the index field can not be queried. |
   ||**TTL** |Check whether to enable the TTL index mode. TTL can be used to automatically delete expired documents, helping you manage and clean up time\-sensitive data, ensuring that the data in the database remains current and relevant.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A TTL index can only be created on a single field containing date values, and this field must be of a timestamp type, such as Timestamp. If it is a non\-date field, the TTL index will not take effect. It is recommended to use the ascending order to ensure that the earliest documents are deleted. For more information on TTL, refer to <a href="https://www.mongodb.com/zh-cn/docs/v6.0/core/index-ttl/">Official documentation for MongoDB</a>.</div><br> |
   ||**ExpireAfterSeconds** |Set automatic deletion of data in the collection after a specified time to save storage space and improve query performance. The value range is [0, 2147483647], in second(s).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You must configure this parameter when TTL is selected.</div><br> |
   

5. Click **Submit**.

6. In the **Execute** **SQL** dialog box, confirm the SQL statement for creating the index.

7. Click **Execute**.


<span id=".5p-l6K-i57Si5byV"></span>
## Query an index


1. Log on to the [data interaction platform for Document Database for MongoDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-documentdb-for-mongodb).

2. On the top menu bar of the **Data interaction platform** page, click the icon after Database and select the target database.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span>icon after the database, select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Index**, right\-click the target index, and select **Query index**.

4. On the **Session** tab, click **Execute**.


In the **Execution result** area, you can view the detailed index information.

<span id=".5Yig6Zmk57Si5byV"></span>
## Delete an index

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The default index <code>_id_</code> can not be deleted.</div>


* <div data-tips="true" data-tips-type="warning">Deleting the index of the system database is not allowed.</div>


1. Log on to the [data interaction platform for Document Database for MongoDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-documentdb-for-mongodb).

2. On the top menu bar of the **Data interaction platform** page, click the icon after Database and select the target database.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span>icon after the database, select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Index**, right\-click the target index, and select **Delete index**.

4. In the **Execute** **SQL** dialog box, confirm deletion of the SQL statement for the index.

5. Click **Execute**.


<span id="0nDaj7Vm"></span>
## Edit the TTL value of an index

When creating an index, you can edit the TTL value of the index if the TTL feature is enabled.


1. [Log on to the data interaction platform for Document Database for MongoDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-documentdb-for-mongodb).

2. On the top menu bar of the **Data interaction platform** page, click theicon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand **Collection **  and **Index**, click the icon after the target index, or right\-click the target index, and **Select** **Edit index TTL value**.

4. On the **Edit index TTL@Database** tab, click Edit after the **ExpireAfterSeconds** **Parameter** to **Modify** the **ExpireAfterSeconds** **Parameter value**. The value range is [0, 2147483647], in second(s).

5. Click the ✅ icon to submit the modified data.

6. In the **Execute SQL** dialog box, confirm the SQL statement to be executed.

7. After confirming that the information is correct, click **Execute**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands) |Call the DataExecCommands interfaceAPI to execute an SQL command. |
|[DataSessionKeepAlive](https://docs.byteplus.com/en/docs/DBW/datasessionkeepalive) |Call the DataSessionKeepAlive API to keep an SQL session alive. |
|[DataCloseSession](https://docs.byteplus.com/en/docs/DBW/dataclosesession) |Call the DataCloseSession API to close an SQL session. |
|[DataCancelExec](https://docs.byteplus.com/en/docs/DBW/datacancelexec) |Call the DataCancelExec API to cancel SQL execution. |
