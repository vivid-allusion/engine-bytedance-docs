---
title: "getCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_getCollection"
---

<span id="4a77c3f8"></span>
# Overview

getCollection is used to query the details of a specified Collection.

<span id="7690bcf9"></span>
# **request parameters**


|**parameter** |**type** |**Is it required?**  |**parameter description** |
|---|---|---|---|
|collectionName |String |Yes |Specifies the Collection name for the query.<br><br><br>* Must contain only English letters, numbers, and underscores (_), begin with an English letter, and not be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names must be unique. |


<span id="94bee695"></span>
# Example

<span id="e00f9b90"></span>
## Request parameters

```Java
Collection collection = vikingDBService.getCollection("javaSDKTest");
```


<span id="b3988324"></span>
## Return value

The Java method call returns the specified Collection instance. The properties contained in the Collection instance are shown in the following table.


|**attribute** |**type** |**Description** |
|---|---|---|
|collectionName |String |The name of the queried Collection. |
|Description |String |The description of the queried Collection. |
|Fields |ArrayList < Field \> |A list of the Collection's fields. |
|Indexes |ArrayList < Index \> |A list of the Collection's indexes. |
|Stat |Map |Statistics/status information.<br><br><br>* data_number: The number of data entries.<br><br>* data_storage: The storage size occupied by the data, in bytes |
|createTime |String |The creation time of the Collection. |
|UpdateTime |String |The last update time of the Collection. |
|UpdatePerson |String |The user who last updated the Collection. |
