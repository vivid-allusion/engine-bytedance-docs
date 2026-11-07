---
title: "createCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_createCollection"
---

<span id="5810a251"></span>
# Overview

The createCollection method is used to create a new Collection, which serves as a container for your dataset. This reference provides a comprehensive guide to all request parameters, including how to define the collection's schema by specifying fields, data types, and a primary key. You will also learn how to configure automatic data vectorization for text and image fields and see a complete Java SDK code example.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Each Collection must specify a primary key field. When defining fields, if you add a field of type <code>vector</code>, you cannot add another <code>vector</code> field. Because only a single vector field is supported, you cannot add multiple vector fields.</div>


* <div data-tips="true" data-tips-type="tip">It is recommended to vectorize image and text data through the vectorize parameter. Users who have used a pipeline for text vectorization must still provide the <code>pipeline_name</code> sub\-parameter.</div>


* <div data-tips="true" data-tips-type="tip">When defining fields, if you add a <code>text</code> field that specifies a <code>pipeline_name</code>, you cannot add <code>vector</code> or <code>sparse_vector</code> fields, and only one such <code>text</code> field is allowed. If you add a <code>text</code> field without a <code>pipeline_name</code>, you can add <code>vector</code> fields and multiple <code>text</code> fields (up to 200 total fields).</div>



<span id="9adcbb8a"></span>
# **request parameters**

The request parameters are CreateCollectionParam, and the parameters included in the CreateCollectionParam class are shown in the following table.


|**parameter** |**sub\-parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|---|
|collectionName |*  |String |Yes |*  |Specifies the name of the Collection created.<br><br><br>* Must contain only English letters, numbers, and underscores (_), and must begin with an English letter.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |
|Description |*  |String |No |"" |Description of Custom Collection.<br><br><br>* Length requirement: [0,65535]. |
|Fields<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">List of Field instances. The maximum number of Field instances in a Collection is 200.</div><br> |FieldName |String |Yes |*  |Specify the name of the custom field.<br><br><br>* Must contain only English letters, numbers, and underscores (_), and must begin with an English letter.<br><br>* Length requirements: [1,128].<br><br>* Field names cannot be repeated. |
||fieldType |String |Yes |*  |Specify a custom field type, such as FieldType. String, with optional values as detailed in the **fieldType optional values section.**  |
||defaultVal |Consistent with fieldType |No |*  |Specify the default value of the custom field, see the **fieldType optional values section for details on the default value.** <br><br><br>* When fieldName is the primary key, defaultVal does not take effect and is not validated. |
||Dimension |Int |Required when fieldType is vector |*  |Specify a custom field vector dimension.<br><br><br>* Value range: [4, 4096], and must be a multiple of 4.<br><br>* Vector dimension refers to the number of elements contained in a vector. |
||isPrimaryKey |Bool |Yes |False |Specifies whether the custom field is the primary key, which is used to uniquely identify a row of data.<br><br>Setting a custom field as a primary key is only supported if it is of type int64/string.<br><br>**Each collection has one and only one primary key**, for other fields, `is_primary_key` defaults to `False`.**If all fields are False, the primary key is automatically generated.** <br><br><br>* Enumeration values: True/False. |
|Vectorize |Dense |Map |No (fill in<br><br>Required when vectorizing) |\-\- |Vectorization parameters of dense vectors. For sub\-parameters, see the **Vectorization parameters table below.**  |
||Sparse |Map |No |\-\- |The vectorization parameter of the sparse vector. This is not required if you do not need a sparse vector. For sub\-parameters, see the **Vectorization parameters table below.**  |


<span id="26ab2e76"></span>
## **fieldType optional value**


|**field type** |**Available index types** |**defaultVal default** |**When data is written**<br><br>**value range** |**defaultVal**<br><br>**value range** |**Can be the primary key** |**explain** |
|---|---|---|---|---|---|---|
|Int 64 |Enumeration |0 |Int64 range |Int64 range |Yes |Integer |
|Float32 |Range |0.0 |Float32 range |Float32 range |No |Floating point number |
|String |Enumeration |"Default" |*  |Length < = 128 |Yes |String |
|Bool |Enumeration |False |True/false |True/false |No |Boolean type |
|List\ < string \> |Enumeration |["Default"] |List length < = 32 |List length < = 32 |No |String array |
|List\ < int64 \> |Enumeration |[0] |List length < = 32 |List length < = 32 |No |Integer array |
|Vector |Vector |*  |Dimension 4\-2048 |*  |No |Dense vector.<br><br><br>* The `dim` parameter is required when `fieldType` is `vector`. |
|sparse_vector |Sparse vector |*  |Non\-zero subscript Unlimited<br><br>Non\-zero values are in the float32 range |*  |No |Sparse vector.<br><br><br>* sparse_vector cannot be set separately, it must be set in combination with the vector field.<br><br>* Accepts a JSON object of key\-value pairs (`<index>: <value>`) representing the keywords and their corresponding weights for the sparse vector.<br><br>> Example:<br><br>> sparse_vector = |
|Text |*  |*  |*  |*  |No |Text, which can be used for vectorization. |
|Image |\-\- |\-\- |\-\- |\-\- |No |* Currently, writing to the tos path is supported. The format is:`tos://{bucket}/{object_key}`.<br><br>* Can be used for vectorization. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The <code>pipeline_name</code> parameter is optional when <code>field_type</code> is <code>text</code>.</div>


* <div data-tips="true" data-tips-type="warning">When defining fields, if you add a <code>text</code> field that specifies a <code>pipeline_name</code>, you cannot add <code>vector</code> or <code>sparse_vector</code> fields, and only one such <code>text</code> field is allowed. If you add a <code>text</code> field without a <code>pipeline_name</code>, you can add <code>vector</code> and <code>sparse_vector</code> fields, and multiple <code>text</code> fields (up to 200 total fields).</div>



<span id="3bf476af"></span>
### Vectorization parameter


|Parameter name |Type |Required |Default value |Note |
|---|---|---|---|---|
|text_field |String |No |/ |Text field to be vectorized |
|image_field |String |No |/ |Image field to be vectorized |
|model_name |String |Yes |/ |Model name. Corresponds to the following\*\*"Model List"\*\*The model name. |
|model_version |String |No |/ |Model version. If there are multiple versions of a model, you can specify a specific version. If the default version of the model is used or the model does not have multiple versions, this field is not required. |
|Dimming |Int |No |/ |If you need to generate dense vectors, you can specify the vector dimensions. If not specified, the model's default dimension is used. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">text_field and image_field settings need to correspond to the choice of model. For example, if <code>model_name</code> is set to a plain text embedding model, <code>image_field</code> is not allowed.</div>


<span id="07ea23dc"></span>
### Model list

> In utilizing the embedding models for the creation of vectorized data, it may be necessary for your uploaded data to be transmitted to BytePlus's servers located in Malaysia for processing purposes. Please be advised that BytePlus does not store your data, inclusive of any processed data, on our Malaysian servers.



|Model name |Supported vectorization type |Default dense vector dimension |Optional dense vector dimension |Supports sparse vectors |Requires instructions |Default version |Optional version |
|---|---|---|---|---|---|---|---|
|Bge\-large\-zh |Text |1024 |1024 |No |No | | |
|BGE\-M3 |Text |1024 |1024 |Yes |No | | |
|bge\-visualized\-m3 |text_image, image |1024 |1024 |No |No | | |


<span id="05437660"></span>
# Example

<span id="eea76cb3"></span>
## Request parameters

```Java
CreateCollectionParam collectionParam = new CreateCollectionParam()
    .setCollectionName("test_coll_for_sdk_with_vectorize")  // Collection name
    .setDescription("this is an example for sdk test")  // Description
    .setFields(new ArrayList(){{
        // Define fields, including primary key, string, text, and image fields
        add(new Field().setFieldType(FieldType.Int64).setFieldName("f_id").setPrimaryKey(true).build());  // Primary key field
        add(new Field().setFieldType(FieldType.String).setFieldName("f_string").build());  // String field
        add(new Field().setFieldType(FieldType.Text).setFieldName("f_text1").build());  // Text field
        add(new Field().setFieldType(FieldType.Text).setFieldName("f_text2").build());  // Text field
        add(new Field().setFieldType(FieldType.Image).setFieldName("f_image1").build());  // Image field
        add(new Field().setFieldType(FieldType.Image).setFieldName("f_image2").build());  // Image field
    }})
    .setVectorize(new ArrayList(){{
        // Define vectorization configuration, including dense and sparse vectors
        add(new VectorizeTuple()
            .setDense(new VectorizeTuple.VectorizeModelConf()
            .setTextField("f_text1")
            .setImageField("f_image1")
            .setModelName("bge-visualized-m3")
            .setDim(1024)
            .build())  // Dense vector configuration
        .setSparse(new VectorizeTuple.VectorizeModelConf()
        .setTextField("f_text2")
        .setModelName("bge-m3")
        .build())  // Sparse vector configuration
    .build()
    );
}})
.build();
        
// Call the `createCollection` method of the service to create the collection
vikingDBService.createCollection(collectionParam);
```


<span id="615489a7"></span>
## Return value

A Java call to perform the above task returns a `Collection` instance. The properties contained in the Collection instance are shown in the following table.


|**attribute** |**type** |**explain** |
|---|---|---|
|collectionName |String |Collection name. |
|Description |String |Collection description. |
|Fields |ArrayList < Field \> |List of fields. |
|Indexes |ArrayList < Index \> |Index list. |
|Stat |Map |Statistics/status information.<br><br><br>* data_number: number of data items.<br><br>* data_storage: The storage size occupied by the data, in bytes. |
|createTime |String |Collection creation time. |
|UpdateTime |String |Collection update time. |
|UpdatePerson |String |The user who last updated the collection. |
