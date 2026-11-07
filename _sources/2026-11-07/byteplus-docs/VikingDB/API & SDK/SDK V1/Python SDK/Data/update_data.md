---
title: "update_data"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_update_data"
---

<span id="3f21fc7b"></span>
# Overview

update_data is used to update some fields of existing data. Updates to text, scalar, and vector fields are supported.

<span id="780c82f5"></span>
# **request parameters**


|**parameter name** |**sub\-parameter** |**type** |**Is it required?**  |**parameter description** |
|---|---|---|---|---|
|Data<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Data instance or list of Data instances.</div><br> |Fields |Array\ < map \> |Yes |Specify the data to be written.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The primary key field value must be set.</div><br><br><br><br>* The number of data items written in a single request cannot exceed 100.<br><br>* Each data item is a map, where the key is the field name and the value is the field value.<br><br>* The total size of the data in the Fields map cannot exceed 65535 bytes. When the limit is exceeded, an error will be returned "fields data is too long, should be less than 65535".<br><br>* The format of field values for different field types is as follows:<br><br>   * Int 64: The format is an integer value.<br><br>   * Float: The format is a floating\-point value.<br><br>   * String: The format is a string.<br><br>   * Bool: The format is true/false.<br><br>   * List\ < string \>: The format is a string array.<br><br>   * List\ < int64 \>: The format is an integer array.<br><br>   * Vector: The format is a vector (array of floating\-point numbers).<br><br>   * The format is a JSON dictionary where the key (k) is a string representing the keyword literal, and the value (v) is a float representing the keyword's weight.<br><br>   * The format is a map of type `map<string, string>`. For example: `{"text": "hello world"}`.<br><br>      * Text: Write text as a string to the original data source, such as {"text": "hello world"}.<br><br>   * The value must be a string representing a TOS path.`tos://{bucket}/{object_key}` |
||TTL |Int |No |Data expiration time, in seconds.<br><br><br>* Format: 0 or a positive integer.<br><br>* Default value: Default is 0, indicating that the data does not expire.<br><br>* When ttl is set to 86400, it means that the data will be automatically deleted after 1 day.<br><br>* Data is deleted when its TTL expires, but this deletion is not immediately reflected in the index. |


<span id="f673af74"></span>
# Example

<span id="7217973f"></span>
## Request example

```Python
collection = vikingdb_service.get_collection("example")
```


```Python
field1 = {
    "doc_id": "11", 
    "author": ["name1", "name2"],
    "aim": True
}

field2 = {
    "doc_id": "22", 
    "text_vector": gen_random_vector(12),
    "text_sparse_vector": {"hi": 0.12, "there": 0.043, "!": 0.5},
    "like": 2,
    "price": 2.22,
}
data1 = Data(field1)
data2 = Data(field2)
datas = []
datas.append(data1)
datas.append(data2)
collection.update_data(datas) 
```


<span id="df448a83"></span>
## Return value

A successful call does not return a value.
