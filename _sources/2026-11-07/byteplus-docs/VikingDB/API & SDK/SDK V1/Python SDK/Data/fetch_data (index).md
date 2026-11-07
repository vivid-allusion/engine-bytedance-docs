---
title: "fetch_data (index)"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_fetch_data__index"
---

<span id="e0eb4174"></span>
# Overview

Use the `fetch_data` method to query and retrieve one or more data records from a specified index based on their primary keys. This method supports querying up to 100 records at once and has an asynchronous equivalent, `async_fetch_data`. Note that there may be a data lag of up to 20 seconds after writing or deleting data before it is reflected in the index.

The asynchronous call uses the async_fetch_data interface, and the parameters remain unchanged.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Index data may take up to 20 seconds to update after collection data is written or deleted, so it might not be found immediately in the index.</div>


<span id="9a9499e1"></span>
# **request parameters**


|**parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|
|ID |String, int64,<br><br>List\ < int64 \>,<br><br>List\ < string \> |Yes |*  |A single primary key or a list of primary keys. |
|output_fields |List\ < string \> |No |*  |Filter scalar fields, specifying a list of scalar fields to return.<br><br><br>* If output_fields is not passed, the query returns all scalar fields.<br><br>* If output_fields is an empty list, the fields field is not returned.<br><br>* If there is an output_fields formatting error or the specified filter field is not in the collection, the interface returns an error. |
|Partition |String/int |No |"Default" |The name of the sub\-index, which must have a type consistent with the field_type of partition_by and a value corresponding to the field_value of partition_by.<br><br><br>* If the field_type is int64 or list, the partition input type is int64.<br><br>* If the field_type is string or list, the partition input type is a string that must match the format: "^[a\-zA\-Z0\-9. _ ]+$". |


<span id="5a63d071"></span>
# Complete example

<span id="deaf349d"></span>
## Request parameters

```Python
index = vikingdb_service.get_index("example", "example_index")
```


```Python
res = index.fetch_data(["11", "33"], partition="1", output_fields=["doc_id", "like"])


async def index_fetch_data():
    index = await vikingdb_service.async_get_index("async", "async")
    res = await index.async_fetch_data(["111", "222", "333", "444"])
asyncio.run(index_fetch_data())
```


<span id="50606c4f"></span>
## Request parameters

The Python call performs the above task and returns a Data instance or a list of Data instances. The properties contained in a Data instance are shown in the following table.


|**attribute** |**Description** |
|---|---|
|ID |The primary key. |
|Fields |The fields field in the response is a dictionary that contains the data for the specified fields. |
