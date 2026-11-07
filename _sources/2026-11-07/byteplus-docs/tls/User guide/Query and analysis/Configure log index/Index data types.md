---
title: "Index data types"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Index-data-types-2"
---

When setting a key\-value index for log fields, you need to set a data type (text, long, double, or json) for each field with key\-value indexing enabled. The data type of a field's index determines how you can query the field and affects the precision and accuracy of query. This topic introduces configuration details and notes for each data type.

<span id=".5pWw5o2u57G75Z6L"></span>
## Data type

Log field values are typically text or numeric. You can set the index data type for a field as text (string), long (integer), or double (floating\-point) to meet different log query needs.

For more complex structured data such as json, you can set the index data type to json. TLS supports expanding standard and valid json fields. You can set the index data type for leaf nodes as text, long, or double to support queries of json leaf field values in nested structures.

The data types for index fields are described below:


|Type |Description |
|---|---|
|text |Suitable for fields of string type. |
|long |Suitable for fields of numeric type, such as integer (Int 64).<br><br>After setting the type to long, you can query log fields by value range using operators such as `>`. |
|double |Suitable for fields of numeric type, such as double (64 bit).<br><br>After setting the type to double, you can query log fields by value range using operators such as `>`. |
|json |Applies to fields of the JSON type.<br><br>Supports creating indexes for standard JSON fields, and allows setting the index data type for each expanded subfield. |


<span id=".dGV4dC3nsbvlnos="></span>
### Text type

Text type is suitable for fields with string values.


* The text type index supports fuzzy queries for this field using wildcards like `*` or `?`.

* After enabling the full\-text index, TLS sets the entire log (all fields except `__time__`) to the text type by default.


<span id=".bG9uZy3nsbvlnos="></span>
### Long type

Long type is suitable for numerical fields, such as integer (Int 64).


* Long type index supports querying log fields by numeric ranges using range operators like `>`.

* Long type index does not support settings for **Case sensitive**, **Contains Chinese**, or **Delimiter**, and does not support fuzzy query.

* If you set the index type for floating\-point or string fields to long, you cannot query those fields.


<span id=".ZG91YmxlLeexu-Weiw=="></span>
### Double type

The double type is suitable for numeric fields, such as 64\-bit floating point.


* Double type indexes support querying log fields by numeric range, for example, using range operators such as `>`.

* Double type indexes do not support **Case sensitive**, **Contains Chinese**, **Delimiter**, or fuzzy queries.

* If the index type of a string field is set to double, that field can not be queried.


<span id=".anNvbi3nsbvlnos="></span>
### json type

TLS supports creating indexes for standard json fields. Once a field is set to the json index data type, each expanded subfield supports individual index data type settings. After setting subfield indexes, query and analysis can be conducted at the subfield level.


* You can set index data types to text, long, or double based on the actual data type of the json subfield.

* If a subfield value is of Boolean type, set its index data type to text.


<span id="0bd85083"></span>
#### json **Subfield description**


* Naming rules

   * When setting the key\-value index for json subfields, use `.` to represent the hierarchical relationship between fields in the json data.

      For example, `key1.key2.key3` means that `key3` is a subfield of `key2`, and `key2` is a subfield of `key1`.

   * The subfield name can not include the name of the top\-level parent field.

   * Child field names can not be prefixed by a parent field with a conflicting data type.

      * You can not configure subfields `key1.key2` and `key1.key2.key3` at the same time.

      * You can configure subfields `key1.key2.key3` and `key1.key2.key4` at the same time.

* Automatic indexing

   When enabled, TLS will automatically create indexes for all fields with text values in json fields. **Automatic indexing** and **automatic index statistics** are mutually exclusive; you can select only one. For details, see [What is the difference between automatic JSON indexing and manual index configuration?](https://docs.byteplus.com/docs/tls/FAQ-about-the-query-and-analysis-of-JSON-logs#2b26c0e3).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1195c813438f4f6ca7b546ca492a1acb~tplv-goo7wpa0wc-image.image) </span>


|Subfield configuration |Description |
|---|---|
|Automatic indexing |* Takes effect within seconds.<br><br>* Supports subfield queries without updating the subfield list in the index configuration.<br><br>* If subfields are not configured, the parent field can be analyzed separately but can not be queried separately. |
|Automatic index statistics |* Takes effect within minutes.<br><br>* Supports querying and analyzing subfields; the subfield list in index configuration will be updated.<br><br>* Once enabled, independent querying and analysis for parent fields is not supported.<br><br>* To configure this, statistics for the parent field must be enabled first. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Notice</div>



* <div data-tips="true" data-tips-type="tip">Query and analysis differences exist between automatic JSON indexing and manual index configuration. For example, automatically created subfield indexes can not be used in SQL statements or <code>not key: *</code> statements.</div>


* <div data-tips="true" data-tips-type="tip">Automatic index creation is not supported for subfields of numeric or array type values.</div>



<span id="259d2efa"></span>
#### json **Subfield restriction settings**


* TLS does not support: indexing fields with JSON array values; indexing fields within a JSON array.

* Only the JSON field dimension supports **Case sensitive**, **Contains Chinese**, **Delimiter**, and **Enable statistics** key\-value index configuration. By default, subfields of text type inherit the key\-value index configuration of the json field and do not support separate settings.

* Supports up to 20 levels of JSON nesting. That is, TLS can parse at most 19 levels of data within a JSON subfield.


<span id="6df5aa07"></span>
#### json **Subfield exception scenario handling**


* For invalid JSON objects, TLS only parses the standard valid part.

* If TLS detects that the data types of the indexed JSON subfields do not match those of the actual log field values, the entire JSON log data can not be queried and analyzed. For example, if the actual field value is "zhangsan" and the field type is set to double, then none of the fields in the JSON object can be queried or analyzed.

* TLS supports indexing leaf nodes in JSON objects, but it is not recommended to index sub\-nodes that contain leaf nodes. If you index a nested JSON object within a JSON object, TLS will serialize the JSON value of the subfield as a string.

* For common issues encountered during query and analysis of JSON logs, see [FAQ about query and analysis of JSON logs](https://docs.byteplus.com/docs/tls/FAQ-about-the-query-and-analysis-of-JSON-logs).


<span id=".6YWN572u5qC35L6L"></span>
## Configuration example

For example, in application service log collection scenarios, each log represents a user request. The info field is formatted as a JSON object and provides details of a service request. Within the info field, the response and developers fields are also nested JSON objects.

Log sample:

```json
{
    "product":"NewApp",
    "total_users":1000000,
    "avg_pv_per_day":1000000.0,
    "regions":[
        "cn-beijing",
        "cn-shanghai"
    ],
    "info":{
        "api":"CreateIndex",
        "ip":[
            "192.168.1.101",
            "192.168.1.102"
        ],
        "request_time":1667232000,
        "latency_time":0.01,
        "response":{
            "request_id":"a**********",
            "status":200,
            "error_msg":""
        },
        "developers":[
            {
                "name":"zhangsan",
                "email":"zhangsan@test.com"
            },
            {
                "name":"lisi",
                "email":"lisi@test.com"
            }
        ]
    }
}
```


Index configuration:


* Set the index data type of the info field to JSON and specify the corresponding index data types for its subfields based on their actual data types. For instance, configure basic key\-value indexes for subfields like response.error_msg and response.status.

* The field value of regions, info.ip, and info.developers is array format. TLS does not support effective JSON key\-value indexing for these fields. You can use [JSON functions](https://docs.byteplus.com/docs/tls/JSON-functions) to parse the parent field of these fields and extract their contents for query and analysis.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e51bf971271c44e982be7a453db3d533~tplv-goo7wpa0wc-image.image) </span>


Sample query and analysis:


|Analysis scenarios |Query statements |
|---|---|
|Query logs containing NewApp |```SQL```<br>```NewApp```<br> |
|Query logs where total users exceed 10,000 and the average daily visits exceed 10,000.0. |```SQL```<br>```total_users: >10000 AND avg_pv_per_day: >10000.0```<br> |
|View all logs |```SQL```<br>```* \| SELECT * ```<br> |
|Filter logs by product name: NewApp |```SQL```<br>```* \| SELECT * WHERE product='NewApp' ```<br> |
|Filter logs where total users exceed 10,000 and the average daily visits exceed 10,000.0. |```SQL```<br>```* \| SELECT * WHERE total_users>10000 AND avg_pv_per_day>10000.0 ```<br> |
|Filter logs where the requested API is CreateIndex |```SQL```<br>```* \| SELECT * WHERE info.api='CreateIndex' ```<br> |
|Count logs with response status codes other than 200 |```SQL```<br>```* \| SELECT COUNT(*) WHERE info.response.status<>200 ```<br> |
|Count logs aggregated by requests to the NewApp API |```SQL```<br>```* \| SELECT info.api, COUNT(*) AS c WHERE product='NewApp' GROUP BY info.api ```<br> |
