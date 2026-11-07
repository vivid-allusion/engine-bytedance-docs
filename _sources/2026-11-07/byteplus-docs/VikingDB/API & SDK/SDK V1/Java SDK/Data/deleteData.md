---
title: "deleteData"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_deleteData"
---

<span id="ade2f151"></span>
# Overview

The deleteData method deletes one or more data items from a specified Collection by primary key, allowing up to 100 items to be deleted at a time.

<span id="e9476eaf"></span>
# **request parameters**


|**parameter** |**type** |**Required** |**parameter description** |
|---|---|---|---|
|ID |String, int64,<br><br>List\ < int64 \>,<br><br>List\ < string \> |Yes |A single primary key or a list of primary keys. |


<span id="12159c22"></span>
# Example

<span id="7d58210b"></span>
## Request parameters

```Java
// Call getCollection once during program initialization to get the specified Collection object. 
Collection collection = vikingDBService.getCollection("javaSDKTest");
```


```Java
List ids = new ArrayList<>();
ids.add("11");
ids.add("22");
collection.deleteData(ids);
```


<span id="0d7dacd0"></span>
## Return value

A successful call returns no information.
