---
title: "GetCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_GetCollection"
---

<span id="64e109b6"></span>
# Overview

GetCollection is used to query the details of a specified collection.

<span id="41f65830"></span>
# **request parameters**


|**parameter** |**type** |**Required** |**parameter description** |
|---|---|---|---|
|collectionName |String |Yes |Specifies the Collection name for the query.<br><br><br>* The name can contain only English letters, numbers, and underscores (_). It must begin with an English letter and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |


<span id="438fd595"></span>
# Example

<span id="57d02880"></span>
## Request parameters

```Go
collection, err := service.GetCollection("go")
if err != nil {
    print(err.Error())
}
```


<span id="f4b12917"></span>
## Return value

This operation returns a pointer to a Collection struct (\*Collection). The properties contained in the Collection structure are shown in the following table.


|**Property** |**type** |**Description** |
|---|---|---|
|CollectionName |String |The name of the collection. |
|Description |String |The description of the collection. |
|Fields |[] Field |A list of fields in the collection. |
|Indexes |[] interface {} |A list of indexes for the collection. |
|Stat |Map |Statistics/status information.<br><br><br>* data_number: The number of data entries.<br><br>* data_storage: The data storage size, in bytes. |
|CreateTime |String |The creation time of the collection. |
|UpdateTime |String |The update time of the collection. |
|UpdatePerson |String |The user who last updated the collection. |
