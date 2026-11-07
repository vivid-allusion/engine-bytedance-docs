---
title: "Visual query management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Visual_query_management"
---

DBW provides visual query capabilities for the Document Database MongoDB. In the visual query console, you can query, copy, edit, and delete data.

<span id="4AZJwnmw"></span>
## Prerequisites


* A MongoDB instance has been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/mongodb/creating_an_instance).

* A database account has been created. For detailed steps, refer to [Creating an account](https://docs.byteplus.com/en/docs/mongodb/create-account).


<span id="vpnmMSEn"></span>
## Precautions


* The query results can display up to 3,000 rows, with a single\-row data limit of 3 MB and a result set limit of 10 MB.

* DBW cannot guarantee optimal performance for SQL executed in the data interaction console.  Therefore, it is not recommended to execute SQL tasks that are sensitive to response latency in the data interaction console.

* The creation, deletion, and other operations you perform may affect the online business operation. It is recommended to perform them during off\-peak hours.

* You can switch databases and collections as needed in the operable area of the data interaction console. A maximum of 100 databases or collections are supported.

* When adding collection records or specifying filter conditions, the field type representation must use the **Canonical Extended JSON (Strict EJSON)**  format. In the **Strict EJSON** format, the field type must be clearly defined, as follows:

   * **Non\-native JSON types**, such as **Date, ObjectId, Binary, Decimal 128, Timestamp, MinKey/MaxKey, and Regular Expression**, must use the **Strict EJSON** specification format. For example, `_id` uses`{"$oid":"507f1f77bcf86cd799439011"}`。

   * **Numerical value** should follow the **Strict EJSON** specification format, such as `\"$numberInt\"`, `\"$numberLong\"`, and `\"$numberDouble\"`, to eliminate ambiguities between 32\-bit integers, 64\-bit integers, and double\-precision numbers. If you do not use the **Strict EJSON** specification format, the MongoDB driver automatically converts the value type. The conversion result is not guaranteed to fully meet expectations.

   For more information about the **Strict EJSON** field type representation, see [Type Representations](https://www.mongodb.com/zh-cn/docs/manual/reference/mongodb-extended-json/#type-representations).


<span id="FLhHE28F"></span>
## Procedure

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can open the visual query window from the <strong>Query collection</strong> option in the right\-click menu of a collection.</div>



1. Log on to the [data interaction console of Document Database MongoDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-documentdb-for-mongodb).

2. On the **data interaction  console** page, click the icon after the target collection in the command execution area, or right\-click the collection name area.

3. In the shortcut menu, select **Query collection**.

4. In the visual query window, you can query, copy, edit, and delete collection data.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1add97482042a9db6740cf4113fc926e.png) </span>

   
   |**No.**  |**Region** |**Description** |
   |---|---|---|
   |1 |Collection catalog tree |In the collection directory tree area, you can visually manage collections and indexes.<br><br><br>* Collection<br><br>   You can create, query, rename, and delete collections. For more information, see [Collection management](https://docs.byteplus.com/en/docs/DBW/collection-management-for-mongodb).<br><br>* Index<br><br>   You can create index, query index, and delete index. For more information, see [Index management](https://docs.byteplus.com/en/docs/DBW/index-management-for-mongodb). |
   |2 |Query area |In the `Query` area, Filter supports using {field:"value"} format and functions as query conditions to query collection data.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When using the <code>{field:"value"}</code> format as a <code>Filter</code> condition, the <code>Field</code> <code>Type</code> representation must <code>Use</code> the <strong>Canonical Extended JSON (Strict EJSON)</strong> format. In the <strong>Strict EJSON</strong> format, the <code>Field</code> <code>Type</code> must be clearly defined, as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="warning"><strong>Non\-native JSON types</strong> such as <strong>Date, ObjectId, Binary, Decimal 128, Timestamp, MinKey/MaxKey, and regular expressions</strong> must use the <strong>Strict EJSON </strong> specification format. For example, use <code>_id</code><code>{"$oid":"507f1f77bcf86cd799439011"}</code>。</div><br><br><br>   * <div data-tips="true" data-tips-type="warning"><strong>Numerical value</strong> should follow the <strong>Strict EJSON</strong> specification format, such as <code>\"$numberInt\"</code>, <code>\"$numberLong\"</code>, and <code>\"$numberDouble\"</code>, to eliminate ambiguities between 32\-bit integers, 64\-bit integers, and double\-precision numbers. If you do not use the <strong>Strict EJSON</strong> specification format, the MongoDB driver automatically converts the value type. The conversion result is not guaranteed to fully meet expectations.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can use functions such as ObjectId, ISODate, Date, Timestamp, Code, NumberDecimal, NumberLong, Double, NumberInt, BinData, MinKey, MaxKey, BSONRegExp, and RegExp as query criteria. See the <a href="https://docs.byteplus.com/en/docs/DBW/Visual_query_management#8XkfP6Vi">function definition</a> for the above <a href="https://docs.byteplus.com/en/docs/DBW/Visual_query_management#8XkfP6Vi">function definition</a>.</div><br><br><br><br>When manually entering query criteria, the command auto\-completion function is supported. Copying `field:"value"` formatted data from collection records as query criteria is also supported. To copy `field:"value"` formatted data in the collection records, you must first select the `field:"value"` formatted data, and then press the copy shortcut key.<br><br>The following are query examples<br><br><br>* The following commands query collection records with a CPU utilization of 0.4 in visual query and shell regular session windows.<br><br>   * In the visual query window, the query condition is`{"cpu.usage":0.4}`。<br><br>   * In a regular shell session, the query command is `db.collection.find({\"cpu.usage\":0.4})`.<br><br>* The following commands perform an exact search for collection records where the `create_at` field is `2025-09-12T10:40:00.000Z`. These commands can be used in the visual query interface and in a standard shell session.<br><br>   * In the visual query window, the query condition is`{"created_at":{"$date":{"$numberLong":"1757673600000"}}}`。<br><br>   * In a regular shell session, the query command is: `db.collection.find({created_at: ISODate("2025-09-12T10:40:00.000Z")})`.<br><br>* Query the collection records where `_id` is `507f1f77bcf86cd799439011`, the region is `cn-beijing`, and the CPU utilization is between 0.20 and 0.80. The following commands are available in the visual query and regular shell session windows.<br><br>   * In the visual query window, the query criteria are as follows.<br><br>      ```JSON```<br>```      {```<br>```          "_id": {```<br>```              "$oid": "507f1f77bcf86cd799439011"```<br>```          },```<br>```          "region": "cn-beijing",```<br>```          "cpu.usage": {```<br>```              "$gte": 0.2,```<br>```              "$lte": 0.8```<br>```          }```<br>```      }```<br>```      ```<br>      <br><br>   * In a regular shell session, the query command is as follows.<br><br>      ```Bash```<br>```      db.collection.find({  _id: ObjectId("507f1f77bcf86cd799439011"),  region: "cn-beijing",  "cpu.usage": { $gte: 0.20, $lte: 0.80 }})```<br>```      ```<br>      <br><br>   Click **More Options** to perform more granular filtering. The filtering criteria include Project, Sort, Max Time (ms), Collation, Skip, and Limit.<br><br>   * Project: Supports **Relax** **Extended JSON (relaxed EJSON)**  format, such as`{"name":1, "region":1, "cpu.usage":1, "_id":0}`。 For more information, see [$projection](https://www.mongodb.com/zh-cn/docs/manual/reference/operator/projection/positional/).<br><br>   * Sort: **Relax Extended JSON (relaxed EJSON)**  format is supported , ** ** such as`{ "region": 1, "cpu.usage": -1}`。 For more information, see [$sort](https://www.mongodb.com/zh-cn/docs/manual/reference/operator/aggregation/sort/).<br><br>   * Skip: For example, 10 indicates skipping 10 collection records.<br><br>   * Limit: For example, 5 indicates selecting only 5 collection records.<br><br>   * Collation: **Relax Extended JSON (Relaxed EJSON) **  format is supported , ** ** which is case\-insensitive. For more syntax information, see [Collation](https://www.mongodb.com/docs/manual/reference/collation/).<br><br>   There are two display formats for query results: JSON and List. You can switch the data display format in the upper right corner of the area. |
   |3 |Visual operation area |In the visual operation area, you can visually add, copy, edit, and delete collection data.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">There are two display formats for collection data: JSON and List. You can switch the data display format in the upper right corner of the area. The following example uses JSON format to describe how to visually add, copy, edit, and delete collection data.</div><br><br><br><br>* Add collection records<br><br>   Click **Add Record**. In the Add Record window, enter the data to be added and click **OK** to add a record to the current collection.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When adding collection records, you must use the <strong>Canonical Extended JSON (Strict EJSON)</strong> format to ensure that the format of the added data strictly complies with the MongoDB standard. In the <strong>Strict EJSON</strong> format, you must specify the field type, such as:   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The date is<code>{ "created_at": { "$date": { "$numberLong": "1757673600000" } } }</code>。 If the date is written as<code>{"created_at": "2025-09-12T08:00:00Z"}</code>It will be treated as a string in the <strong>Strict EJSON</strong> format instead of a date type.   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">ObjectId is<code>{ "_id": { "$oid": "507f1f77bcf86cd799439011" } }</code>。   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For more information about <strong>Strict EJSON</strong> field type representations, see <a href="https://www.mongodb.com/zh-cn/docs/manual/reference/mongodb-extended-json/#type-representations">Type Representation</a>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Adding multiple collection records at once is supported in the format <code>[{},{},{},……]</code>. All records are within <code>[]</code>, and each record is separated by a comma (,).   </div><br>   <br><br>   * The following is a complete example of adding a collection record.<br><br>      ```JSON```<br>```      {```<br>```          "_id": {```<br>```              "$oid": "507f1f77bcf86cd79943****"```<br>```          },```<br>```          "name": "mongo-instance",```<br>```          "type": "MongoDB",```<br>```          "region": "cn-beijing",```<br>```          "cpu": {```<br>```              "cores": {```<br>```                  "$numberInt": "2"```<br>```              },```<br>```              "usage": {```<br>```                  "$numberDouble": "0.40"```<br>```              }```<br>```          },```<br>```          "tags": [```<br>```              "shard",```<br>```              "router"```<br>```          ],```<br>```          "created_at": {```<br>```              "$date": {```<br>```                  "$numberLong": "1757673600000"```<br>```              }```<br>```          }```<br>```      }```<br>```      ```<br>      <br><br>      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f94e64e4ce19d1de7a007b22b1199677.png) </span><br><br>* Copy Collection Data<br><br>   Click the copy icon to copy the entire record or a value.<br><br>   * Copy the entire record: Click the copy icon in the upper right corner of the record to copy the entire record.<br><br>   * Copy a value: Hover the mouse over the target data. After the copy icon appears, click the copy icon to copy the target data value.<br><br>   * Copy `field:"value"` data: Select the `field:"value"` data, and then press the copy shortcut key, or the **Copy** option in the right\-click menu.<br><br>         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2135bce86ae7891ef71c623d93771fb1.png) </span><br><br>* Edit Collection Data<br><br>   Click the edit icon in the upper right corner of the record. After entering edit mode, you can copy, modify, and delete collection data in BSON or EJSON presentation forms. After the modification is completed, click **Submit** to save the modified information.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When editing collection data, you are not allowed to modify the field value of <code>_id</code>. In EJSON mode, modifications to the <code>_id</code> field value will not be saved.   </div><br>   <br><br>   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_95932dffc9bbe6af92da3eeb211a3b61.png) </span><br><br>* Delete collection data<br><br>   Click the delete icon in the upper right corner of the record, and after a second confirmation, you can delete the entire collection data. In the edit mode of collection data, click the delete icon after a field and field value to delete the field and field value.<br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Collections cannot be recovered once deleted. And deleting collections may degrade database performance because the database needs to process more files. Exercise caution when performing this operation.   </div><br>    |
   


<span id="8XkfP6Vi"></span>
## Appendix

In Mongo visual query, functions such as ObjectId, ISODate, Date, Timestamp, Code, NumberDecimal, NumberLong, Double, NumberInt, BinData, MinKey, MaxKey, BSONRegExp, and RegExp are supported as filter conditions. The definitions of these functions are as follows.

```TypeScript
/**
 *@param {string} id Must be a 24 byte hex string.
 */
declare function ObjectId(id: string): {
 $oid: string;
};

/**
 *@param {string} date An ISO-8601 date string
 */
declare function ISODate(date?: string): {
 $date: {
 $numberLong: string;
 };
};

/**
 *@param {number|string}date
 */
declare function Date(date?: number | string): {
 $date: {
 $numberLong: string;
 };
};

/**
 *@param {string} A high-precision decimal as string.
 */
declare function NumberDecimal(num: string | number): {
 $numberDecimal: string;
};

/**
 *@param {string} num A long number string
 */
declare function NumberLong(num: string | number): {
 $numberLong: string;
};

/**
 *@param {string} num A double number string
 */
declare function Double(num: string | number): {
 $numberDouble: string;
};

/**
 *@param {string} num A int number string
 */
declare function NumberInt(num: string): {
 $numberInt: string;
};

/**
 *@param {number} t A positive integer for the seconds since epoch.
 *@param {number} i A positive integer for the increment.
 */
declare function Timestamp(
 t: number,
 i: number,
): {
 $timestamp: {
 t: number;
 i: number;
 };
};

/**
 *@param {number} subType BSON binary subtype. See the extended bson documentation http://bsonspec.org/spec.html for subtypes available.
 *@param {string} base64 Base64 encoded (with padding as “=”) payload string.
 */
declare function BinData(
 subType: number,
 base64: string,
): {
 $binary: {
 base64: string;
 subType: string;
 };
};

/**
 *
 * The MinKey BSON data type compares lower than all other types.
 */
declare function MinKey(): { $minKey: 1 };

/**
 * The MaxKey BSON data type compares higher than all other types.
 */
declare function MaxKey(): { $maxKey: 1 };

declare function BSONRegExp(
 pattern: string,
 options?: string,
): {
 $regularExpression: {
 pattern: string;
 options: string;
 };
};

declare function RegExp(
 pattern: string,
 options?: string,
): {
 $regularExpression: {
 pattern: string;
 options: string;
 };
};

const SubType = {
 Generic: 0x0,
 Function: 0x1,
 Binary_old: 0x2,
 UUID_old: 0x3,
 UUID: 0x4,
 MD5: 0x5,
 Encrypted: 0x6,
 UserDefined: 0x80,
};
```
