---
title: "DropIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_DropIndex"
---

<span id="b4c7f100"></span>
# Overview

To remove a specific index from a collection, you can use the DropIndex operation. This document describes the DropIndex operation and provides a code example for its implementation.

<span id="ac369f00"></span>
# **request parameters**


|**parameter** |**type** |**Is it required?**  |**parameter description** |
|---|---|---|---|
|collectionName |String |Yes |The name of the collection that contains the index to be dropped.<br><br><br>* The name can only contain English letters, numbers, and underscores (_). It must begin with an English letter and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |
|indexName |String |Yes |Specify the name of the Index to delete.<br><br><br>* The name can only contain English letters, numbers, and underscores (_). It must begin with an English letter and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Index names cannot be repeated. |


<span id="1df99991"></span>
# Example

<span id="51937e68"></span>
## Request parameters

```Go
err := service.DropIndex("go", "goIndex")
if err != nil {
    fmt.Println(err)
}
```


<span id="604cea18"></span>
## Return value

On successful execution, the function returns no information.
