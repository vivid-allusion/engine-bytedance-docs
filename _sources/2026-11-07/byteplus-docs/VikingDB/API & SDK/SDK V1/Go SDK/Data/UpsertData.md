---
title: "UpsertData"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_UpsertData"
---

<span id="015db2a1"></span>
# Overview

The UpsertData method inserts new data records or updates existing ones within a specified collection. You can use this method to write up to 100 data records in a single batch operation and optionally set a Time\-To\-Live (TTL) for each record.

<span id="7e3f482a"></span>
# **Request parameters**


|**Parameter Name** |**Sub\-parameter** |**type** |**Is It Required?**  |**Parameter Description** |
|---|---|---|---|---|
|Data<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Data structure or list of its components.</div><br> |Fields |Array\ < map \> |Yes |Specifies the data to be written.<br><br><br>* A single write operation can include a maximum of 100 data entries.<br><br>* Each data entry is a map where the key is the field name and the value is the field value.<br><br>* The maximum size of the data in the Fields map is 65535 bytes. When the limit is exceeded, an error will be returned "fields data is too long, should be less than 65535".<br><br>* The format of field values for different field types is as follows:<br><br>   * Int 64: The format is an integer value.<br><br>   * Float: The format is a floating\-point value.<br><br>   * String: The value is a string.<br><br>   * Bool: The format is true/false.<br><br>   * List\ < string \>: The format is a string array.<br><br>   * List\ < int64 \>: The format is an integer array.<br><br>   * Vector: The format is vector (array of floating\-point numbers).<br><br>   * sparse_vector: A JSON object where keys are string literals representing keywords, and values are float types representing the weight of each keyword.<br><br>   * Text: A map of type map<string, string\>. The key must be 'text'.<br><br>      * Text: Write text as a string to the original data source, such as {"text": "hello world"}.<br><br>   * Image: The value must be a TOS path. The format is`tos://{bucket}/{object_key}`. |
||TTL |Int |No |Data expiration time, in seconds.<br><br><br>* Format: 0 or a positive integer.<br><br>* Default value: 0, which indicates that the data does not expire.<br><br>* When TTL is set to 86400, the data is automatically deleted after 1 day.<br><br>* Data deleted due to an expired TTL is not immediately removed from the index. |


<span id="040f78c5"></span>
# Example

<span id="1a636b2f"></span>
## Request parameters

```Go
// Call GetCollection once during the initialization of the program to get the specified collection. 
collection, _ := service.GetCollection("go")
```


```Go
field1 := map[string]interface{}{
    "doc_id":      "111",
    "text_vector": genRandomVector(12),
    "text_sparse_vector":map[string]float64{"hello": 0.34, "world": 0.03, "!": 0.11}
    "like":        1,
    "price":       1.11,
    "author":      []string{"gy"},
    "aim":         true,
}
field2 := map[string]interface{}{
    "doc_id":      "222",
    "text_vector": genRandomVector(12),
    "text_sparse_vector": map[string]float64{"hello": 0.34, "world": 0.03, "!": 0.11}
    "like":        2,
    "price":       2.22,
    "author":      []string{"gy", "xjq"},
    "aim":         false,
}
field3 := map[string]interface{}{
    "doc_id":      "333",
    "text_vector": genRandomVector(12),
    "text_sparse_vector": map[string]float64{"hello": 0.34, "world": 0.03, "!": 0.11}
    "like":        3,
    "price":       3.33,
    "author":      []string{"gy"},
    "aim":         true,
}
field4 := map[string]interface{}{
    "doc_id":      "444",
    "text_vector": genRandomVector(12),
    "text_sparse_vector": map[string]float64{"hello": 0.34, "world": 0.03, "!": 0.11}
    "like":        4,
    "price":       4.44,
    "author":      []string{"gy"},
    "aim":         true,
}
data1 := vikingdb.Data{
    Fields: field1,
    TTL:    100000,
}
data2 := vikingdb.Data{
    Fields: field2,
    TTL:    200000,
}
data3 := vikingdb.Data{
    Fields: field3,
    TTL:    100000,
}
data4 := vikingdb.Data{
    Fields: field4,
}
datas := []vikingdb.Data{
    data1,
    data2,
    data3,
    data4,
}
err := collection.UpsertData(datas)
if err != nil {
    print(err.Error())
}
```


<span id="082bf611"></span>
## Return value

A successful Go call for this operation does not return any data.
