---
title: "UpdateData"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_UpdateData"
---

<span id="d7241640"></span>
# Overview

UpdateData is used to update some fields of existing data. Updates to text, scalar, and vector fields are supported.

<span id="571f57e8"></span>
# **request parameters**


|**parameter name** |**sub\-parameter** |**type** |**Is it required?**  |**parameter description** |
|---|---|---|---|---|
|Data<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Data structure or list of its components.</div><br> |Fields |Array\ < map \> |Yes |Specifies the data to be written.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The primary key field value must be set.</div><br><br><br><br>* A single write request can include a maximum of 100 records.<br><br>* Each data record is a map where keys are field names and values are the corresponding field values.<br><br>* The maximum length of fields when data is written is 65535. When the limit is exceeded, an error will be returned "fields data is too long, should be less than 65535".<br><br>* The format of field values for different field types is as follows:<br><br>   * Int 64: The format is an integer value.<br><br>   * Float: The format is a floating\-point value.<br><br>   * String: The format is a string.<br><br>   * Bool: The format is true/false.<br><br>   * List\ < string \>: The format is a string array.<br><br>   * List\ < int64 \>: The format is an integer array.<br><br>   * Vector: The format is an array of floating\-point numbers.<br><br>   * sparse_vector: The format is a JSON object where the key (k) is a string that represents the keyword literal, and the value (v) is a float that represents the keyword's weight.<br><br>   * Text: The format is a map that must contain a `text` key with a string value.<br><br>      * Text: Write text as a string to the original data source, such as {"text": "hello world"}.<br><br>   * The value must be a TOS path. The format is tos://{bucket}/{object_key}. |
||TTL |Int |No |Data expiration time, in seconds.<br><br><br>* Format: 0 or a positive integer.<br><br>* Default: 0, which indicates that the data does not expire.<br><br>* When ttl is set to 86400, it means that the data will be automatically deleted after 1 day.<br><br>* Expired data is deleted, but this change is not immediately reflected in the index. |


<span id="297e0398"></span>
# Example

<span id="34d751d0"></span>
## Request parameters

```Go
// Call GetCollection once during the initialization of the program to get the specified collection. 
collection, _ := service.GetCollection("go")
```


```Go
// Update the author and aim fields with doc_id as the primary key. 
field1 := map[string]interface{}{ 
     "doc_id": "11", 
     "author": []string{"name1", "name2"}, 
     "aim": true, 
} 
// Update the text_vector, text_sparse_vector, like, and price fields with doc_id as the primary key. 
field2 := map[string]interface{}{ 
     "doc_id": "22", 
     "text_vector": genRandomVector(12), 
     "text_sparse_vector": map[string]float64{"hello": 0.34, "world": 0.03, "!": 0.11}, 
     "like": 2, 
     "price": 2.22, 
} 
var data1 vikingdb.Data 
var data2 vikingdb.Data 
data1.Fields = field1 
data2.Fields = field2 
datas := []vikingdb.Data{ 
     data1, 
     data2, 
} 
err := collection.UpdateData(datas) 
if err != nil { 
     print(err.Error()) 
}
```


<span id="1aaa1337"></span>
## Return value

If the operation is successful, the method does not return any information.
