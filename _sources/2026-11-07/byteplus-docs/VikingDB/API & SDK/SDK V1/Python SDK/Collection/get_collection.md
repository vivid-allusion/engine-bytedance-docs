---
title: "get_collection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_get_collection"
---

<span id="3622a92e"></span>
# Overview

To retrieve the complete details of a specific collection, including its schema, indexes, and statistics, you can use the `get_collection` method. This document provides the syntax, parameters, and return value specifications for both the synchronous (`get_collection`) and asynchronous (`async_get_collection`) methods, along with Python code examples.

The asynchronous call uses the async_get_collection interface, and the parameters remain unchanged.

<span id="e49dd0f6"></span>
# **request parameters**


|**parameter** |**type** |**Required** |**parameter description** |
|---|---|---|---|
|collection_name |String |Yes |Specifies the Collection name for the query.<br><br><br>* The name must contain only English letters, numbers, and underscores (_), and must begin with an English letter.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |


<span id="93e4358e"></span>
# Example

<span id="ff158ea4"></span>
## Request parameters

```Python
res = vikingdb_service.get_collection("example")

async def get_collection():
    res = await vikingdb_service.async_get_collection("async")
asyncio.run(get_collection())
```


<span id="4ed2c400"></span>
## Return value

This function returns a Collection instance. The returned Collection instance has the following properties:


|**attribute** |**type** |**Description** |
|---|---|---|
|collection_name |String |Collection name. |
|Description |String |Collection description. |
|Fields |List < Field \> |List of fields. |
|Indexes |List < Index \> |Index list. |
|Stat |Map |Statistics/status information.<br><br><br>* data_number: number of data items.<br><br>* data_storage: The storage size occupied by the data, in bytes. |
|create_time |String |Collection creation time. |
|update_time |String |Collection update time. |
|update_person |String |The user who last updated the collection. |
