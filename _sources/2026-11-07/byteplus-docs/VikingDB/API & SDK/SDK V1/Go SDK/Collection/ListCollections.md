---
title: "ListCollections"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_ListCollections"
---

<span id="afff46af"></span>
# Overview

To retrieve a list of all available collections in your dataset, you can use the ListCollections function from the Go SDK. This reference provides a code example and details the structure of the returned collection objects, including their names, fields, indexes, and statistics.

<span id="0862618a"></span>
# **Request parameters**

None.

<span id="ce40a1d4"></span>
# Example

<span id="ddee5af7"></span>
## Request parameters

```Go
collections, err := service.ListCollections()
if err != nil {
    fmt.Println(err.Error())
}
for _, collection := range collections {
    fmt.Println(collection)
}
```


<span id="dfe9dd7a"></span>
## Return value

The Go call returns a slice of pointers to Collection structs. The Collection struct contains the following properties:


|**Property** |**type** |**Description** |
|---|---|---|
|CollectionName |String |The name of the collection. |
|Description |String |A description of the collection. |
|Fields |[] Field |A list of fields in the collection. |
|Indexes |[] interface {} |A list of indexes in the collection. |
|Stat |Map |Statistics/status information.<br><br><br>* data_number: The number of data records.<br><br>* data_storage: The storage size of the data, in bytes |
|CreateTime |String |Dataset creation time. |
|UpdateTime |String |Dataset update time. |
|UpdatePerson |String |The user who last updated the dataset. |
