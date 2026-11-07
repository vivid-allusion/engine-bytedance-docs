---
title: "drop_index"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_drop_index"
---

<span id="97f4a48a"></span>
# Overview

To delete a specific index from a collection, you can use the drop_index method. This document provides the syntax, parameters, and Python code examples for both the synchronous drop_index method and its asynchronous counterpart, async_drop_index.

The asynchronous call uses the async_drop_index interface, and the parameters remain unchanged.

<span id="afba07ce"></span>
# **request parameters**


|**parameter** |**type** |**Is it required?**  |**parameter description** |
|---|---|---|---|
|collection_name |String |Yes |Specifies the name of the collection that contains the index to be dropped.<br><br><br>* The name must only contain English letters, numbers, and underscores (_), must begin with an English letter, and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |
|index_name |String |Yes |Specify the name of the Index to delete.<br><br><br>* The name must only contain English letters, numbers, and underscores (_), must begin with an English letter, and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Index names cannot be repeated. |


<span id="1f5043d5"></span>
# Example

<span id="5114771f"></span>
## Request parameters

```Python
vikingdb_service.drop_index("example", "example_index")

# Asynchronous call
async def del_index():
    await vikingdb_service.async_drop_index("async", "async")
asyncio.run(del_index())
```


<span id="8f033f4b"></span>
## Return value

Upon successful execution, the call returns no information.
