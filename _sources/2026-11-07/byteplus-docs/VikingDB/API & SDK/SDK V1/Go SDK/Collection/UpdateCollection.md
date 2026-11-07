---
title: "UpdateCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_UpdateCollection"
---

<span id="ebc22599"></span>
# Overview

UpdateCollection is used to add fields to a specified collection.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A collection supports the addition of new fields. Defined fields cannot be modified, but the collection description can be modified.</div>


<span id="077fad06"></span>
# **request parameters**


|**parameter** |**sub\-parameter** |**sub\-parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|---|---|
|collectionName |*  |*  |String |Yes |*  |Specifies the modified Collection name.<br><br><br>* Must contain only English letters, numbers, and underscores (_), must begin with an English letter, and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |
|UpdateCollectionOptions |Description |*  |String |No |" |The new description for the collection.<br><br><br>* Length requirement: [0,65535]. |
||Fields<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">List of Field instances. The maximum number of Field instances in a Collection is 200.</div><br> |FieldName |String |Yes |*  |Specifies the name of the new field to add.<br><br><br>* Must contain only English letters, numbers, and underscores (_), must begin with an English letter, and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Field names cannot be repeated. |
|||FieldType |String |Yes |*  |Specify a custom field type, such as vikingDB. String, with optional values as detailed in **fieldType optional value**Explanation. |
|||DefaultVal |Same as FieldType |No |*  |Specify the default value of the custom field, see the default value for details **FieldType optional value**Explanation.<br><br><br>* When FieldName is the primary key, DefaultVal does not take effect and is not validated. |
|||Dim |Int |Required when FieldType is vector |*  |Specify a custom field vector dimension.<br><br><br>* Value range: [4, 2048], and must be a multiple of 4.<br><br>* Vector dimension refers to the number of elements contained in a vector. |
|||IsPrimaryKey |Bool |Yes |False |Specifies whether the field is the primary key. You can select one 'int64' or 'string' field to be the primary key. Each collection must have exactly one primary key.<br><br><br>* Enumeration values: True/False. |
|||PipelineName |String |Optional when FieldType is text |*  |Text. The plain text preprocessing capability pipeline refers to the preprocessing process that the vector database automates text slicing, text vectorization, warehousing, and storage. Support writing to the original data source in string form.<br><br>pipeline_name enumeration values are as follows:<br><br><br>* text_split_bge_large_zh: The vector database uses a slicer to split long text into short text, and calls the embedding model to vectorize short text.<br><br>* text_bge_large_zh: The vector database does not split the text, and directly calls the embedding model to vectorize the text.<br><br>* text_split_bge_m3: The vector database uses the slicer to divide the long text into short text, calls the bge m3 model to extract the sparse features and dense features of the short text, and stores the dense vector field and sparse vector field preset by the system.<br><br>* text_bge_m3: The vector database does not divide the text, directly calls bge m3 to extract the sparse features and dense features of the short text, and stores the dense vector field and sparse vector field preset by the system.<br><br>* text_split_bge_large_and_m3: The vector database uses the slicer to divide the long text into short texts, calls the bge v1.5 model to extract the dense features of the short text and stores it in the dense vector field preset by the system; calls the bge m3 model to extract the sparse features of the short text and stores it in the sparse vector field preset by the system.<br><br>* The vector database does not split the text; it calls the bge v1.5 model to extract dense features and the bge m3 model to extract sparse features, storing them in the system's preset dense and sparse vector fields respectively. |


<span id="c1fb2190"></span>
## field_type optional value


|**field type** |**Available index types** |**default_val default** |**When data is written**<br><br>**value range** |**default_val**<br><br>**value range** |**Can be the primary key** |**Description** |
|---|---|---|---|---|---|---|
|Int 64 |Enumeration |0 |Int64 range |Int64 range |Yes |Integer |
|Float32 |Range |0.0 |Float32 range |Float32 range |No |Floating point number |
|String |Enumeration |"Default" |*  |Length < = 128 |Yes |String |
|Bool |Enumeration |False |True/false |True/false |No |Boolean type |
|List\ < string \> |Enumeration |["Default"] |List length < = 32 |List length < = 32 |No |String array |
|List\ < int64 \> |Enumeration |[0] |List length < = 32 |List length < = 32 |No |Integer array |
|Vector |Vector |*  |Dimension 4\-2048 |*  |No |Dense vector.<br><br><br>* The 'dim' parameter is required when 'field_type' is 'vector'. |
|sparse_vector |Sparse vector |*  |Non\-zero subscript Unlimited<br><br>Non\-zero values are in the float32 range |*  |No |Sparse vector.<br><br><br>* sparse_vector cannot be set separately, it must be set in combination with the vector field.<br><br>* Accepts a JSON object of <index, value\> pairs, where 'index' represents a keyword and 'value' represents its weight.<br><br>> Example:<br><br>> sparse_vector = |
|Text |*  |*  |*  |*  |No |Text, note:<br><br><br>* Optional parameter pipeline_name field_type set to text.<br><br>* When adding a 'text' field with a 'PipelineName', you cannot add a 'vector' field, and only one such 'text' field is allowed. When adding a 'text' field without a 'PipelineName', 'vector' fields are allowed, and you can add multiple 'text' fields (up to the 200\-field limit). |


<span id="ae99fd48"></span>
# Example

<span id="73244e2e"></span>
## Request parameters

```Go
fields := []vikingdb.Field{
    {
       FieldName: "new_field1",
       FieldType: vikingdb.String,
    },
    {
       FieldName:  "new_field2",
       FieldType:  vikingdb.Float32,
       DefaultVal: 100,
    },
}
updateCollectionOptions := vikingdb.NewUpdateCollectionOptions().SetFields(fields).SetDescription("new field")
err := service.UpdateCollection("goTest", updateCollectionOptions)
if err != nil {
    fmt.Println(err)
}
```


<span id="631eaca6"></span>
## Return value

If successful, this operation does not return any data.
