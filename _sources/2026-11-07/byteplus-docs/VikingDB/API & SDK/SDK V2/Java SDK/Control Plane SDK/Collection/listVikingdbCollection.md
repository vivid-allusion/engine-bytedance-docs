---
title: "listVikingdbCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/listVikingdbCollection"
---

<span id="overview"></span>
# Overview

listVikingdbCollection is used to query the Collection list.

<span id="method-definition"></span>
# Method Definition

```Java
public ListVikingdbCollectionResponse listVikingdbCollection(ListVikingdbCollectionRequest body) throws ApiException
```


<span id="request-parameters"></span>
# **Request Parameters**


|Parameter |Type |
|---|---|
|projectName |String |
|pageSize |Integer |
|pageNumber |Integer |
|filter |FilterForListVikingdbCollectionInput |



* FilterForListVikingdbCollectionInput parameter structure



|Parameter |Type |Required |Description |
|---|---|---|---|
|fieldName |String |Yes |Field name.<br><br>Restrictions: English letters, digits, or underscores. Must start with an English letter. Length must not exceed 64 bytes. |
|fieldType |FieldTypeEnum（enumeration type） |Yes |Field type.<br><br>Enumeration values include:<br><br>vector,sparse_vector,string,int64,float32,bool,list[string],list[int64],text,image,video |
|defaultValue |Object |No |Default value for field content.<br><br>Note: Fields of type vector/sparse_vector/text/image/video do not support default values. |
|dim |Integer |No |If the field type is vector, this parameter specifies the dimension of the dense vector. Supports values from 4 to 4096 and must be an integer multiple of 4. |
|isPrimaryKey |Boolean |No |Whether it is a primary key field. One primary key field (string or int64 type) can be specified for the dataset. If not specified, an automatically generated primary key is used with the field name "AUTO_ID". |


<span id="response-parameters"></span>
# Response Parameters

Java calls to execute the above task return a list of Collection instances. The properties included in Collection instances are shown in the table below.


|Parameter |Level 1 Parameter |Level 2 Parameter |Level 3 Parameter |Type |Description |
|---|---|---|---|---|---|
|totalCount | | | |Integer |Total number of query results |
|pageSize | | | |Integer |PageSize value from the request; if not specified in the request, it uses the default value. |
|pageNumber | | | |Integer |PageNumber value from the request; if not specified in the request, it uses the default value. |
|collections | | | |List[CollectionForListVikingdbCollectionOutput] |Vector database dataset list |
| |collectionName | | |String |Dataset name |
| |resourceId | | |String |Resource ID |
| |projectName | | |String |Project name |
| |vectorize | | |VectorizeForListVikingdbCollectionOutput |Vectorization configuration |
| | |dense | |DenseForListVikingdbCollectionOutput |Dense vectorization model configuration |
| | | |modelName |String |Model name |
| | | |modelVersion |String |Model version |
| | | |textField |String |Text vectorization field name |
| | | |imageField |String |Image vectorization field name |
| | | |dim |Integer |If dense vectors need to be generated, specify the vector dimension. The default uses the model's default dimension. |
| | | |videoField |String |Video vectorization field name |
| | |sparse | |SparseForListVikingdbCollectionOutput |Sparse vectorization configuration |
| | | |modelName |String |Model name |
| | | |modelVersion |String |Model version |
| | | |textField |String |Text vectorization field name |
| |tags | | |List[TagForListVikingdbCollectionOutput] |Tags |
| | |key | |String |Tag key |
| | |value | |String |Tag value |
| |description | | |String |Dataset description |
| |fields | | |List[FieldForListVikingdbCollectionOutput] |Field list |
| | |fieldName | |String |Field name |
| | |fieldType | |String |Field type |
| | |dim | |Integer |If the field type is vector, this parameter specifies the dimension of the dense vector |
| | |isPrimaryKey | |Boolean |Whether it is a primary key field. One primary key field (string or int64 type) can be specified for the dataset. If not specified, an automatically generated primary key is used with the field name "**AUTO_ID**". |
| | |defaultValue | |Object |Default value for field content |
| |createTime | | |String |Creation time |
| |updateTime | | |String |Update time |
| |updatePerson | | |String |Updated by |
| |collectionStats | | |CollectionStatsForListVikingdbCollectionOutput |Statistics |
| | |dataCount | |Long |Number of data entries |
| | |dataStorage | |Long |Data storage size (bytes) |
| |enableKeywordsSearch | | |Boolean |Whether keyword search is supported |
| |indexNames | | |Array of String |List of index names under the dataset |
| |indexCount | | |Integer |Number of indexes under the dataset |


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

public class ListVikingdbCollection {
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

        ListVikingdbCollectionRequest request = new ListVikingdbCollectionRequest()
                .filter(new FilterForListVikingdbCollectionInput().collectionNameKeyword("collection_for_sdk"));

        try {
            ListVikingdbCollectionResponse response = api.listVikingdbCollection(request);
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
