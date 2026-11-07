---
title: "list_collections"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_list_collections"
---

<span id="7eae63c8"></span>
# Overview

Use the `list_collections` method to query and retrieve a list of all collections within a dataset.

This document provides details for both the synchronous `list_collections` and asynchronous `async_list_collections` interfaces, which share the same parameters.

<span id="0321949a"></span>
# **request parameters**

None.

<span id="acc90967"></span>
# Example

<span id="ac3ce6a6"></span>
## Request parameters

```Python
res = vikingdb_service.list_collections()

async def list_collections():
    res = await vikingdb_service.async_list_collections()
asyncio.run(list_collections())
```


<span id="c09eeaf1"></span>
## Return value

The Python call performs the above task and returns a list of Collection instances. The properties contained in a Collection instance are shown in the following table.


|**attribute** |**type** |**Description** |
|---|---|---|
|collection_name |String |Collection name. |
|Description |String |Collection description. |
|Fields |List < Field \> |List of fields. |
|Indexes |List < Index \> |List of indexes. |
|Stat |Map |Statistics/status information.<br><br><br>* data_number: Number of data entries.<br><br>* data_storage: Data storage size, in bytes. |
|create_time |String |Collection creation time. |
|update_time |String |Collection update time. |
|update_person |String |Collection updater. |
