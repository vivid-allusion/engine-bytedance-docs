---
title: "fetchData (index)"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_fetchData__index"
---

<span id="558e772d"></span>
# Overview

fetchData is used to query data in an index. It queries for one or more data entries in a specified index by primary key ID, and you can query for up to 100 entries at a time.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After collection data is written or deleted, there is an update lag of up to 20 seconds, during which the data may not be found in the index.</div>


<span id="c180f097"></span>
# **Response**


|**parameter** |**sub\-parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|---|
|ID |*  |String, int64,<br><br>List\ < int64 \>,<br><br>List\ < string \> |Yes |*  |A single primary key or a list of primary keys. |
|FetchDataParam |outputFields |List\ < string \> |No |*  |Specifies a list of scalar fields to return.<br><br><br>* If outputFields is not provided, the method returns all scalar fields.<br><br>* When outputFields is an empty list, the fields field is not returned.<br><br>* When outputFields is formatted incorrectly or the filter field is not a field in the collection, the interface returns an error. |
||Partition |String/int |No |"Default" |The name of the sub\-index. Its type must be consistent with the fieldType of partitionBy, and its value must correspond to the fieldValue of partition_by.<br><br><br>* If the fieldType is int64 or List, the partition input type is int64.<br><br>* If the fieldType is string or List, the partition input type is string and must match the format: ^[a\-zA\-Z0\-9._]+$.\*n |


<span id="7a26a8fa"></span>
# Complete example

<span id="1d9e28e0"></span>
## Request parameters

```Java
// Call getCollection once during the initialization of the program to get the specified collection. 
Collection collection = vikingDBService.getCollection("javaSDKTest");
```


```Java
List outputField = new ArrayList<>();
outputField.add("doc_id");
outputField.add("like");
outputField.add("text_vector");
ArrayList ids = new ArrayList<>();
ids.add("11");
ids.add("22");
ids.add("33");
ids.add("44");

List dataObject = index.fetchData(ids, new FetchDataParam().setOutputFields(outputField).build());
```


<span id="4e76e349"></span>
## Request parameters

The Java call performs the above task and returns a List. The properties contained in the DataObject instance are shown in the following table.


|**attribute** |**explain** |
|---|---|
|ID |The primary key. |
|Fields |The fields field in the response contains the specific data, which is a map. |
