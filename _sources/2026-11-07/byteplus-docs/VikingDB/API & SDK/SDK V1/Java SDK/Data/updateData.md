---
title: "updateData"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_updateData"
---

<span id="4d8d6e6b"></span>
# Overview

updateData is used to update some fields of existing data. Updates to text, scalar, and vector fields are supported.

<span id="4dcdc02d"></span>
# **request parameters**


|**parameter name** |**sub\-parameter** |**type** |**Required?**  |**parameter description** |
|---|---|---|---|---|
|DataObject<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">DataObject instance or list of instances.</div><br> |Fields |Array\ < map \> |Yes |Specifies the data to be written.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The primary key field must be specified.</div><br><br><br><br>* The number of data objects in a single write operation cannot exceed 100.<br><br>* Each data object is a map where the key is the field name and the value is the field's value.<br><br>* The maximum total size of the data in the `Fields` map is 65,535 bytes. When the limit is exceeded, an error will be returned "fields data is too long, should be less than 65535".<br><br>* The format of field values for different field types is as follows:<br><br>   * Int 64: The format is an integer value.<br><br>   * Float: The format is a floating\-point value.<br><br>   * String: The value is a string.<br><br>   * Bool: The format is true/false.<br><br>   * List\ < string \>: The format is a string array.<br><br>   * List\ < int64 \>: The format is an integer array.<br><br>   * Vector: An array of floating\-point numbers.<br><br>   * sparse_vector: A JSON object where each key (k) is a string representing a keyword, and its corresponding value (v) is a float representing the keyword's weight.<br><br>   * Text: The format is a map of strings to strings. Currently, the map must contain a `text` key.<br><br>      * The value for the `text` key is the string content to be written, for example: `{"text": "hello world"}`.<br><br>   * Image: This field supports values in the TOS path format: tos://{bucket}/{object_key}. |
||TTL |Int |No |Data expiration time, in seconds.<br><br><br>* Format: A non\-negative integer.<br><br>* Default value: 0, which indicates that the data does not expire.<br><br>* When ttl is set to 86400, it means that the data will be automatically deleted after 1 day.<br><br>* Data deleted due to TTL expiration is not immediately removed from the index. |


<span id="3b9bba07"></span>
# Example

<span id="7562e459"></span>
## Request parameters

```Java
// Call getCollection once during the initialization of the program to get the specified collection. 
Collection collection = vikingDBService.getCollection("javaSDKTest");
```


```Java
// Update the author and aim fields with doc_id as the primary key. 
HashMap<String,Object> field1 = new HashMap<String,Object>(); 
List<String> author1 = new ArrayList<>(); 
author1.add("name1"); 
author1.add("name2"); 
field1.put("doc_id", "11"); 
field1.put("aim", true); 
field1.put("author", author1); 
DataObject dataObject1 = new DataObject() 
                        .setFields(field1) 
                        .build(); 
// Update the text_vector, text_sparse_vector, like, and price fields with doc_id as the primary key. 
HashMap<String,Object> field2 = new HashMap<String,Object>(); 
field2.put("doc_id", "22"); 
field2.put("text_vector", genRandomVector(12)); 
field2.put("text_sparse_vector", {"hi": 0.12, "there": 0.043, "!": 0.5}); 
field2.put("like", 2); 
field2.put("price", 1.11); 
DataObject dataObject2 = new DataObject() 
                        .setFields(field2) 
                        .build(); 
List<DataObject> dataObjects = new ArrayList<>(); 
dataObjects.add(dataObject1); 
dataObjects.add(dataObject2); 
collection.updateData(dataObjects);
```


<span id="f332f772"></span>
## Return value

If the call is successful, the method does not return any information.
