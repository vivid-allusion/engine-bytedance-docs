---
title: "fetch_data (collection)"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_fetch_data_collection"
---

<span id="2fa7d0cf"></span>
# Overview

To retrieve specific data entries from a Collection, you can use the `fetch_data` function. This function allows you to query for one or more data records from a specified Collection by primary key, up to 100 records at a time. After data in the Collection is written or deleted, it can be queried in real time.

For asynchronous calls, use the async_fetch_data method. The parameters are the same as for the synchronous method.

<span id="c749cce4"></span>
# **Request parameters**


|**parameter** |**type** |**Required** |**default value** |**parameter description** |
|---|---|---|---|---|
|ID |String, int64,<br><br>List\ < int64 \>,<br><br>List\ < string \> |Yes |*  |A single primary key or a list of primary keys. |


<span id="26bc4288"></span>
# Complete example

<span id="dd2d7a17"></span>
## Request parameters

```Python
collection = vikingdb_service.get_collection("example")
```


```Python
res = collection.fetch_data("22")

async def fetch_data():
    collection = vikingdb_service.get_collection("async")
    res = await collection.async_fetch_data(["111", "222"])
asyncio.run(fetch_data())
```


<span id="a4c909e4"></span>
## Return value

The method returns a Data instance or a list of Data instances. The properties contained in a Data instance are shown in the following table.


|**attribute** |**Description** |
|---|---|
|ID |The primary key. |
|Fields |A dictionary containing the data fields. |
