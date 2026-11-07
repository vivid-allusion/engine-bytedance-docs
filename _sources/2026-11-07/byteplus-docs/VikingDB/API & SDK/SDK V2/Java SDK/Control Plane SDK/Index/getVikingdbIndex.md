---
title: "getVikingdbIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/getVikingdbIndex"
---

<span id="overview"></span>
# Overview

getVikingdbIndex is used to query index details.

<span id="method-definition"></span>
# Method Definition

```Java
public GetVikingdbIndexResponse getVikingdbIndex(GetVikingdbIndexRequest body) throws ApiException
```


<span id="request-parameters"></span>
# **Request Parameters**


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|projectName |String |No |Project name |
|collectionName |String |One of two required |Dataset name |
|resourceId |String | |Dataset resource ID. The request must specify either resourceId or collectionName. |
|indexName |String |Yes |Specifies the Index name to query.<br><br><br>* Can only use English letters, numbers, underscores _, and must start with an English letter, cannot be empty.<br><br>* Length requirement: [1, 128].<br><br>* Index names cannot be duplicated. |


<span id="response-parameters"></span>
# Response Parameters

After Java executes the above method, it returns an Index instance. The properties contained in the Index instance are shown in the table below.


|Parameter |First\-level sub\-parameter |Type |Description |
|---|---|---|---|
|collectionName | |String |Dataset name |
|projectName | |String |Project name |
|resourceId | |String |Resource ID |
|indexName | |String |Index name |
|cpuQuota | |Integer |CPU quota consumed by index retrieval. |
|shardPolicy | |String |Index sharding type, auto for automatic sharding, custom for custom sharding. |
|shardCount | |Integer |Index shard count |
|description | |String |Index description |
|vectorIndex | |VectorIndexForGetVikingdbIndexOutput |Vector index configuration |
| |indexType |IndexTypeEnum<br><br>Enum |Index type |
| |distance |DistanceEnum<br><br>Enum |Distance type, the algorithm for measuring distance between vectors. Values are as follows:<br><br>ip: Full name is Inner Product, inner product. This algorithm calculates similarity based on the inner product of vectors, which is the sum of products of corresponding elements of two vectors. The larger the inner product value, the higher the similarity.<br><br>l2: Euclidean distance, which calculates the Euclidean space distance between two vectors. The smaller the Euclidean distance, the higher the similarity.<br><br>cosine: Cosine Similarity, also known as Cosine Distance, used to calculate the cosine value of the angle between two high\-dimensional vectors to measure vector similarity. The smaller the cosine value, the larger the angle between the two vectors, meaning the greater the difference between the two vectors.<br><br>When distance=cosine, vectors are normalized by default.<br><br>When IVF is selected as the index algorithm, distance types ip and cosine are available.<br><br>For hnsw_hybrid index algorithm, distance type selection only takes effect for dense vectors, sparse vectors only support inner product. |
| |quant |QuantEnum<br><br>Enum |Quantization method. Quantization method is the compression method for vectors in the index, which can reduce the complexity of similarity calculation between vectors. Based on the high\-dimensional and large\-scale characteristics of vectors, vector quantization can effectively reduce vector storage and computation costs. Values are as follows:<br><br><br>* int8: Compresses 4\-byte float into a single byte to gain memory and computation latency benefits, causing minor precision loss, for example, cosine distance may have scores greater than 1.<br><br>* float: Full precision, no compression quantization.<br><br>* fix16: Compresses 4\-byte float into two bytes to gain memory and computation latency benefits, causing minor precision loss. Improves retrieval performance and saves resource costs by sacrificing some retrieval precision.<br><br>* pq: Converts high\-dimensional vectors into low\-dimensional codebook vectors to reduce memory usage and improve search efficiency.<br><br><br>int8 applies to hnsw, hnsw_hybrid, flat index algorithms, with distance methods ip and cosine.<br><br>float applies to hnsw, hnsw_hybrid, flat, diskann index algorithms, with distance methods ip, l2, and cosine.<br><br>fix16 applies to hnsw, hnsw_hybrid, flat index algorithms, with distance methods ip, l2, and cosine.<br><br>pq applies to diskann, ivf index algorithms, with distance methods ip, l2, and cosine. |
| |hnswM |Integer |hnsw index parameter, representing the number of neighbor nodes.<br><br><br>* Optional configuration when index_type is configured as hnsw and hnsw_hybrid. |
| |hnswCef |Integer |hnsw index parameter, representing the breadth of searching neighbor nodes when building the graph.<br><br><br>* Optional configuration when index_type is configured as hnsw and hnsw_hybrid. |
| |hnswSef |Integer |hnsw index parameter, representing the search breadth for online retrieval.<br><br><br>* Optional configuration when index_type is configured as hnsw and hnsw_hybrid. |
| |diskannM |Integer |diskann parameter, representing the number of neighbor nodes.<br><br><br>* Optional configuration when index_type is configured as diskann. |
| |diskannCef |Integer |diskann parameter, representing the breadth of searching neighbor nodes when building the graph.<br><br><br>* Optional configuration when index_type is configured as diskann. |
| |pqCodeRatio |Float |diskann parameter, size limit for vector dimension encoding. The larger the value, the higher the recall rate, but it will increase memory usage, range (0.0, 0.25].<br><br><br>* Optional configuration when index_type is configured as diskann. |
| |cacheRatio |Float |diskann parameter, ratio of cache nodes to original data. A larger value will improve index performance and increase memory usage. Range [0.0, 0.3).<br><br><br>* Optional configuration when index_type is configured as diskann. |
|scalarIndex | |List[ScalarIndexForGetVikingdbIndexOutput] |Scalar field list<br><br>`JSON <br> "ScalarIndex": [ <br> { <br> "FieldName": "f_int64_1", #string <br> "FieldType": "int64", #string <br> "DefaultValue": 0 #any <br> }, <br>` |
| |defaultValue |Object | |
| |dim |Integer | |
| |fieldName |String | |
|actualCU | |Integer |Actual CU usage |


<span id="example"></span>
# Example

<span id="request-parameters"></span>
## Request Parameters

```Java
package org.example.newsubproduct.console.index;

import com.volcengine.ApiClient;
import com.volcengine.ApiException;
import com.volcengine.sign.Credentials;
import com.volcengine.vikingdb.VikingdbApi;
import com.volcengine.vikingdb.model.*;

public class GetVikingdbIndex {
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

        GetVikingdbIndexRequest request = new GetVikingdbIndexRequest()
                .collectionName("test_collection_for_sdk_with_vector")
                .indexName("idx_simple");

        try {
            GetVikingdbIndexResponse response = api.getVikingdbIndex(request);
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
