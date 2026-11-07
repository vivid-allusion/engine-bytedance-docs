---
title: "CreateVikingdbCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/CreateVikingdbCollection"
---

<span id="overview"></span>
# Overview

This interface is used to create a vector database collection. A single account can create up to 200 collections.


* Each Collection must specify a primary key field.

* After defining a vector type field in fields, when adding new fields, the vector type cannot be selected. Currently, only single vector is supported, and multiple vector fields cannot be added.

* When creating a collection, please clarify the configuration method based on the data type: If you have existing vector data, fill in the vector field; if you need to vectorize multimodal data (such as images and text), configure the vectorize parameter. The two are different data processing logics, and only one can be selected during creation, not both.

* The maximum number of fields in a Collection is 200.


<span id="method-definition"></span>
# Method Definition

The Go SDK calls the `CreateVikingdbCollection(input)` method through the client instance created by `vikingdb.New(sess)` to initiate a collection creation request. The input parameter type is vikingdb.CreateVikingdbCollectionInput, which includes configurations such as collection name, description, project name, and field definitions.

<span id="request-parameters"></span>
# **Request Parameters**

The table below only lists the unique request parameters and some public parameters for this interface. For more information, please refer to [Public Parameters](https://www.volcengine.com/docs/6369/67268).


|Parameter |Type |Required |Description |
|---|---|---|---|
|ProjectName |string |No |The name of the project. Corresponds to the concept of "project" in Volcengine. If not filled, it will be treated as default by default. |
|CollectionName |string |Yes |The name of the collection, corresponding to the API field `CollectionName`<br><br><br>* Can only use English letters, numbers, underscores _, and start with an English letter, cannot be empty<br><br>* Length (bytes) requirements: [1, 128]<br><br>* Under the same account, all Collection names cannot be duplicated<br><br>* Under the same account, the number of Collections cannot exceed 200 |
|Description |string |No |Description of the collection<br><br>Maximum 65535 bytes |
|Fields |[]FieldForCreateVikingdbCollectionInput |Yes |Fields in the collection.<br><br>Limit: Maximum 200 fields in the collection. |
|Vectorize |VectorizeForCreateVikingdbCollectionInput |No |Vectorization configuration for the collection. |



* FieldForCreateVikingdbCollectionInput parameter structure



|Parameter |Type |Required |Description |
|---|---|---|---|
|FieldName |string |Yes |Field name.<br><br>Limit: English letters, numbers, or underscores. And must start with an English letter. Length does not exceed 64 bytes. |
|FieldType |FieldTypeEnum (enumeration type) |Yes |Field type. |
|DefaultValue |interface{} |No |Default value for field content.<br><br>Note: vector/sparse_vector/text/image/video type fields do not support default values. |
|Dim |Int |No |If the field type is vector, this parameter specifies the dimension of the dense vector. Supports 4\-4096 and must be an integer multiple of 4. |
|IsPrimaryKey |bool |No |Whether it is a primary key field. You can specify 1 primary key field (string or int64 type) for the collection. If not specified, an automatically generated primary key will be used, with the field name "**AUTO_ID**". |



* VectorizeForCreateVikingdbCollectionInput parameter structure



|Parameter |Type |Required |Description |
|---|---|---|---|
|Dense |DenseForCreateVikingdbCollectionInput |Yes |Dense vectorization model configuration |
|Sparse |SparseForCreateVikingdbCollectionInput |No |Sparse vectorization model configuration |



* DenseForCreateVikingdbCollectionInput and SparseForCreateVikingdbCollectionInput parameter structure



|Parameter |Type |Required |Description |
|---|---|---|---|
|ModelName |ModelNameEnum (enumeration type) |Yes |Model name.<br><br>See the embedding model list for enumeration values. |
|ModelVersion |string |No |Model version. If it is a doubao series model, the model version is required. If it is a bge series model, the default is default. |
|Dim |int |No |Dense vector dimension. See the embedding model list for dimensions supported by each model. |
|TextField |string |No |Text vectorization field name. |
|ImageField |string |No |Image vectorization field name. |
|VideoField |string |No |Video vectorization field name. |


<span id="field-type"></span>
# field_type


|Field Type |Format |Can be Primary Key |Description |
|---|---|---|---|
|int64 |Integer value |Yes |Integer<br><br><br>* When used as a primary key, it cannot be 0 |
|float32 |Floating point value |No |Floating point number |
|string |String |Yes |String<br><br><br>* Recommended usage: When used for enumeration value filtering, the recommended length does not exceed 128 bytes<br><br>* Hard limit: Must not exceed 65535 bytes; when used as a primary key, the length must not exceed 256 bytes |
|bool |true/false |No |Boolean type |
|[]string |String array |No |String array<br><br><br>* Recommended usage: When used for enumeration value filtering, the list length does not exceed 32, and a single element does not exceed 1024 bytes<br><br>* Hard limit: List length does not exceed 20000, a single element does not exceed 1024 bytes, and the total size does not exceed 1MB |
|[]int64 |Integer array |No |Integer array<br><br><br>* Hard limit: List length does not exceed 1024 |
|vector |* Vector (floating point array)<br><br>* Base64 encoding after float32/float64 is compressed to bytes |No |Dense vector<br><br><br>* Hard limit: Length not less than 4, not greater than 4096, and must be an integer multiple of 4. |
|sparse_vector |Input format: a list of dictionaries of <token_id, token_weight\> to represent the non\-zero index and corresponding value of the sparse vector, where token_id is string type and token_weight is float type |No |Sparse vector |
|text |string |No |If it is a vectorization field, the value cannot be empty. (Otherwise, it can be empty)<br><br><br>* If it is a vectorization field, the value cannot be empty. (Otherwise, it can be empty)<br><br>* Hard limit: Must be less than 65535 bytes |
|image |string |No |If it is a vectorization field, the value cannot be empty. (Otherwise, it can be empty)<br><br><br>* Image tos link `tos://{bucket}/{object}`<br><br>* http/https format link<br><br>* The corresponding image must meet width and height greater than 14px, pixels less than 36 million<br><br>* Reference: [Multimodal Vectorization](https://www.volcengine.com/docs/82379/1409291?lang=zh#a256838b) |
|video |map[string]interface{} |No |If it is a vectorization field, the value cannot be empty. (Otherwise, it can be empty)<br><br><br>* Video tos link `tos://{bucket}/{object}`<br><br>* http/https format url link<br><br>* The corresponding video must meet the size not exceeding 50mb<br><br>* Reference: [Multimodal Vectorization](https://www.volcengine.com/docs/82379/1409291?lang=zh#a256838b)<br><br><br>`Plain <br> { <br> "value": "tos://{bucket}/{object}" # Or http/https format url link, this field is required <br> "fps": 0.2 # Value range 0.2-5, optional <br> } <br>` |
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
|Skylark\-embedding\-vision |*250615* |Compatible with the usage of *241215*. In addition, supports full_modal_seq (text/image/video sequence) |2048 |2048, 1024 |128k |No |Yes |


<span id="response-parameters"></span>
# **Response Parameters**

The table below only lists the unique response parameters for this interface. For more information, please refer to [Response Structure](https://www.volcengine.com/docs/6369/80336).


|Parameter |Type |Description |
|---|---|---|
|Message |string |Message about the request status. |
|ResourceId |string |ID of the new collection. |


<span id="request-examples"></span>
# Request Examples

<span id="create-a-collection-with-vectorize-vectorization-configuration"></span>
### Create a collection with vectorize (vectorization) configuration

```Go
package main

import (
    "fmt"
    "os"

    "github.com/volcengine/volcengine-go-sdk/service/vikingdb"
    "github.com/volcengine/volcengine-go-sdk/volcengine"
    "github.com/volcengine/volcengine-go-sdk/volcengine/credentials"
    "github.com/volcengine/volcengine-go-sdk/volcengine/session"
)

func main() {
    var (
       accessKey = os.Getenv("VIKINGDB_AK")
       secretKey = os.Getenv("VIKINGDB_SK")
       region    = "ap-southeast-1"
    )
    config := volcengine.NewConfig().
       WithRegion(region).
       WithCredentials(credentials.NewStaticCredentials(accessKey, secretKey, ""))

    sess, err := session.NewSession(config)
    if err != nil {
       panic(err)
    }
    svc := vikingdb.New(sess)

    input := vikingdb.CreateVikingdbCollectionInput{
       CollectionName: volcengine.String("Your Collection Name"),
       Description:    volcengine.String("Your Collection Description"),
       ProjectName:    volcengine.String("default"),
       Fields: []*vikingdb.FieldForCreateVikingdbCollectionInput{
          {
             FieldName:    volcengine.String("item_id"),
             FieldType:    volcengine.String("int64"),
             IsPrimaryKey: volcengine.Bool(true),
          },
          {
             FieldName: volcengine.String("title"),
             FieldType: volcengine.String("string"),
          },
          {
             FieldName: volcengine.String("content"),
             FieldType: volcengine.String("text"),
          },
          {
             FieldName:    volcengine.String("f_int64"),
             FieldType:    volcengine.String("int64"),
             DefaultValue: 123456,
          },
       },
       Vectorize: &vikingdb.VectorizeForCreateVikingdbCollectionInput{
          Dense: &vikingdb.DenseForCreateVikingdbCollectionInput{
             ModelName: volcengine.String("bge-m3"),
             TextField: volcengine.String("content"),
          },
          Sparse: &vikingdb.SparseForCreateVikingdbCollectionInput{
             ModelName: volcengine.String("bge-m3"),
             TextField: volcengine.String("content"),
          },
       },
    }

    resp, err := svc.CreateVikingdbCollection(&input)
    if err != nil {
       panic(err)
    }

    fmt.Println(resp.Message)
    fmt.Println(resp.ResourceId)
}
```


<span id="create-a-collection-with-vector-field"></span>
### Create a collection with vector field

```Go
package main

import (
    "fmt"
    "os"

    "github.com/volcengine/volcengine-go-sdk/service/vikingdb"
    "github.com/volcengine/volcengine-go-sdk/volcengine"
    "github.com/volcengine/volcengine-go-sdk/volcengine/credentials"
    "github.com/volcengine/volcengine-go-sdk/volcengine/session"
)

func main() {
    var (
       accessKey = os.Getenv("VIKINGDB_AK")
       secretKey = os.Getenv("VIKINGDB_SK")
       region    = "ap-southeast-1"
    )
    config := volcengine.NewConfig().
       WithRegion(region).
       WithCredentials(credentials.NewStaticCredentials(accessKey, secretKey, ""))

    sess, err := session.NewSession(config)
    if err != nil {
       panic(err)
    }
    svc := vikingdb.New(sess)

    input := vikingdb.CreateVikingdbCollectionInput{
       CollectionName: volcengine.String("Your Collection Name"),
       Description:    volcengine.String("Your Collection Description"),
       ProjectName:    volcengine.String("default"),
       Fields: []*vikingdb.FieldForCreateVikingdbCollectionInput{
          {
             FieldName:    volcengine.String("item_id"),
             FieldType:    volcengine.String("int64"),
             IsPrimaryKey: volcengine.Bool(true),
          },
          {
             FieldName: volcengine.String("title"),
             FieldType: volcengine.String("string"),
          },
          {
             FieldName: volcengine.String("dense_vector"),
             FieldType: volcengine.String("vector"),
             Dim:       volcengine.Int32(768),
          },
          {
             FieldName: volcengine.String("sparse_vector"),
             FieldType: volcengine.String("sparse_vector"),
          },
          {
             FieldName:    volcengine.String("f_int64"),
             FieldType:    volcengine.String("int64"),
             DefaultValue: 123456,
          },
       },
    }

    resp, err := svc.CreateVikingdbCollection(&input)
    if err != nil {
       panic(err)
    }

    fmt.Println(resp.Message)
    fmt.Println(resp.ResourceId)
}
```
