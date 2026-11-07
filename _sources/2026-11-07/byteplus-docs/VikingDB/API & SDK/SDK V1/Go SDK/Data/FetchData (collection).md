---
title: "FetchData (collection)"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_FetchData__collection"
---

<span id="951f8044"></span>
# Overview

This method allows you to query one or more items from a specified Collection by primary key. You can query up to 100 items at a time.

After data is written to or deleted from a collection, it can be queried in real time.

<span id="11d1e148"></span>
# **Request parameters**


|**parameter** |**type** |**Is it required?**  |**default value** |**Parameter description** |
|---|---|---|---|---|
|ID |String, int64,<br><br>List\ < int64 \>,<br><br>List\ < string \> |Yes |*  |A single primary key or a list of primary keys. |


<span id="ac1342d0"></span>
# Complete example

<span id="cd0b638a"></span>
## Request parameters

```Go
// Call GetCollection once during the initialization of the program to get the specified collection. 
collection, _ := service.GetCollection("go")
```


```Go
res, err := collection.FetchData([]string{"111", "222", "333", "444"})
if err != nil {
    fmt.Println(err)
}
for _, item := range res {
    fmt.Println(item)
}
```


<span id="8bf14bfc"></span>
## Return value

The Go call performs the above task and returns a slice of pointers to Data structs ([]\*Data). The properties contained in the Data struct are shown in the following table.


|**Attribute** |**Description** |
|---|---|
|Id |The primary key of the record. |
|Fields |The Fields attribute contains the record's data as a map. |
