---
title: "updateCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_updateCollection"
---

<span id="e9389c15"></span>
# Overview

The UpdateCollection API allows you to modify the schema of an existing Collection. You can use it to add new fields or update the Collection's description, but it does not support modifying existing field definitions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Collection supports the addition of new field fields. The defined field fields do not support modification, but only support modifying the dataset description.</div>


<span id="ffe255d8"></span>
# **request parameters**


|**parameter** |**sub\-parameter** |**type** |**Required** |**default value** |**parameter description** |
|---|---|---|---|---|---|
|collectionName |*  |String |Yes |*  |Specifies the updated Collection name.<br><br><br>* Must start with an English letter and can only contain English letters, numbers, and underscores (_). Cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |
|Description |*  |String |No |" |Update the description of the Collection.<br><br><br>* Length requirement: [0,65535]. |
|Fields<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">List of Field instances. The maximum number of Field instances in a Collection is 200.</div><br> |FieldName |String |Yes |*  |Specify the name of the custom field.<br><br><br>* Must start with an English letter and can only contain English letters, numbers, and underscores (_). Cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Field names cannot be repeated. |
||fieldType |String |Yes |*  |The custom field type. For optional values, see the **fieldType optional value** section. |
||defaultVal |Consistent with fieldType |No |*  |Specify the default value of the custom field, see the default value for details **fieldType optional value**Explanation.<br><br><br>* When fieldName is the primary key, defaultVal does not take effect and is not validated. |
||dim |Int |Required when fieldType is vector |*  |The dimension of the custom field vector.<br><br><br>* Value range: [4, 2048], and must be a multiple of 4.<br><br>* Vector dimension refers to the number of elements contained in a vector. |
||isPrimaryKey |Bool |Yes |False |Specify whether the field is the primary key. The user can select a field of type int64/string from the field list defined by fields as the primary key field. Each Collection has one and only one primary key, and for the other fields, `isPrimaryKey` defaults to `False`.<br><br><br>* Enumeration values: True/False. |
||pipelineName |String |Optional when fieldType is text |*  |Text. The plain text preprocessing capability pipeline refers to the preprocessing process that the vector database automates text slicing, text vectorization, warehousing, and storage. Supports writing to the original data source in string form.<br><br>pipeline_name enumeration values are as follows:<br><br><br>* text_split_bge_large_zh: The vector database uses a slicer to split long text into short text, and calls the embedding model to vectorize short text.<br><br>* text_bge_large_zh: The vector database does not split the text, and directly calls the embedding model to vectorize the text.<br><br>* text_split_bge_m3: The vector database uses the slicer to divide the long text into short text, calls the bge m3 model to extract the sparse features and dense features of the short text, and stores the dense vector field and sparse vector field preset by the system.<br><br>* text_bge_m3: The vector database does not divide the text, directly calls bge m3 to extract the sparse features and dense features of the short text, and stores the dense vector field and sparse vector field preset by the system.<br><br>* text_split_bge_large_and_m3: The vector database uses the slicer to divide the long text into short texts, calls the bge v1.5 model to extract the dense features of the short text and stores it in the dense vector field preset by the system; calls the bge m3 model to extract the sparse features of the short text and stores it in the sparse vector field preset by the system.<br><br>* (This entry has a duplicate key 'text_bge_m3' and its description appears to be incorrect. Please verify and correct the key and content.) |


<span id="b9eba279"></span>
## field_type optional value


|**field type** |**Available index types** |**Default value** |**When data is written**<br><br>**value range** |**defaultVal**<br><br>**value range** |**Can be the primary key** |**explain** |
|---|---|---|---|---|---|---|
|Int 64 |Enumeration |0 |Int64 range |Int64 range |Yes |Integer |
|Float32 |Range |0.0 |Float32 range |Float32 range |No |Floating\-point number |
|String |Enumeration |"Default" |*  |Length < = 128 |Yes |String |
|Bool |Enumeration |False |True/false |True/false |No |Boolean type |
|List |Enumeration |["Default"] |List length < = 32 |List length < = 32 |No |String array |
|List |Enumeration |[0] |List length < = 32 |List length < = 32 |No |Integer array |
|Vector |Vector |*  |Dimension 4\-2048 |*  |No |Dense vector.<br><br><br>* Required parameter dim when fieldType is set to vector. |
|sparse_vector |Sparse vector |*  |Non\-zero subscript Unlimited<br><br>Non\-zero values are in the float32 range |*  |No |Sparse vector.<br><br><br>* sparse_vector cannot be set separately, it must be set in combination with the vector field.<br><br>* Accepts a JSON object where each key\-value pair represents a keyword and its corresponding weight in the sparse vector.<br><br>> Example:<br><br>> sparse_vector = |
|Text |*  |*  |*  |*  |No |Text, note:<br><br><br>* Optional parameter pipelineName when fieldType is set to text.<br><br>* When you define a `text` field and specify a `pipelineName`, you cannot add a separate `vector` field, and you can only add one such `text` field. When you define a `text` field without a `pipelineName`, you can add `vector` fields and multiple `text` fields (up to 200). |


<span id="ef8830dc"></span>
# Example

<span id="01144d3d"></span>
## Request parameters

```Python
 List fields = new ArrayList<>();
        fields.add(new Field().setFieldName("new_field1").setFieldType(FieldType.Int64).setDefaultVal(10).build());
        fields.add(new Field().setFieldName("new_field2").setFieldType(FieldType.String).setDefaultVal("test").build());
        UpdateCollectionParam updateCollectionParam = new UpdateCollectionParam().setCollectionName("javaSDKTest1")
                                                                                .setFields(fields)
                                                                                .setDescription("modify")
                                                                                .build();
        vikingDBService.updateCollection(updateCollectionParam);
```


<span id="6797809b"></span>
## Return value

This operation does not return a value.
