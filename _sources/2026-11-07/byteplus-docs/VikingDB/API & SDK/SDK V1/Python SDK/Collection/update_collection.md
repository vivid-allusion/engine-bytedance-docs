---
title: "update_collection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_update_collection"
---

<span id="ac8fa4c7"></span>
# Overview

The `update_collection` API allows you to modify an existing Collection by adding new fields or changing its description.

This document provides the complete parameter list and code examples for both synchronous (`update_collection`) and asynchronous (`async_update_collection`) calls.

Note that this operation cannot be used to modify the properties of existing fields.

<span id="37ad79d4"></span>
# **request parameters**


|**parameter** |**sub\-parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|---|
|collection_name |*  |String |Yes |*  |Specifies the name of the collection to update. |
|Description |*  |String |No |" |Specifies the description of the Modified Collection.<br><br><br>* Length requirement: [0,65535]. |
|Fields<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">List of Field instances. The maximum number of Field instances in a Collection is 200.</div><br> |field_name |String |Yes |*  |Specifies the name of the custom field.<br><br><br>* The name must begin with an English letter, can only contain English letters, numbers, and underscores (_), and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Field names cannot be repeated. |
||field_type |String |Yes |*  |Specifies a custom field type, such as `FieldType.String`. For a list of optional values, see the "Optional values for field_type" section. |
||default_val |Consistent with field_type |No |*  |Specifies the default value of the custom field. For details, see the "Optional values for field_type" section.<br><br><br>* When `field_name` is a primary key, `default_val` has no effect and is not validated. |
||dim |Int |Required when field_type is a vector |*  |Specifies the dimension of the custom field vector.<br><br><br>* Value range: [4, 2048], and must be a multiple of 4.<br><br>* Vector dimension refers to the number of elements contained in a vector. |
||is_primary_key |Bool |Yes |False |Specifies whether the field is the primary key. The user can select a field of type int64/string from the field list defined by fields as the primary key field. Each collection has only one primary key. For all other fields, `is_primary_key` defaults to `False`.<br><br><br>* Enumeration values: True/False. |
||pipeline_name |String |Optional when field_type is text |*  |Text. The plain text preprocessing capability pipeline refers to the preprocessing process that the vector database automates text slicing, text vectorization, warehousing, and storage. Support writing to the original data source in string form.<br><br>pipeline_name enumeration values are as follows:<br><br><br>* text_split_bge_large_zh: The vector database uses a slicer to split long text into short text, and calls the embedding model to vectorize short text.<br><br>* text_bge_large_zh: The vector database does not split the text, and directly calls the embedding model to vectorize the text.<br><br>* text_split_bge_m3: The vector database uses the slicer to divide the long text into short text, calls the bge m3 model to extract the sparse features and dense features of the short text, and stores the dense vector field and sparse vector field preset by the system.<br><br>* text_bge_m3: The vector database does not divide the text, directly calls bge m3 to extract the sparse features and dense features of the short text, and stores the dense vector field and sparse vector field preset by the system.<br><br>* text_split_bge_large_and_m3: The vector database uses the slicer to divide the long text into short texts, calls the bge v1.5 model to extract the dense features of the short text and stores it in the dense vector field preset by the system; calls the bge m3 model to extract the sparse features of the short text and stores it in the sparse vector field preset by the system.<br><br>* The key `text_bge_m3` is listed twice with conflicting descriptions. Please verify the correct behavior and remove the incorrect entry. |


<span id="402266b1"></span>
## field_type optional value


|**field type** |**Available index types** |**default_val default** |**When data is written**<br><br>**value range** |**default_val**<br><br>**value range** |**Can be the primary key** |**explain** |
|---|---|---|---|---|---|---|
|Int 64 |Enumeration |0 |Int64 range |Int64 range |Yes |Integer |
|Float32 |Range |0.0 |Float32 range |Float32 range |No |Floating point number |
|String |Enumeration |"Default" |*  |Length < = 128 |Yes |String |
|Bool |Enumeration |False |True/false |True/false |No |Boolean type |
|List\ < string \> |Enumeration |["Default"] |List length < = 32 |List length < = 32 |No |String array |
|List\ < int64 \> |Enumeration |[0] |List length < = 32 |List length < = 32 |No |Integer array |
|Vector |Vector |*  |Dimension 4\-2048 |*  |No |Dense vector.<br><br><br>* The `dim` parameter is required when `field_type` is set to `vector`. |
|sparse_vector |Sparse vector |*  |Non\-zero subscript Unlimited<br><br>Non\-zero values are in the float32 range |*  |No |Sparse vector.<br><br><br>* sparse_vector cannot be set separately, it must be set in combination with the vector field.<br><br>* Receives a JSON object representing the keywords and their corresponding weights for the sparse vector.<br><br>> Example:<br><br>> sparse_vector = |
|Text |*  |*  |*  |*  |No |Text, note:<br><br><br>* The `pipeline_name` parameter is optional when `field_type` is set to `text`.<br><br>* When defining fields: If you add a `text` field with a `pipeline_name`, you cannot add a `vector` field, and only one such `text` field is allowed. If you add a `text` field without a `pipeline_name`, you can add `vector` fields and multiple `text` fields (up to 200). |


<span id="7c6edbdb"></span>
# Example

<span id="e5e9791e"></span>
## Request parameters

```Python
fields = [
    Field(
        field_name="like_new",
        field_type=FieldType.Float32,
        default_val=0
    ),
    Field(
        field_name="price_new",
        field_type=FieldType.String,
        default_val=""
    ),
]
vikingdb_service.update_collection("example",fields,description="change")

# Asynchronous call
async def update_collection():
        fields = [
            Field(
                field_name="like1",
                field_type=FieldType.Float32,
                default_val=0
            ),
            Field(
                field_name="price1",
                field_type=FieldType.String,
                default_val=""
            ),
        ]
        await vikingdb_service.async_update_collection("async1", fields)
asyncio.run(update_collection())
```


<span id="c4c1c03d"></span>
## Return value

This operation does not return a value.
