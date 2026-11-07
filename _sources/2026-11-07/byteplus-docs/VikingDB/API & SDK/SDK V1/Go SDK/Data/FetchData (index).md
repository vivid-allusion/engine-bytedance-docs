---
title: "FetchData (index)"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_FetchData__index"
---

<span id="e7511aa0"></span>
# Function introduction

FetchData is used for querying index data. It queries for single or multiple data records in the specified Index based on their primary key IDs. You can query up to 100 records at a time.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Index data updates can lag by up to 20 seconds after collection data is written or deleted, so the data may not be found immediately in the index.</div>


<span id="7dc6bc44"></span>
# **Response parameters**


|**parameter** |**sub\-parameter** |**type** |**Required** |**default value** |**parameter description** |
|---|---|---|---|---|---|
|ID |*  |String, int64,<br><br>List\ < int64 \>,<br><br>List\ < string \> |Yes |*  |A single primary key or a list of primary keys. |
|searchOptions |outputField |List\ < string \> |No |*  |Specifies a list of scalar fields to return.<br><br><br>* If outputField is not provided, the API returns all scalar fields.<br><br>* If outputField is an empty list, the `fields` map is not included in the response.<br><br>* The API returns an error if outputField is malformed or contains a field that does not exist in the collection. |
||Partition |String/int |No |"Default" |The name of the sub\-index. The type must be consistent with the `FieldType` of `partitionBy`, and the field value must correspond to the `FieldValue` of `partition_by`.<br><br><br>* When FieldType is int64 and list\ < int64 \>, the partition input type is int64.<br><br>* If `FieldType` is `string` or `list<string>`, the partition input type is `string`. The string must match the format `^[a-zA-Z0-9._]+$`. |


<span id="ca3a3a94"></span>
# Complete example

<span id="2da2b0b0"></span>
## Request parameters

```Go
// Call GetCollection once during the initialization of the program to get the specified collection. 
collection, _ := service.GetCollection("go")
```


```Python
searchOption := vikingdb.NewSearchOptions().SetOutputFields([]string{"doc_id", "like", "text_vector", "price"})
res, err := index.FetchData([]string{"111", "222"}, searchOption)
if err != nil {
    fmt.Println(err)
}
for _, item := range res {
    fmt.Println(item)
}
```


<span id="fd97965d"></span>
## Request parameters

The Go SDK call returns a slice of pointers to the `Data` structure (`[]*Data`). The properties contained in the `Data` structure are shown in the following table.


|**attribute** |**Description** |
|---|---|
|Id |The primary key. |
|Fields |A map that contains the returned scalar field data. |
