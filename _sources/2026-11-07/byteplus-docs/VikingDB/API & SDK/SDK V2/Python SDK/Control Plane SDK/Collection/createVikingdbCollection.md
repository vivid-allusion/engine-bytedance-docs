---
title: "createVikingdbCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/createVikingdbCollection_v2"
---

<span id="overview"></span>
# Overview

This interface is used to create a vector database Collection. A maximum of 200 collections can be created under a single account.


* Each Collection must specify a primary key field.

* After adding a vector type field to the defined `fields`, when adding new fields, the `vector` type cannot be selected as the field type. Currently, only single vector is supported, and multiple vector fields cannot be added.

* When creating a collection, please clarify the configuration method based on data type: If you have existing vector data, fill in the vector field; if you need to vectorize multimodal data (such as images and text), configure the `vectorize` parameter. The two have different data processing logic, and only one can be selected during creation; they cannot be used simultaneously.

* The maximum number of `fields` in a Collection is 200.


<span id="method-definition"></span>
# Method Definition

The Python SDK initiates calls through `VIKINGDBApi().create_vikingdb_collection(request)`, where `request` is of type `volcenginesdkvikingdb.CreateVikingdbCollectionRequest`.

<span id="request-parameters"></span>
# **Request Parameters**

The table below only lists the request parameters specific to this interface and some common parameters. For more information, see [Common Parameters](https://www.volcengine.com/docs/6369/67268).


|Parameter |Type |Required |Description |
|---|---|---|---|
|project_name |str |No |Project name, corresponding to API field `ProjectName`. If not filled, it defaults to `default`. |
|collection_name |str |Yes |Collection name, corresponding to API field `CollectionName`<br><br><br>* Can only use English letters, numbers, and underscores `_`, must start with an English letter, and cannot be empty<br><br>* Length (bytes) requirement: [1, 128]<br><br>* Collection names cannot be duplicated under the same account<br><br>* The number of Collections under the same account cannot exceed 200 |
|description |str |No |Collection description, corresponding to API field `Description`, maximum 65535 bytes. |
|fields |list[FieldForCreateVikingdbCollectionInput] |Yes |Field definition list, corresponding to API field `Fields`<br><br><br>* Can only use English letters, numbers, and underscores `_`, must start with an English letter, and cannot be empty.<br><br>* Length (bytes) requirement: [1, 128]<br><br>* Field names cannot be duplicated under the same Collection<br><br>* Must contain at least one primary key field (string/int64)<br><br>* The number of fields under a single Collection cannot exceed 200 |
|vectorize |VectorizeForCreateVikingdbCollectionInput |No |Vectorization configuration, corresponding to API field `Vectorize`. Supports dense/sparse model combinations. |



* FieldForCreateVikingdbCollectionInput parameter structure



|Parameter |Type |Required |Description |
|---|---|---|---|
|field_name |str |Yes |Field name, corresponding to API field `FieldName`. Must start with a letter, can contain letters, numbers, and underscores, length 1\-128 bytes. |
|field_type |str |Yes |Field type, corresponding to API field `FieldType`. See `field_type` list below for optional values. |
|default_value |object |No |Field default value, corresponding to API field `DefaultValue`. vector / sparse_vector / text / image / video types do not support default values. |
|dim |int |No |Dense vector dimension, corresponding to API field `Dim`. Required for vector fields, range 4\-4096, must be a multiple of 4. |
|is_primary_key |bool |No |Whether it is a primary key, corresponding to API field `IsPrimaryKey`. Only string / int64 fields can be set as primary keys; if not specified, the system will generate `"__AUTO_ID__"`. |



* VectorizeForCreateVikingdbCollectionInput parameter structure



|Parameter |Type |Required |Description |
|---|---|---|---|
|dense |DenseForCreateVikingdbCollectionInput |Yes |Dense vectorization configuration, corresponding to API field `Dense`. Used to specify embedding model, dimension, and input fields. |
|sparse |SparseForCreateVikingdbCollectionInput |No |Sparse vectorization configuration, corresponding to API field `Sparse`. |



* DenseForCreateVikingdbCollectionInput and SparseForCreateVikingdbCollectionInput parameter structure



|Parameter |Type |Required |Description |
|---|---|---|---|
|model_name |str |Yes |Model name, corresponding to API field `ModelName`. See embedding model list below for optional values. |
|model_version |str |No |Model version, corresponding to API field `ModelVersion`. Required for Doubao series models, defaults to `default` for bge series. |
|dim |int |No |Dense vector dimension. See embedding model list for dimensions supported by each model. |
|text_field |str |No |Text vectorization field name, corresponding to API field `TextField`. |
|image_field |str |No |Image vectorization field name, corresponding to API field `ImageField`. |
|video_field |str |No |Video vectorization field name, corresponding to API field `VideoField`. |


<span id="field-type"></span>
# field_type


|Field Type |Format |Can be Primary Key |Description |
|---|---|---|---|
|int64 |Integer value |Yes |Integer<br><br><br>* When used as primary key, cannot be 0 |
|float32 |Floating point value |No |Floating point number |
|string |String |Yes |String.<br><br><br>* Recommended usage: When used for enumeration value filtering, recommended length should not exceed 128 bytes<br><br>* Hard limit: Must not exceed 65535 bytes; when used as primary key, length must not exceed 256 bytes |
|bool |true/false |No |Boolean type |
|list |String array |No |String array<br><br><br>* Recommended usage: When used for enumeration value filtering, list length should not exceed 32, single element should not exceed 1024 bytes<br><br>* Hard limit: List length should not exceed 20000, single element should not exceed 1024 bytes, total size should not exceed 1MB |
|list |Integer array |No |Integer array<br><br><br>* Hard limit: List length should not exceed 1024 |
|vector |* Vector (floating point array)<br><br>* Base64 encoding after float32/float64 compression to bytes |No |Dense vector<br><br><br>* Hard limit: Length not less than 4, not greater than 4096, and must be an integer multiple of 4. |
|sparse_vector |Dictionary list of input format, used to represent non\-zero position indices and corresponding values of sparse vector, where token_id is string type, token_weight is float type |No |Sparse vector |
|text |String |No |If it is a vectorization field, the value cannot be empty. (Otherwise, it can be empty)<br><br><br>* If it is a vectorization field, the value cannot be empty. (Otherwise, it can be empty)<br><br>* Hard limit: Must be less than 65535 bytes |
|image |String |No |If it is a vectorization field, the value cannot be empty. (Otherwise, it can be empty)<br><br><br>* Image tos link `tos://{bucket}/{object}`<br><br>* http/https format link<br><br>* Corresponding image must satisfy width and height greater than 14px, pixels less than 36 million<br><br>* Reference: [Multimodal Vectorization](https://www.volcengine.com/docs/82379/1409291?lang=zh#a256838b) |
|video |Object |No |If it is a vectorization field, the value cannot be empty. (Otherwise, it can be empty)<br><br><br>* Video tos link `tos://{bucket}/{object}`<br><br>* http/https format URL link<br><br>* Corresponding video must satisfy size not exceeding 50 MB<br><br>* Reference: [Multimodal Vectorization](https://www.volcengine.com/docs/82379/1409291?lang=zh#a256838b)<br><br><br>`Plain <br> { <br> "value": tos://{bucket}/{object} # or http/https format url link, this field is required <br> "fps": 0.2 # Value range 0.2-5, optional <br> } <br>` |
|date_time |string |No |Minute level:<br><br>`yyyy-MM-ddTHH:mmZ` or `yyyy-MM-ddTHH:mm±HH:mm`<br><br>Second level:<br><br>`yyyy-MM-ddTHH:mm:ssZ` or `yyyy-MM-ddTHH:mm:ss±HH:mm`<br><br>Millisecond level:<br><br>`yyyy-MM-ddTHH:mm:ss.SSSZ` or `yyyy-MM-ddTHH:mm:ss.SSS±HH:mm`<br><br>Example: "2025\-08\-12T11:33:56+08:00" |
|geo_point |string |No |Geographic coordinates `longitude,latitude`, where `longitude` range is (\-180,180), `latitude` range is (\-90,90)<br><br>Example: "116.408108,39.915023" |


<span id="model-list"></span>
## Model List


|Model Name |Model Version |Supported Vectorization Types |Default Dense Vector Dimension |Optional Dense Vector Dimensions |Text Truncation Length |Supports Sparse Vector |Supports instruction |
|---|---|---|---|---|---|---|---|
|bge\-large\-zh |(default) |text |1024 |1024 |512 |No |Yes |
|bge\-m3 |(default) |text |1024 |1024 |8192 |Yes |No |
|bge\-visualized\-m3 |(default) |text, image and their combinations |1024 |1024 |8192 |No |No |
|Skylark\-embedding |*240715* |text |2048 |512, 1024, 2048 |4096 |No |Yes |
|Skylark\-embedding\-vision |*250615* |Compatible with *241215* usage. Additionally, supports full_modal_seq (text/image/video sequence) |2048 |2048, 1024 |128k |No |Yes |


<span id="response-parameters"></span>
# **Response Parameters**

The table below only lists the response parameters specific to this interface. For more information, see [Response Structure](https://www.volcengine.com/docs/6369/80336).


|Parameter |Type |Description |
|---|---|---|
|message |str |Request status description, corresponding to API field `Message`. |
|resource_id |str |Newly created Collection ID, corresponding to API field `ResourceId`. |


<span id="request-example"></span>
# Request Example

<span id="create-a-collection-with-vector-fields"></span>
### Create a Collection with vector fields

```python
import os
import volcenginesdkcore
import volcenginesdkvikingdb as vdb
from volcenginesdkvikingdb.api.vikingdb_api import VIKINGDBApi

configuration = volcenginesdkcore.Configuration()
configuration.ak = os.environ["VIKINGDB_AK"]
configuration.sk = os.environ["VIKINGDB_SK"]
configuration.region = os.environ["VIKINGDB_REGION"]
configuration.host = os.environ["VIKINGDB_HOST"]
configuration.scheme = "https"
volcenginesdkcore.Configuration.set_default(configuration)

client = VIKINGDBApi()

request = vdb.CreateVikingdbCollectionRequest(
    collection_name="sdk_demo_collection",
    description="Create collection with vector fields",
    project_name="default",
    fields=[
        vdb.FieldForCreateVikingdbCollectionInput(
            field_name="item_id",
            field_type="int64",
            is_primary_key=True,
        ),
        vdb.FieldForCreateVikingdbCollectionInput(
            field_name="title",
            field_type="string",
        ),
        vdb.FieldForCreateVikingdbCollectionInput(
            field_name="dense_vector",
            field_type="vector",
            dim=768,
        ),
        vdb.FieldForCreateVikingdbCollectionInput(
            field_name="sparse_vector",
            field_type="sparse_vector",
        ),
        vdb.FieldForCreateVikingdbCollectionInput(
            field_name="f_int64",
            field_type="int64",
            default_value=123456,
        ),
    ],
)

response = client.create_vikingdb_collection(request)
print("message:", response.message)
print("resource_id:", response.resource_id)
```


<span id="create-a-collection-with-vectorize-auto-vectorization"></span>
### Create a Collection with vectorize (auto vectorization)

```python
import os
import volcenginesdkcore
import volcenginesdkvikingdb as vdb
from volcenginesdkvikingdb.api.vikingdb_api import VIKINGDBApi

configuration = volcenginesdkcore.Configuration()
configuration.ak = os.environ["VIKINGDB_AK"]
configuration.sk = os.environ["VIKINGDB_SK"]
configuration.region = os.environ["VIKINGDB_REGION"]
configuration.host = os.environ["VIKINGDB_HOST"]
configuration.scheme = "https"
volcenginesdkcore.Configuration.set_default(configuration)

client = VIKINGDBApi()

request = vdb.CreateVikingdbCollectionRequest(
    collection_name="sdk_demo_vectorize",
    description="Auto vectorize text and image",
    project_name="default",
    fields=[
        vdb.FieldForCreateVikingdbCollectionInput(
            field_name="doc_id",
            field_type="string",
            is_primary_key=True,
        ),
        vdb.FieldForCreateVikingdbCollectionInput(
            field_name="content",
            field_type="text",
        ),
        vdb.FieldForCreateVikingdbCollectionInput(
            field_name="cover_image",
            field_type="image",
        ),
        vdb.FieldForCreateVikingdbCollectionInput(
            field_name="f_int64",
            field_type="int64",
            default_value=123456,
        ),
    ],
    vectorize=vdb.VectorizeForCreateVikingdbCollectionInput(
        dense=vdb.DenseForCreateVikingdbCollectionInput(
            model_name="bge-m3",
            text_field="content",
        ),
        sparse=vdb.SparseForCreateVikingdbCollectionInput(
            model_name="bge-m3",
            text_field="content",
        ),
    ),
)

response = client.create_vikingdb_collection(request)
if response.resource_id:
    print("collection created:", response.resource_id)
else:
    print("request failed:", response.message)
```
