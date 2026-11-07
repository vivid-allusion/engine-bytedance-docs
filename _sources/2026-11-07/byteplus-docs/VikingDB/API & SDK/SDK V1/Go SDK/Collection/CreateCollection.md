---
title: "CreateCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_CreateCollection"
---

<span id="overview"></span>
# Overview

Use the CreateCollection operation to define and create a new data collection. This reference provides the necessary parameters to configure your collection's schema, including specifying fields, data types (such as vector and sparse_vector), and a primary key. You can also configure automatic vectorization for text and image data.


* Each Collection must specify a primary key field. When you add a field of the vector type to the fields definition, you cannot add another vector field. Because only one vector field is supported, you cannot add multiple vector fields.

* It is recommended to vectorize image and text data through the vectorize parameter. Users who have vectorized text using a pipeline should use the pipeline_name sub\-parameter.

* When adding fields to the definition: if you add a text field that has a pipeline_name, you cannot add vector or sparse_vector fields, and you can only have one such text field. If you add a text field without a pipeline_name, you can add vector fields and multiple text fields without a pipeline_name (up to 200 total fields).


<span id="request-parameters"></span>
# **request parameters**


|**parameter** |**sub\-parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|---|
|collectionName |*  |String |Yes |*  |Specifies the name of the Collection created.<br><br><br>* Must contain only English letters, numbers, and underscores (_), and must begin with an English letter.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |
|Description |*  |String |No |" |Description of Custom Collection.<br><br><br>* Length requirement: [0,65535]. |
|Fields<br><br>List of Field instances. The maximum number of Field instances in a Collection is 200. |FieldName |String |Yes |*  |The name of the custom field.<br><br><br>* Must contain only English letters, numbers, and underscores (_), and must begin with an English letter.<br><br>* Length requirements: [1,128].<br><br>* Field names cannot be repeated. |
| |FieldType |String |Yes |*  |Specify a custom field type, such as vikingDB. String, with optional values as detailed in **fieldType optional value**Explanation. |
| |DefaultVal |Same as FieldType |No |*  |Specify the default value of the custom field, see the default value for details **FieldType optional value**Explanation.<br><br><br>* When FieldName is the primary key, DefaultVal does not take effect and is not validated. |
| |Dim |Int |Required when FieldType is vector |*  |Specify a custom field vector dimension.<br><br><br>* Value range: [4, 4096], and must be a multiple of 4.<br><br>* Vector dimension refers to the number of elements contained in a vector. |
| |IsPrimaryKey |Bool |Yes |False |Specifies whether the custom field is the primary key, which is used to uniquely identify a row of data.<br><br>Setting a custom field as a primary key is only supported if it is of type int64/string.<br><br>Each collection has one and only one primary key, the is_primary_key for other fields defaults to False. If all fields are set to False, a primary key is automatically generated.<br><br><br>* Enumeration values: True/False. |
|Vectorize<br><br>If there is a vectorize parameter, the fields should not be filled with pipeline. |Dense |Map |No (fill in<br><br>Required when vectorizing) |\-\- |Vectorization parameters of dense vectors. For sub\-parameters, see the **Vectorization parameter** table below. |
| |Sparse |Map |No |\-\- |The vectorization parameter of the sparse vector. If you don't need a sparse vector, you don't have to fill it in. See below for sub\-parameters\*\*"Vectorized parameter"\*\*Table. |


<span id="fieldtype-optional-value"></span>
## **fieldType optional value**


|**field type** |**Available index types** |**defaultVal default** |**When data is written**<br><br>**value range** |**defaultVal**<br><br>**value range** |**Can be the primary key** |**explain** |
|---|---|---|---|---|---|---|
|Int 64 |Enumeration |0 |Int64 range |Int64 range |Yes |Integer |
|Float32 |Range |0.0 |Float32 range |Float32 range |No |Floating point number |
|String |Enumeration |"Default" |*  |Length < = 128 |Yes |String |
|Bool |Enumeration |False |True/false |True/false |No |Boolean type |
|List\ < string \> |Enumeration |["Default"] |List length < = 32 |List length < = 32 |No |String array |
|List\ < int64 \> |Enumeration |[0] |List length < = 32 |List length < = 32 |No |Integer array |
|Vector |Vector |*  |Dimension 4\-2048 |*  |No |Dense vector.<br><br><br>* Required parameter dim when fieldType is set to vector. |
|sparse_vector |Sparse vector |*  |Non\-zero subscript Unlimited<br><br>Non\-zero values are in the float32 range |*  |No |Sparse vector.<br><br><br>* sparse_vector cannot be set separately, it must be set in combination with the vector field.<br><br>* Accepts a JSON object of <index, value\> pairs representing the non\-zero elements of the sparse vector and their corresponding weights.<br><br>> Example:<br><br>> sparse_vector = |
|Text |*  |*  |*  |*  |No |Text, which can be used for vectorization. |
|Image |\-\- |\-\- |\-\- |\-\- |No |* Currently, writing to the tos path is supported. The format is:`tos://{bucket}/{object_key}`.<br><br>* Can be used for vectorization. |



* The optional pipeline_name parameter can be used when field_type is set to text.

* When adding fields to the definition: if you add a text field with a pipeline_name, you cannot add vector or sparse_vector fields, and you can only have one such text field. If you add a text field without a pipeline_name, you can add vector and sparse_vector fields, as well as multiple text fields without a pipeline_name (up to 200 total fields).


<span id="vectorization-parameter"></span>
### Vectorization parameter


|Parameter name |Type |Required |Default value |Note |
|---|---|---|---|---|
|text_field |String |No |/ |Text field to be vectorized |
|image_field |String |No |/ |Image field to be vectorized |
|model_name |String |Yes |/ |Model name. Corresponds to the following\*\*"Model List"\*\*The model name. |
|model_version |String |No |/ |Model version. If there are multiple versions of a model, you can specify a specific version. If the default version of the model is used or the model does not have multiple versions, this field is not required. |
|Dim |Int |No |/ |If you need to generate dense vectors, specify the vector dimensions. Default model dimensions are used. |


text_field and image_field settings need to correspond to the choice of model. For example, if model_name is a plain text embedding model, image_field is not allowed.

<span id="model-list"></span>
### Model list

> In utilizing the embedding models for the creation of vectorized data, it may be necessary for your uploaded data to be transmitted to BytePlus's servers located in Malaysia for processing purposes. Please be advised that BytePlus does not store your data, inclusive of any processed data, on our Malaysian servers.



|Model name |Supports vectorization type |Default dense vector dimension |Optional dense vector dimension |Support for sparse vectors |Need instructions |Default version |Optional version |
|---|---|---|---|---|---|---|---|
|Bge\-large\-zh |Text |1024 |1024 |No |No | | |
|BGE\-M3 |Text |1024 |1024 |Yes |No | | |
|bge\-visualized\-m3 |text_image, image |1024 |1024 |No |No | | |


<span id="example"></span>
# Example

<span id="request-parameters"></span>
## Request parameters

```Python
import (
        "fmt"
        "testing"
        "github.com/volcengine/volc-sdk-golang/service/vikingdb"
)
```


Create a dense vector + sparse vector dataset

```Go
fields := []vikingdb.Field{ 
    {FieldName: "f_id", FieldType: vikingdb.String, IsPrimaryKey: true},  // Specify the primary key 
    {FieldName: "f_int64", FieldType: vikingdb.Int64},  // Specify an integer field 
    {FieldName: "f_vector", FieldType: vikingdb.Vector, Dim: 4},  // Specify a vector field with 4 dimensions 
    {FieldName: "f_sparse_vector", FieldType: vikingdb.Sparse_Vector},  // Specify a sparse_vector field 
} 

// Create a collection, specify the collection name, and define fields and other parameters 
collection, err := service.CreateCollection("test_coll_for_sdk_2", fields, "") 
if err != nil { 
    // Specify the error handling mode 
    panic(err) 
} 

// Specify to output the collection name 
fmt.Println(collection.CollectionName)
```


Create a multimodal dataset

```Go
fields := []vikingdb.Field{ 
    {FieldName: "f_id", FieldType: vikingdb.String, IsPrimaryKey: true},  // Specify the primary key 
    {FieldName: "f_int64", FieldType: vikingdb.Int64},  // Specify an integer field 
    {FieldName: "f_text1", FieldType: vikingdb.Text},  // Specify a text field 
    {FieldName: "f_text2", FieldType: vikingdb.Text},  // Specify a text field 
    {FieldName: "f_image1", FieldType: vikingdb.Image},  // Specify an image field 
    {FieldName: "f_image2", FieldType: vikingdb.Image},  // Specify an image field 
} 

// Specify the vectorize parameter 
vectorize := []*vikingdb.VectorizeTuple{ 
    vikingdb.NewVectorizeTuple(). 
    // Specify parameters for dense and sparse vectors 
    SetDense(vikingdb.NewVectorizeModelConf(). 
        SetTextField("f_text1"). 
        SetImageField("f_image1"). 
        SetModelName("Skylark-embedding-vision"). 
        SetModelVersion("241215"). 
        SetDim(3072)). 
    SetSparse(vikingdb.NewVectorizeModelConf(). 
        SetTextField("f_text2"). 
        SetModelName("bge-m3")), 
} 

// Create a collection, specify the collection name, define fields, and set vector parameters and other parameters 
collection, err := service.CreateCollection("test_coll_for_sdk_with_vectorize", fields, "", vectorize) 
if err != nil { 
    // Specify the error handling mode 
    panic(err) 
} 

// Specify to output the collection name 
fmt.Println(collection.CollectionName)
```


<span id="return-value"></span>
## Return value

The Go call performs the above task and returns a pointer to a Collection struct (\*Collection). The properties contained in the Collection structure are shown in the following table.


|**attribute** |**type** |**explain** |
|---|---|---|
|CollectionName |String |The name of the created Collection. |
|Description |String |Displays a description of the created Collection. |
|Fields |[] Field |Displays a list of fields created. |
|Indexes |[] interface {} |Displays a list of indexes created. |
|Stat |Map |Statistics/status information.<br><br><br>* data_number: number of data items.<br><br>* data_storage: The storage size occupied by the data, in bytes. |
|CreateTime |String |The time the Collection was created. |
|UpdateTime |String |Dataset update time. |
|UpdatePerson |String |The user who last updated the Collection. |
