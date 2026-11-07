---
title: "dropIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_dropIndex"
---

<span id="77c49b56"></span>
# Overview

The dropIndex method is used to delete a specified index from a collection.

<span id="9d7d172e"></span>
# **request parameters**


|**parameter** |**type** |**Is it required?**  |**parameter description** |
|---|---|---|---|
|collectionName |String |Yes |Specifies the name of the collection from which to drop the index.<br><br><br>* The name must contain only English letters, numbers, and underscores (_), begin with an English letter, and not be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |
|indexName |String |Yes |Specify the name of the index to delete.<br><br><br>* The name must contain only English letters, numbers, and underscores (_), begin with an English letter, and not be empty.<br><br>* Length requirements: [1,128].<br><br>* Index names cannot be repeated. |


<span id="8c112510"></span>
# Example

<span id="4a1d5722"></span>
## Request parameters

```Java
vikingDBService.dropIndex("javaSDKTest", "test_index");
```


<span id="e712d553"></span>
## Return value

A successful Java call to execute this task returns no information.
