---
title: "create_collection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_create_collection"
---

<span id="a962107a"></span>
# Overview

The create_collection method allows you to create a new dataset Collection. You can define the collection's structure by specifying its fields, including a primary key, and optionally configure automatic vectorization for text and image data. This document provides a complete reference, including all request parameters, field type options, and a Python SDK example.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Each Collection must have a primary key field. When you add a field of type <code>vector</code> to the <code>fields</code> definition, you cannot add another <code>vector</code> field, because only one vector field is supported per Collection.</div>


* <div data-tips="true" data-tips-type="tip">It is recommended to vectorize image and text data through the vectorize parameter. Users who use a pipeline for text vectorization must still provide the pipeline_name sub\-parameter.</div>


* <div data-tips="true" data-tips-type="tip">When you add a text field with <code>pipeline_name</code> to the <code>fields</code> definition, you cannot add <code>vector</code> or <code>sparse_vector</code> fields, and you can only have one such text field. When you add a text field without <code>pipeline_name</code>, you can add <code>vector</code> fields and multiple text fields without <code>pipeline_name</code> (up to 200 total fields).</div>



<span id="eac3ac0f"></span>
# **request parameters**


|**parameter** |**sub\-parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|---|
|collection_name |*  |String |Yes |*  |Specifies the name of the Collection created.<br><br><br>* Can only contain English letters, numbers, and underscores (_). Must begin with an English letter and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |
|Description |*  |String |No |" |Description of Custom Collection.<br><br><br>* Length requirement: [0,65535]. |
|Fields<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">List of Field instances. The maximum number of Field instances in a Collection is 200.</div><br> |field_name |String |Yes |*  |Specify the name of the custom field.<br><br><br>* Can only contain English letters, numbers, and underscores (_). Must begin with an English letter and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Field names cannot be repeated. |
| |field_type |String |Yes |*  |Specify a custom field type, such as FieldType. String, with optional values as detailed in the **field_type optional values** section. |
| |default_val |Consistent with field_type |No |*  |Specify the default value of the custom field, see the **field_type optional values** section for details on default values.<br><br><br>* When `field_name` is a primary key, `default_val` does not take effect and is not validated. |
| |dim |Int |Required when field_type is a vector |*  |The `dim` parameter is required when `field_type` is set to `vector`.<br><br><br>* Value range: [4, 4096], and must be a multiple of 4.<br><br>* Vector dimension refers to the number of elements contained in a vector. |
| |is_primary_key |Bool |Yes |False |Specifies whether the custom field is the primary key, which is used to uniquely identify a row of data.<br><br>Setting a custom field as a primary key is only supported if it is of type int64/string.<br><br>**Each collection has one and only one primary key**, the `is_primary_key` setting for all other fields defaults to `False`. If all fields are set to `False`, a primary key is automatically generated.<br><br><br>* Enumeration values: True/False. |
|Vectorize |Dense |Map |No (fill in<br><br>Required when vectorizing) |\-\- |Vectorization parameters of dense vectors. See the **Vectorization parameter** table below for sub\-parameters. |
||Sparse |Map |No |\-\- |The vectorization parameter of the sparse vector. If you don't need a sparse vector, you don't have to fill it in. See the **Vectorization parameter** table below for sub\-parameters. |


<span id="10162d12"></span>
## field_type optional value


|**field type** |**Available index types** |**default_val default** |**When data is written**<br><br>**Value range when writing data** |**default_val**<br><br>**Default value range** |**Can be the primary key** |**explain** |
|---|---|---|---|---|---|---|
|Int 64 |Enumeration |0 |Int64 range |Int64 range |Yes |Integer |
|Float32 |Floating\-point number |0.0 |Float32 range |Float32 range |No |Floating point number |
|String |Enumeration |"Default" |*  |Length < = 128 |Yes |String |
|Bool |Enumeration |False |True/false |True/false |No |Boolean type |
|List\ < string \> |Enumeration |["Default"] |List length < = 32 |List length < = 32 |No |String array |
|List\ < int64 \> |Enumeration |[0] |List length < = 32 |List length < = 32 |No |Integer array |
|Vector |Vector |*  |Dimension 4\-2048 |*  |No |Dense vector.<br><br><br>* The `dim` parameter is required when `field_type` is set to `vector`. |
|sparse_vector |Sparse vector |*  |Non\-zero subscript Unlimited<br><br>Non\-zero values are in the float32 range |*  |No |Sparse vector.<br><br><br>* sparse_vector cannot be set separately, it must be set in combination with the vector field.<br><br>* Receives a JSON object of `{"index": value}` pairs to represent the keywords and their corresponding weight values for the sparse vector.<br><br>> Example:<br><br>> sparse_vector = |
|Text |*  |*  |*  |*  |No |Text, which can be used to be vectorized. |
|Image |\-\- |\-\- |\-\- |\-\- |No |* Currently, writing to the tos path is supported. The format is:`tos://{bucket}/{object_key}`.<br><br>* Image, can be used for vectorization. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The <code>pipeline_name</code> parameter is optional and can be used when <code>field_type</code> is set to <code>text</code>.</div>


* <div data-tips="true" data-tips-type="warning">When you add a text field with <code>pipeline_name</code> to the <code>fields</code> definition, you cannot add <code>vector</code> or <code>sparse_vector</code> fields, and only one text field with <code>pipeline_name</code> is allowed. When you add a text field without <code>pipeline_name</code>, you can add <code>vector</code> and <code>sparse_vector</code> fields, as well as multiple text fields without <code>pipeline_name</code> (up to 200 total fields).</div>



<span id="cee4b2d3"></span>
### Vectorization parameter


|Parameter name |Type |Required |Default value |Note |
|---|---|---|---|---|
|text_field |String |No |/ |Text field to be vectorized |
|image_field |String |No |/ |Image field to be vectorized |
|model_name |String |Yes |/ |Model name. Corresponds to a model name in the **Model list** table. |
|model_version |String |No |/ |Model version. If there are multiple versions of a model, you can specify a specific version. If the default version of the model is used or the model does not have multiple versions, this field is not required. |
|dim |Int |No |/ |If you need to generate dense vectors, specify the vector dimensions. Default model dimensions are used. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">text_field and image_field settings need to correspond to the model selection. For example, if you select a plain text embedding model for <code>model_name</code>, the <code>image_field</code> parameter is not allowed.</div>


<span id="42cbce2d"></span>
### Model list

> In utilizing the embedding models for the creation of vectorized data, it may be necessary for your uploaded data to be transmitted to BytePlus's servers located in Malaysia for processing purposes. Please be advised that BytePlus does not store your data, inclusive of any processed data, on our Malaysian servers.



|Model name |Supports vectorization type |Default dense vector dimension |Optional dense vector dimension |Support for sparse vectors |Requires instructions |Default version |Optional version |
|---|---|---|---|---|---|---|---|
|Bge\-large\-zh |Text |1024 |1024 |No |No | | |
|BGE\-M3 |Text |1024 |1024 |Yes |No | | |
|bge\-visualized\-m3 |text_image, image |1024 |1024 |No |No | | |


<span id="59c16c83"></span>
# Example

<span id="3ce47310"></span>
## Request parameters

If there is an error, try to update the SDK package: pip install \-\-upgrade volcengine

```Python
# Define dataset fields, including primary key, string fields, text fields, and image fields
fields = [
    Field(field_name="f_id", field_type=FieldType.String, is_primary_key=True),  # Primary key field
    Field(field_name="f_string", field_type=FieldType.String, default_val=""),  # String field
    Field(field_name="f_text1", field_type=FieldType.Text),  # Text field 1
    Field(field_name="f_text2", field_type=FieldType.Text),  # Text field 2
    Field(field_name="f_image1", field_type=FieldType.Image),  # Image field 1
    Field(field_name="f_image2", field_type=FieldType.Image),  # Image field 2
]

# Define vectorization configuration, including dense and sparse vectors
vectorize = [
    VectorizeTuple(
        dense=VectorizeModelConf(
        model_name="bge-visualized-m3",  # Name of the model used
        # model_version="241215",  # Model version
        text_field="f_text1",  # Text field 1
        image_field="f_image1",  # Image field 1
        dim=1024,  # Dimension of the vector
        ),
        sparse=VectorizeModelConf(
            model_name="bge-m3",  # Name of the sparse model used
            text_field="f_text1",  # Sparse vectorization text field
        )
    )
]

# Create dataset, providing field definitions, description, and vectorization configuration
collection = vikingdb_service.create_collection(
    "test_coll_for_sdk_with_vectorize",  # Dataset name
    fields=fields,  # Field definitions
    description="test for sdk",  # Dataset description
    vectorize=vectorize  # Vectorization configuration
)

# Print dataset information
print(collection.collection_name)  # Output dataset name
print(collection.description)  # Output dataset description
print(collection.vectorize)  # Output dataset vectorization configuration
```


<span id="92994b04"></span>
## Return value

The Python call performs the above task and returns the Collection instance. The properties contained in the Collection instance are shown in the following table.


|**attribute** |**type** |**explain** |
|---|---|---|
|collection_name |String |Collection name. |
|Description |String |Collection description. |
|Fields |List < Field \> |List of fields. |
|Indexes |List < Index \> |Index list. |
|Stat |Map |Statistics/status information.<br><br><br>* data_number: Number of data records.<br><br>* data_storage: The storage size occupied by the data, in bytes. |
|create_time |String |Dataset creation time. |
|update_time |String |Dataset update time. |
|update_person |String |The user who last updated the dataset. |
