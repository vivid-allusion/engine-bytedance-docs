---
title: "delete_data"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_delete_data"
---

<span id="7bfacf46"></span>
# Overview

The `delete_data` method deletes one or more data entries from a specified Collection based on their primary keys. This method allows for the deletion of up to 100 entries in a single call.

For asynchronous operations, you can use the `async_delete_data` method, which accepts the same parameters.

<span id="7fa0438c"></span>
# **Request parameters**


|**Parameter** |**Type** |**Required** |**Parameter description** |
|---|---|---|---|
|ID |String, int64,<br><br>List\ < int64 \>,<br><br>List\ < string \> |Yes |A primary key or a list of primary keys. |


<span id="500d1dfd"></span>
# Example

<span id="72f3ac77"></span>
## Request parameters

```Python
collection = vikingdb_service.get_collection("example")
```


```Python
collection.delete_data("11")

async def del_data():
    collection = vikingdb_service.get_collection("async")
    res = await collection.async_delete_data("111")
asyncio.run(del_data())
```


<span id="87f6e327"></span>
## Return value

This method does not return a value upon successful execution.
