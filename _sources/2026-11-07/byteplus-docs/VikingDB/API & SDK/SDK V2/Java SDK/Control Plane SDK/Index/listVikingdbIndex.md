---
title: "listVikingdbIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/listVikingdbIndex"
---

<span id="overview"></span>
# Overview

listIndexes is used to query the list of Indexes associated with a Collection.

<span id="method-definition"></span>
# Method Definition

```Java
public ListVikingdbIndexResponse listVikingdbIndex(ListVikingdbIndexRequest body) throws ApiException
```


<span id="request-parameters"></span>
# **Request Parameters**


|Parameter |Type |Required |Description |
|---|---|---|---|
|pageNumber |Integer |No |Page number for pagination. Starts at 1. |
|pageSize |Integer |No |Page size for pagination. |
|filter |FilterForListVikingdbIndexInput |No |Filter conditions, as follows |



* FilterForListVikingdbIndexInput



|Parameter |Type |Description |
|---|---|---|
|collectionName |List[String] |Collection name |
|indexNameKeyword |String |Index name |
|status |List[String] |Status |


<span id="response-parameters"></span>
# Response Parameters

Java calls to execute the above task return a list of Index instances. The properties included in Index instances are shown in the table below.


|Parameter |Level 1 sub\-parameter |Level 2 sub\-parameter |Type |Description |
|---|---|---|---|---|
|indexes | | |List[IndexForListVikingdbIndexOutput] |Vector database index detail list |
| |collectionName | |String |Collection name |
| |projectName | |String |Project name |
| |resourceId | |String |Resource ID |
| |indexName | |String |Index name |
| |description | |String |Custom description of the index. |
| |vectorIndex | |VectorIndexForListVikingdbIndexOutput |Vector index configuration |
| | |indexType |IndexTypeEnum<br><br>Enum |Index type |
| | |distance |DistanceEnum<br><br>Enum |Distance type, algorithm for measuring distance between vectors. Possible values:<br><br>ip: Full name is Inner Product. This algorithm calculates similarity based on the inner product of vectors, which is the sum of products of corresponding elements. The larger the inner product value, the higher the similarity.<br><br>l2: Euclidean distance, which calculates the Euclidean space distance between two vectors. The smaller the Euclidean distance, the higher the similarity.<br><br>cosine: Cosine Similarity, also known as Cosine Distance. Used to calculate the cosine value of the angle between two high\-dimensional vectors to measure vector similarity. A smaller cosine value indicates a larger angle between the two vectors, meaning greater difference between them.<br><br>When distance=cosine, vectors are normalized by default.<br><br>When the indexing algorithm is IVF, available distance types are ip, cosine.<br><br>For hnsw_hybrid indexing algorithm, distance type selection only applies to dense vectors; sparse vectors only support inner product. |
| | |quant |QuantEnum<br><br>Enum |Quantization method. Quantization is the compression method for vectors in the index, which can reduce the complexity of similarity calculation between vectors. Based on the high\-dimensional and large\-scale characteristics of vectors, vector quantization can effectively reduce vector storage and computation costs. Possible values:<br><br><br>* int8: Compresses 4\-byte floats into a single byte to gain memory and computation latency benefits, causing minor precision loss—for example, cosine distance may yield scores greater than 1.<br><br>* float: Full precision, no compression quantization.<br><br>* fix16: Compresses 4\-byte floats into two bytes to gain memory and computation latency benefits, causing minor precision loss. By sacrificing some retrieval accuracy, it improves retrieval performance and reduces resource costs.<br><br>* pq: Converts high\-dimensional vectors into low\-dimensional codebook vectors to reduce memory usage and enhance search efficiency.<br><br><br>int8 supports hnsw, hnsw_hybrid, flat indexing algorithms with distance methods ip, cosine.<br><br>float supports hnsw, hnsw_hybrid, flat, diskann indexing algorithms with distance methods ip, l2, cosine.<br><br>fix16 supports hnsw, hnsw_hybrid, flat indexing algorithms with distance methods ip, l2, cosine.<br><br>pq supports diskann, ivf indexing algorithms with distance methods ip, l2, cosine. |
| | |hnswM |Integer |hnsw index parameter, indicating the number of neighbor nodes.<br><br><br>* Configurable when index_type is set to hnsw and hnsw_hybrid. |
| | |hnswCef |Integer |hnsw index parameter, indicating the search breadth for neighbor nodes during graph construction.<br><br><br>* Configurable when index_type is set to hnsw and hnsw_hybrid. |
| | |hnswSef |Integer |hnsw index parameter, indicating the search breadth for online retrieval.<br><br><br>* Configurable when index_type is set to hnsw and hnsw_hybrid. |
| | |diskannM |Integer |diskann parameter, indicating the number of neighbor nodes.<br><br><br>* Configurable when index_type is set to diskann. |
| | |diskannCef |Integer |diskann parameter, indicating the search breadth for neighbor nodes during graph construction.<br><br><br>* Configurable when index_type is set to diskann. |
| | |pqCodeRatio |Float |diskann parameter, size limit for vector dimension encoding. The larger the value, the higher the recall rate, but memory usage increases. Range (0.0, 0.25].<br><br><br>* Configurable when index_type is set to diskann. |
| | |cacheRatio |Float |diskann parameter, ratio of cached nodes to original data. Larger values improve index performance and increase memory usage. Range [0.0, 0.3).<br><br><br>* Configurable when index_type is set to diskann. |
| |scalarIndex | |List[ScalarIndexForListVikingdbIndexOutput] |List of scalar fields |
| |cpuQuota | |Integer |CPU quota consumed by index retrieval. |
| |shardPolicy | |String |Index sharding type: auto for automatic sharding, custom for custom sharding. |
| |shardCount | |Integer |Number of index shards |
| |actualCU | |Integer |Actual CU usage |
|pageSize | | |Integer |PageSize value from the request, or the default value if not specified in the request. |
|pageNumber | | |Integer |PageNumber value from the request, or the default value if not specified in the request. |
|totalCount | | |Integer |Total number of query results |


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

import java.util.Arrays;
import java.util.Collections;

public class ListVikingdbIndex {
    public static void main(String[] args) {
        String ak = System.getenv("AK"); // ak
        String sk = System.getenv("SK"); // sk
        String endpoint = "vikingdb.ap-southeast-1.byteplusapi.com"; // Fill in the vector database control plane v2 domain name https://www.volcengine.com/docs/84313/1792715
        String region = "ap-southeast-1"; // Service region

        ApiClient apiClient = new ApiClient()
                .setEndpoint(endpoint)
                .setCredentials(Credentials.getCredentials(ak, sk))
                .setRegion(region);

        VikingdbApi api = new VikingdbApi(apiClient);

        ListVikingdbIndexRequest request = new ListVikingdbIndexRequest()
                .filter(new FilterForListVikingdbIndexInput()
                        .collectionName(Arrays.asList("test_collection_for_sdk_with_vector", "test_collection_for_sdk_with_vectorize"))
                        .indexNameKeyword("idx")
                        .status(Collections.singletonList("ready"))
                );

        try {
            ListVikingdbIndexResponse response = api.listVikingdbIndex(request);
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
