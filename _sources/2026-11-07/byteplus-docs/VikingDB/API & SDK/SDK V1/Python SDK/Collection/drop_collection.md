---
title: "drop_collection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_drop_collection"
---

<span id="36be39d0"></span>
# Overview

To delete a Collection and all its data, you can use the drop_collection method.

This document describes both the synchronous drop_collection and the asynchronous async_drop_collection methods.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Deleting a collection will permanently delete all data under the specified collection. Please proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">Before deleting a Collection, all of its associated Indexes must be deleted. Please note that this operation is irreversible and will permanently delete all data.</div>



<span id="fbb42630"></span>
# **request parameters**


|**parameter** |**type** |**Is it required?**  |**parameter description** |
|---|---|---|---|
|collection_name |String |Yes |Specify the name of the Collection to delete.<br><br><br>* The name must begin with an English letter, use only English letters, numbers, and underscores (_), and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |


<span id="4a971262"></span>
# Example

<span id="0d5dec27"></span>
## Request parameters

```Python
vikingdb_service.drop_collection("example")

async def del_collection():
    await vikingdb_service.async_drop_collection("async")
asyncio.run(del_collection())
```


<span id="45e5dfdc"></span>
## Return value

This function call returns no value upon successful execution.
