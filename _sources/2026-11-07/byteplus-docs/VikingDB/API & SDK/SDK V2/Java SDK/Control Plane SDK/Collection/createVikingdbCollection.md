---
title: "createVikingdbCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/createVikingdbCollection"
---

<span id="overview"></span>
# Overview

This interface is used to create collections for the vector database. A single account can create up to 200 collections.


* Each Collection must specify a primary key field.

* After adding a field of vector type to the defined fields, vector type cannot be selected when adding new fields. Currently only single vector is supported, and multiple vector fields cannot be added.

* When creating a collection, please clarify the configuration method based on data type: if you have existing vector data, fill in the vector field; if you need to vectorize multimodal data (such as text and images), configure the vectorize parameter. These two are different data processing logics, and only one can be selected during creation; they cannot be used simultaneously.

* The maximum number of fields in a Collection is 200.


<span id="method-definition"></span>
# Method Definition

```Java
public CreateVikingdbCollectionResponse createVikingdbCollection(CreateVikingdbCollectionRequest body) throws ApiException
```


<span id="request-parameters"></span>
# **Request Parameters**

The table below only lists the request parameters specific to this interface and some common parameters. For more information, see [Common Parameters](https://www.volcengine.com/docs/6369/67268).


|Parameter |Type |Required |Description |
|---|---|---|---|
|projectName |String |No |Project name. Corresponds to the "project" concept in Volcano Engine. If not filled, it defaults to "default". |
|collectionName |String |Yes |Collection name, corresponding to API field `CollectionName`<br><br><br>* Can only use English letters, numbers, underscores, and must start with an English letter; cannot be empty<br><br>* Length (bytes) requirement: [1, 128]<br><br>* All Collection names under the same account must be unique<br><br>* The number of collections under the same account cannot exceed 200 |
|description |String |No |Collection description<br><br>Maximum 65535 bytes |
|fields |List[FieldForCreateVikingdbCollectionInput] |Yes |Fields in the collection.<br><br>Limit: maximum 200 fields per collection. |
|vectorize |VectorizeForCreateVikingdbCollectionInput |No |Vectorization configuration for the collection. |



* FieldForCreateVikingdbCollectionInput parameter structure



|Parameter |Type |Required |Description |
|---|---|---|---|
|fieldName |String |Yes |Field name.<br><br>Limit: English letters, numbers, or underscores. Must start with an English letter. Length must not exceed 64 bytes. |
|fieldType |FieldTypeEnum (Enumeration) |Yes |Field type. |
|defaultValue |Object |No |Default value for field content.<br><br>Note: vector/sparse_vector/text/image/video type fields do not support default values. |
|dim |Integer |No |If the field type is vector, this parameter specifies the dimension of the dense vector. Supports 4\-4096 and must be an integer multiple of 4. |
|isPrimaryKey |Boolean |No |Whether it is a primary key field. One primary key field (string or int64 type) can be specified for the collection. If not specified, an auto\-generated primary key will be used with the field name "**AUTO_ID**". |



* VectorizeForCreateVikingdbCollectionInput parameter structure



|Parameter |Type |Required |Description |
|---|---|---|---|
|dense |DenseForCreateVikingdbCollectionInput |Yes |Dense vectorization model configuration |
|sparse |SparseForCreateVikingdbCollectionInput |No |Sparse vectorization model configuration |



* DenseForCreateVikingdbCollectionInput and SparseForCreateVikingdbCollectionInput parameter structure



|Parameter |Type |Required |Description |
|---|---|---|---|
|modelName |ModelNameEnum (Enumeration) |Yes |Model name.<br><br>See the embedding model list for enumerated values. |
|modelVersion |String |No |Model version. Required for doubao series models. For bge series models, defaults to "default". |
|dim |Integer |No |Dense vector dimension. See the embedding model list for dimensions supported by each model. |
|textField |String |No |Text vectorization field name. |
|imageField |String |No |Image vectorization field name. |
|videoField |String |No |Video vectorization field name. |


<span id="field-type-field-type"></span>
# field_type (Field Type)


|Field Type |Format |Can be Primary Key |Description |
|---|---|---|---|
|int64 |Integer value |Yes |Integer<br><br><br>* When used as a primary key, must not be 0 |
|float32 |Floating point value |No |Floating point number |
|string |String |Yes |String<br><br><br>* Recommended usage: when used for enumeration value filtering, recommended length does not exceed 128 bytes<br><br>* Hard limit: must not exceed 65535 bytes; when used as a primary key, length must not exceed 256 bytes |
|bool |true/false |No |Boolean type |
|list[string] |String array |No |String array<br><br><br>* Recommended usage: when used for enumeration value filtering, list length does not exceed 32, single element does not exceed 1024 bytes<br><br>* Hard limit: list length does not exceed 20000, single element does not exceed 1024 bytes, total size does not exceed 1MB |
|list[int64] |Integer array |No |Integer array<br><br><br>* Hard limit: list length does not exceed 1024 |
|vector |* Vector (floating point array)<br><br>* Base64 encoding after float32/float64 compression to bytes |No |Dense vector<br><br><br>* Hard limit: length not less than 4, not greater than 4096, and must be an integer multiple of 4. |
|sparse_vector |Dictionary list of input format <token_id, token_weight\>, representing the non\-zero position indices and corresponding values of sparse vector, where token_id is string type and token_weight is float type |No |Sparse vector |
|text |String |No |If it is a vectorization field, the value cannot be empty. (Otherwise, it can be empty)<br><br><br>* If it is a vectorization field, the value cannot be empty. (Otherwise, it can be empty)<br><br>* Hard limit: must be less than 65535 bytes |
|image |String |No |If it is a vectorization field, the value cannot be empty. (Otherwise, it can be empty)<br><br><br>* Image tos link `tos://{bucket}/{object}`<br><br>* http/https format link<br><br>* Corresponding image must have width and height greater than 14px, pixels less than 36 million<br><br>* See: [Multimodal Vectorization](https://www.volcengine.com/docs/82379/1409291?lang=zh#a256838b) |
|video |Object |No |If it is a vectorization field, the value cannot be empty. (Otherwise, it can be empty)<br><br><br>* Video tos link `tos://{bucket}/{object}`<br><br>* http/https format url link<br><br>* Corresponding video must not exceed 50mb in size<br><br>* See: [Multimodal Vectorization](https://www.volcengine.com/docs/82379/1409291?lang=zh#a256838b)<br><br><br>`Plain <br> { <br> "value": "tos://{bucket}/{object}" # or http/https format url link, this field is required <br> "fps": 0.2 # Value 0.2-5, optional <br> } <br>` |
|date_time |string |No |Minute level:<br><br>`yyyy-MM-ddTHH:mmZ` or `yyyy-MM-ddTHH:mm±HH:mm`<br><br>Second level:<br><br>`yyyy-MM-ddTHH:mm:ssZ` or `yyyy-MM-ddTHH:mm:ss±HH:mm`<br><br>Millisecond level:<br><br>`yyyy-MM-ddTHH:mm:ss.SSSZ` or `yyyy-MM-ddTHH:mm:ss.SSS±HH:mm`<br><br>For example: "2025\-08\-12T11:33:56+08:00" |
|geo_point |string |No |Geographic coordinates `longitude,latitude`, where `longitude` value is (\-180,180), `latitude` value is (\-90,90)<br><br>For example: "116.408108,39.915023" |


<span id="model-list"></span>
## Model List


|Model Name |Model Version |Supported Vectorization Type |Default Dense Vector Dimension |Optional Dense Vector Dimension |Text Truncation Length |Supports Sparse Vector |Supports Instruction |
|---|---|---|---|---|---|---|---|
|bge\-large\-zh |(default) |text |1024 |1024 |512 |No |Yes |
|bge\-m3 |(default) |text |1024 |1024 |8192 |Yes |No |
|bge\-visualized\-m3 |(default) |text、image and combinations |1024 |1024 |8192 |No |No |
|Skylark\-embedding |*240715* |text |2048 |512, 1024, 2048 |4096 |No |Yes |
|Skylark\-embedding\-vision |*250615* |Compatible with *241215* usage. Additionally, supports full_modal_seq (text/image/video sequence) |2048 |2048, 1024 |128k |No |Yes |


<span id="response-parameters"></span>
# **Response Parameters**

The table below only lists the response parameters specific to this interface. For more information, see [Response Structure](https://www.volcengine.com/docs/6369/80336).


|Parameter |Type |Description |
|---|---|---|
|message |String |Message about request status. |
|resourceId |String |ID of the new collection. |


<span id="request-example"></span>
# Request Example

<span id="create-collection-with-vector-field"></span>
### Create collection with vector field

```Java
import com.volcengine.ApiClient;
import com.volcengine.ApiException;
import com.volcengine.sign.Credentials;
import com.volcengine.vikingdb.VikingdbApi;
import com.volcengine.vikingdb.model.*;
import java.util.Arrays;

public class TestCreateVikingdbCollectionWithVector {
    public static void main(String[] args) {
        String ak = System.getenv("AK"); // input your ak
        String sk = System.getenv("SK"); // input your sk
        String endpoint = "vikingdb.ap-southeast-1.byteplusapi.com"; // Fill in the vector database control plane v2 domain name https://www.volcengine.com/docs/84313/1792715
        String region = "ap-southeast-1"; // Service region

        ApiClient apiClient = new ApiClient()
                .setEndpoint(endpoint)
                .setCredentials(Credentials.getCredentials(ak, sk))
                .setRegion(region);

        VikingdbApi api = new VikingdbApi(apiClient);

        CreateVikingdbCollectionRequest request = new CreateVikingdbCollectionRequest()
                .collectionName("test_coll_for_java_sdk_with_vector")
                .description("this is a test collection of vikingdb")
                .fields(Arrays.asList(
                        new FieldForCreateVikingdbCollectionInput().fieldName("f_int64_id").fieldType(FieldForCreateVikingdbCollectionInput.FieldTypeEnum.INT64).isPrimaryKey(true), // Primary key field
                        new FieldForCreateVikingdbCollectionInput().fieldName("f_string_1").fieldType(FieldForCreateVikingdbCollectionInput.FieldTypeEnum.STRING),
                        new FieldForCreateVikingdbCollectionInput().fieldName("f_int64_1").fieldType(FieldForCreateVikingdbCollectionInput.FieldTypeEnum.INT64),
                        new FieldForCreateVikingdbCollectionInput().fieldName("f_float_1").fieldType(FieldForCreateVikingdbCollectionInput.FieldTypeEnum.FLOAT32),
                        new FieldForCreateVikingdbCollectionInput().fieldName("f_list_string_1").fieldType(FieldForCreateVikingdbCollectionInput.FieldTypeEnum.LIST_STRING_),
                        new FieldForCreateVikingdbCollectionInput().fieldName("f_vector").fieldType(FieldForCreateVikingdbCollectionInput.FieldTypeEnum.VECTOR).dim(4), // Dense vector field, and set dimension
                        new FieldForCreateVikingdbCollectionInput().fieldName("f_sparse_vector").fieldType(FieldForCreateVikingdbCollectionInput.FieldTypeEnum.SPARSE_VECTOR) // Sparse vector field
                ));

        try {
            CreateVikingdbCollectionResponse response = api.createVikingdbCollection(request);
            System.out.println("all response content: " + response);
            System.out.println("response getResponseMetadata: " + response.getResponseMetadata());
            System.out.println("response getResponseMetadata: " + response.getResponseMetadata().getAction());
            System.out.println("response getMessage: " + response.getMessage());
            System.out.println("response getResourceId: " + response.getResourceId());

            System.out.println("response RequestId: " + response.getResponseMetadata().getRequestId());
            System.out.println("response Action: " + response.getResponseMetadata().getAction());
            System.out.println("response Region: " + response.getResponseMetadata().getRegion());
            System.out.println("response Service: " + response.getResponseMetadata().getService());
        } catch (ApiException e) {
            System.out.println("exception http code: " + e.getCode());
            System.out.println("exception RequestId: " + e.getResponseMetadata().getRequestId());
            System.out.println("exception Action: " + e.getResponseMetadata().getAction());
            System.out.println("exception Region: " + e.getResponseMetadata().getRegion());
            System.out.println("exception Service: " + e.getResponseMetadata().getService());
            System.out.println("exception Error.Code: " + e.getResponseMetadata().getError().getCode());
            System.out.println("exception Error.Message: " + e.getResponseMetadata().getError().getMessage());
            System.out.println("exception http response body: " + e.getResponseBody());
        }
    }
}
```


<span id="create-collection-with-vectorize"></span>
### Create collection with vectorize

```Java
import com.volcengine.ApiClient;
import com.volcengine.ApiException;
import com.volcengine.sign.Credentials;

import com.volcengine.vikingdb.VikingdbApi;
import com.volcengine.vikingdb.model.*;

import java.util.Arrays;

public class TestCreateVikingdbCollectionWithVectorize {
    public static void main(String[] args) {
        String ak = System.getenv("AK"); // input your ak
        String sk = System.getenv("SK"); // input your sk
        String endpoint = "vikingdb.ap-southeast-1.byteplusapi.com"; // Fill in the vector database control plane v2 domain name https://www.volcengine.com/docs/84313/1792715
        String region = "ap-southeast-1"; // Service region

        ApiClient apiClient = new ApiClient()
                .setEndpoint(endpoint)
                .setCredentials(Credentials.getCredentials(ak, sk))
                .setRegion(region);

        VikingdbApi api = new VikingdbApi(apiClient);

        CreateVikingdbCollectionRequest request = new CreateVikingdbCollectionRequest()
                .collectionName("test_coll_for_java_sdk_with_vectorize")
                .description("this is a test collection of vikingdb")
                .fields(Arrays.asList(
                        new FieldForCreateVikingdbCollectionInput().fieldName("f_int64_id").fieldType(FieldForCreateVikingdbCollectionInput.FieldTypeEnum.INT64).isPrimaryKey(true), // Primary key field
                        new FieldForCreateVikingdbCollectionInput().fieldName("f_string_1").fieldType(FieldForCreateVikingdbCollectionInput.FieldTypeEnum.STRING),
                        new FieldForCreateVikingdbCollectionInput().fieldName("f_int64_1").fieldType(FieldForCreateVikingdbCollectionInput.FieldTypeEnum.INT64),
                        new FieldForCreateVikingdbCollectionInput().fieldName("f_float_1").fieldType(FieldForCreateVikingdbCollectionInput.FieldTypeEnum.FLOAT32),
                        new FieldForCreateVikingdbCollectionInput().fieldName("f_list_string_1").fieldType(FieldForCreateVikingdbCollectionInput.FieldTypeEnum.LIST_STRING_),
                        new FieldForCreateVikingdbCollectionInput().fieldName("f_text_1").fieldType(FieldForCreateVikingdbCollectionInput.FieldTypeEnum.TEXT),
                        new FieldForCreateVikingdbCollectionInput().fieldName("f_image_1").fieldType(FieldForCreateVikingdbCollectionInput.FieldTypeEnum.IMAGE)
                ))
                .vectorize(new VectorizeForCreateVikingdbCollectionInput()
                        .dense(new DenseForCreateVikingdbCollectionInput()
                                .modelName(DenseForCreateVikingdbCollectionInput.ModelNameEnum.DOUBAO_EMBEDDING_VISION)
                                .modelVersion("250615")
                                .dim(1024)
                                .textField("f_text_1")
                                .imageField("f_image_1")
                        )
                        .sparse(new SparseForCreateVikingdbCollectionInput()
                                .modelName(SparseForCreateVikingdbCollectionInput.ModelNameEnum.BGE_M3)
                                .modelVersion("default")
                                .textField("f_text_1")
                        )
                );

        try {
            CreateVikingdbCollectionResponse response = api.createVikingdbCollection(request);
            System.out.println("all response content: " + response);
            System.out.println("response getMessage: " + response.getMessage());
            System.out.println("response getResourceId: " + response.getResourceId());

            System.out.println("response RequestId: " + response.getResponseMetadata().getRequestId());
            System.out.println("response Action: " + response.getResponseMetadata().getAction());
            System.out.println("response Region: " + response.getResponseMetadata().getRegion());
            System.out.println("response Service: " + response.getResponseMetadata().getService());
        } catch (ApiException e) {
            System.out.println("exception http code: " + e.getCode());
            System.out.println("exception RequestId: " + e.getResponseMetadata().getRequestId());
            System.out.println("exception Action: " + e.getResponseMetadata().getAction());
            System.out.println("exception Region: " + e.getResponseMetadata().getRegion());
            System.out.println("exception Service: " + e.getResponseMetadata().getService());
            System.out.println("exception Error.Code: " + e.getResponseMetadata().getError().getCode());
            System.out.println("exception Error.Message: " + e.getResponseMetadata().getError().getMessage());
            System.out.println("exception http response body: " + e.getResponseBody());
        }
    }
}
```
