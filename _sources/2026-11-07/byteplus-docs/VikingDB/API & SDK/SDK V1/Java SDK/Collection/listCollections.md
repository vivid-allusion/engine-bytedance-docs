---
title: "listCollections"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_listCollections"
---

<span id="d367aed4"></span>
# Overview

To get a list of all collections in your database, you can use the listCollections method. This API reference provides the Java SDK call signature and details the structure of the returned Collection objects, including their properties and statistics.

<span id="7a284858"></span>
# **request parameters**

None.

<span id="581c98ac"></span>
# Example

<span id="69ff5752"></span>
## Request parameters

```Java
List collections = vikingDBService.listCollections();
```


<span id="18945963"></span>
## Return value

The Java method call returns a list of Collection instances. The properties contained in a Collection instance are shown in the following table.


|**attribute** |**type** |**Description** |
|---|---|---|
|collectionName |String |The name of the collection |
|Description |String |The description of the collection |
|Fields |ArrayList < Field \> |A list of fields in the collection |
|Indexes |ArrayList < Index \> |A list of indexes in the collection |
|Stat |Map |Statistics/status information.<br><br><br>* data_number: The number of data items.<br><br>* data_storage: The storage size occupied by the data, in bytes |
|createTime |String |Collection creation time. |
|UpdateTime |String |Collection update time. |
|UpdatePerson |String |The user who last updated the collection. |
