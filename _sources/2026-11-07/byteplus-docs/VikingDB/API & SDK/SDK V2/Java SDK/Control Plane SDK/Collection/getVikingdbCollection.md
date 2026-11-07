---
title: "getVikingdbCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/getVikingdbCollection"
---

<span id="overview"></span>
# Overview

getVikingdbCollection is used to query detailed information about a specified Collection.

<span id="method-definition"></span>
# Method Definition

```Java
public GetVikingdbCollectionResponse getVikingdbCollection(GetVikingdbCollectionRequest body) throws ApiException
```


<span id="request-parameters"></span>
# **Request Parameters**


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|projectName |String |No |Project name |
|collectionName |String |Either this or resourceId is required |Specifies the name of the Collection to query.<br><br><br>* Can only contain English letters, numbers, and underscores _, must start with an English letter, and cannot be empty.<br><br>* Length requirement: [1, 128].<br><br>* Collection names must be unique. |
|resourceId |String | |Collection resource ID. Either resourceId or collectionName must be specified in the request. |


<span id="response-parameters"></span>
# Response Parameters

Calling the above method in Java returns a Collection instance. The properties contained in the Collection instance are shown in the table below.


|Parameter |Type |Description |
|---|---|---|
|projectName |String |Project name |
|resourceId |String |Resource ID |
|collectionName |String |Collection name |
|description |String |Collection description |
|enableKeywordsSearch |Boolean |Whether keyword search is supported |
|fields |List[FieldForGetVikingdbCollectionOutput] |Field list |
|vectorize |VectorizeForGetVikingdbCollectionOutput |Vectorization configuration |
|createTime |String |Creation time |
|updateTime |String |Update time |
|updatePerson |String |Updated by |
|collectionStats |CollectionStatsForGetVikingdbCollectionOutput |Statistics information |
|indexNames |List[String] |List of index names under the collection |
|indexCount |Integer |Number of indexes under the collection |



* List[FieldForGetVikingdbCollectionOutput]



|Parameter |Type |Description |
|---|---|---|
|fieldName |String |Field name |
|fieldType |String |Field type |
|dim |Integer |If the field type is vector, this parameter specifies the dimension of the dense vector |
|isPrimaryKey |Boolean |Whether it is a primary key field. One primary key field (string or int64 type) can be specified for the collection. If not specified, an auto\-generated primary key with field name "**AUTO_ID**" is used. |
|defaultValue |Object |Default value of field content |



* VectorizeForGetVikingdbCollectionOutput



|Parameter | |Type |Description |
|---|---|---|---|
|dense | |DenseForGetVikingdbCollectionOutput |Dense vectorization model configuration |
| |modelName |String |Model name |
| |modelVersion |String |Model version |
| |textField |String |Text vectorization field name |
| |imageField |String |Image vectorization field name |
| |dim |Integer |If dense vectors need to be generated, specify the vector dimension. The default dimension of the model is used by default. |
| |videoField |String |Video vectorization field name |
|sparse | |SparseForGetVikingdbCollectionOutput |Sparse vectorization configuration |
| |modelName |String |Model name |
| |modelVersion |String |Model version |
| |textField |String |Text vectorization field name |



* CollectionStatsForGetVikingdbCollectionOutput



|Parameter |Type |Description |
|---|---|---|
|dataCount |Long |Number of data entries |
|dataStorage |Long |Data storage (bytes) |


<span id="example"></span>
# Example

<span id="request-parameters"></span>
## Request Parameters

```Java
package org.example.newsubproduct.console.collection;

import com.volcengine.ApiClient;
import com.volcengine.ApiException;
import com.volcengine.sign.Credentials;
import com.volcengine.vikingdb.VikingdbApi;
import com.volcengine.vikingdb.model.*;

public class GetVikingdbCollection {
    public static void main(String[] args) {
        String ak = System.getenv("AK"); // ak
        String sk = System.getenv("SK"); // sk
        String endpoint = "vikingdb.ap-southeast-1.byteplusapi.com"; // Fill in the vector database control plane v2 domain https://www.volcengine.com/docs/84313/1792715
        String region = "ap-southeast-1"; // Service region

        ApiClient apiClient = new ApiClient()
                .setEndpoint(endpoint)
                .setCredentials(Credentials.getCredentials(ak, sk))
                .setRegion(region);

        VikingdbApi api = new VikingdbApi(apiClient);

        GetVikingdbCollectionRequest request = new GetVikingdbCollectionRequest()
                .collectionName("test_collection_for_sdk_with_vector");

        try {
            GetVikingdbCollectionResponse response = api.getVikingdbCollection(request);
            System.out.println("response body: " + response);
            System.out.println();
            System.out.println("response meta RequestId: " + response.getResponseMetadata().getRequestId());
            System.out.println("response meta Service: " + response.getResponseMetadata().getService());
            System.out.println("response meta Region: " + response.getResponseMetadata().getRegion());
            System.out.println("response meta Action: " + response.getResponseMetadata().getAction());
            System.out.println("response meta Version: " + response.getResponseMetadata().getVersion());
        } catch (ApiException e) {
            System.out.println("exception http code: " + e.getCode());
            System.out.println("exception response body: " + e.getResponseBody());
            System.out.println();
            System.out.println("exception RequestId: " + e.getResponseMetadata().getRequestId());
            System.out.println("exception Action: " + e.getResponseMetadata().getAction());
            System.out.println("exception Region: " + e.getResponseMetadata().getRegion());
            System.out.println("exception Service: " + e.getResponseMetadata().getService());
            System.out.println("exception Error.Code: " + e.getResponseMetadata().getError().getCode());
            System.out.println("exception Error.Message: " + e.getResponseMetadata().getError().getMessage());
        }
    }
}
```


 &nbsp;
