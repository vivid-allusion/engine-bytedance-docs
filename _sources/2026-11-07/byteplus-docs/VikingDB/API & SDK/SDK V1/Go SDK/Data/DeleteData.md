---
title: "DeleteData"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_DeleteData"
---

<span id="e2705138"></span>
# Overview

DeleteData is used to delete single or multiple data entries from a specified collection by primary key, with a limit of 100 entries at a time.

<span id="6fa4ed6e"></span>
# **Request parameters**


|**parameter** |**type** |**Required** |**Parameter description** |
|---|---|---|---|
|ID |String, int64,<br><br>List\ < int64 \>,<br><br>List\ < string \> |Yes |A single primary key or a list of primary keys. |


<span id="00df511a"></span>
# Example

<span id="b9522f5c"></span>
## Request parameters

```Go
// Call GetCollection once during program initialization to retrieve the specified collection. 
collection, _ := service.GetCollection("go")
```


```Go
err := collection.DeleteData([]string{"111", "222"})
if err != nil {
    fmt.Println(err.Error())
}
```


<span id="f32902e5"></span>
## Return value

Upon successful execution, the call does not return a value.
