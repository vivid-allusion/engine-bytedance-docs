---
title: "createVikingdbIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/createVikingdbIndex"
---

The price calculator can output three types of core estimation results based on your data and index configuration: computing resource (CU) usage, storage resource (disk capacity, unit: GB), and corresponding cost details.

Usage link: https://console.volcengine.com/vikingdb/region:vikingdb+cn\-beijing/bohr/price\-calculator

<span id="overview"></span>
# Overview

createVikingdbIndex is used to create an Index for a specified Collection.

Creating an index can accelerate vector similarity search. It groups and sorts the raw data in the vector database according to the specified index algorithm and data structure, improving the efficiency and accuracy of similarity search. It is the core mechanism that enables the vector database to filter out candidates in a short time.

When the dataset for the index only contains dense vectors (i.e., vector type fields), we call this type of index a pure dense index; when the dataset for the index contains both dense vectors and sparse vectors (vector and sparse_vector type fields), we call this type of index a hybrid index.

<span id="method-definition"></span>
# Method Definition

```Java
public CreateVikingdbIndexResponse createVikingdbIndex(CreateVikingdbIndexRequest body) throws ApiException
```


<span id="request-parameters"></span>
# **Request Parameters**

The request parameter is CreateVikingdbIndexRequest. The parameters included in the CreateVikingdbIndexRequest class are shown in the table below.


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|projectName |String |No |Project name |
|collectionName |String |Either one is required |Dataset name |
|resourceId |String | |Dataset resource ID. The request must specify either resourceId or collectionName. |
|indexName |String |Yes |Specifies the name of the Index to create.<br><br><br>* Can only use English letters, numbers, underscores _, and must start with an English letter, cannot be empty.<br><br>* Length requirement: [1, 128].<br><br>* Index names cannot be duplicated.<br><br>* Under the same account, the number of Indexes cannot exceed 200. |
|description |String |No |Custom description of the index. |
|scalarIndex |List[String] |No |List of scalar fields, used to set fields that need to be built into the scalar index. |
|shardPolicy |ShardPolicyEnum |No |Index sharding type<br><br><br>* Optional values are ShardPolicyEnum.Auto/ShardPolicyEnum.Custom. Auto means automatic sharding, Custom means custom sharding. |
|shardCount |Integer |No |Custom shard count. |
|cpuQuota |Integer |No |CPU quota consumed by index retrieval, format is a positive integer. |
|vectorIndex |VectorIndexForCreateVikingdbIndexInput |Yes |See below |



* VectorIndexForCreateVikingdbIndexInput



|**Parameter** |**Type** |**Required** |**Default Value** |**Description** |
|---|---|---|---|---|
|indexType |IndexTypeEnum<br><br>Enumeration |Yes |IndexType.HNSW |Vector index type. Possible values are:<br><br><br>* IndexType.HNSW: Full name is Hierarchical Navigable Small World, a data structure and algorithm for ANN search in high\-dimensional space, based on graph indexing. HNSW reduces the number of nodes that need to be accessed during search by building a multi\-layer network, enabling fast and efficient nearest neighbor search, suitable for scenarios with high search efficiency requirements.<br><br>* IndexType.HNSW_HYBRID: HNSW algorithm supporting hybrid indexes. The hybrid index algorithm can index both dense vectors and sparse vectors in the dataset simultaneously, and return results that consider both types of similarity during retrieval. Suitable for scenarios with high search efficiency requirements and the need to retrieve both sparse and dense vectors simultaneously.<br><br>   The dataset for HNSW_HYBRID index must contain sparse_vector type data, i.e., define sparse_vector type fields, or bind a pipeline that can generate sparse_vector type vectors.<br><br>* IndexType.FLAT: Brute\-force index, which traverses all vectors in the entire vector database during search to perform distance calculation and comparison with the target vector. The query speed is slow, but flat can provide 100% retrieval recall rate, suitable for scenarios with few vector candidate sets and requiring 100% retrieval recall rate.<br><br>* IndexType.IVF: Inverted index, using the idea of inversion to store vectors under each cluster center. Each time a vector is queried, the nearest few centers are found, and the vectors under these centers are searched respectively. The speed is fast but the accuracy is slightly lower, suitable for medium\-scale data volume with high search efficiency requirements and secondary priority on accuracy.<br><br>* IndexType.DISKANN: Disk index algorithm based on Vamana graph, combining Vamana graph with PQ quantization compression scheme to construct DiskANN index. The graph index and raw data are stored in SSD, and the compressed index is placed in memory. During retrieval requests, the query vector is compared with cluster centers, and then the corresponding raw data is read from disk for scoring. Suitable for scenarios with large\-scale data volume, not particularly sensitive to performance, lower memory cost, and high recall rate requirements. |
|distance |DistanceEnum Enumeration |No |DistanceType.IP |Distance type, algorithm for measuring the distance between vectors. Possible values are:<br><br><br>* DistanceType.IP: Full name is Inner Product, which calculates similarity based on the inner product of vectors, i.e., the result of multiplying and summing corresponding elements of two vectors. The larger the inner product value, the higher the similarity.<br><br>* DistanceType.L2: Euclidean distance, which calculates the Euclidean space distance between two vectors. The smaller the Euclidean distance, the higher the similarity.<br><br>* DistanceType.COSINE: Cosine Similarity, also known as Cosine Distance, used to calculate the cosine value of the angle between two high\-dimensional vectors to measure vector similarity. A smaller cosine value indicates a larger angle between the two vectors, meaning greater difference between the two vectors.<br><br>   When distance=DistanceType.COSINE, vectors are normalized by default.<br><br><br>For hnsw_hybrid index algorithm, distance type selection only applies to dense vectors; sparse vectors only support inner product. |
|quant |QuantEnum Enumeration |No |QuantType.Int8 |Quantization method. The quantization method is the compression method for vectors in the index, which can reduce the complexity of similarity calculation between vectors. Based on the high\-dimensional and large\-scale characteristics of vectors, using vector quantization can effectively reduce vector storage and computing costs. Possible values are:<br><br><br>* QuantType.Int8: Compresses 4\-byte float into a single byte to gain memory and computing latency benefits, causing minor precision loss, e.g., cosine distance may have scores greater than 1.<br><br>* QuantType.Float: Full precision, no compression quantization.<br><br>* QuantType.Fix16: Compresses 4\-byte float into two bytes to gain memory and computing latency benefits, causing minor precision loss. By sacrificing some retrieval precision, it improves retrieval performance and saves resource costs.<br><br>* QuantType.PQ: Converts high\-dimensional vectors into low\-dimensional codebook vectors to reduce memory usage and improve search efficiency. |
|hnswM |Integer |No |20 |HNSW index parameter, indicating the number of neighbor nodes.<br><br><br>* Optional configuration when indexType is set to IndexType.HNSW. |
|hnswCef |Integer |No |400 |HNSW index parameter, indicating the breadth of searching neighbor nodes when building the graph.<br><br><br>* Optional configuration when indexType is set to IndexType.HNSW. |
|hnswSef |Integer |No |800 |HNSW index parameter, indicating the search breadth for online retrieval.<br><br><br>* Optional configuration when indexType is set to IndexType.HNSW. |
|diskannM |Integer |No | |DISKANN parameter, indicating the number of neighbor nodes.<br><br><br>* Optional configuration when indexType is set to IndexType.DISKANN. |
|diskannCef |Integer |No | |DISKANN parameter, indicating the breadth of searching neighbor nodes when building the graph.<br><br><br>* Optional configuration when indexType is set to IndexType.DISKANN. |
|pqCodeRatio |Float |No | |DISKANN parameter, size limit for vector dimension encoding. The larger the value, the higher the recall rate, but it will increase memory usage. Range (0.0, 0.25].<br><br><br>* Optional configuration when indexType is set to IndexType.DISKANN. |
|cacheRatio |Float |No | |DISKANN parameter, ratio of cached nodes to raw data. Larger values improve index performance and increase memory usage. Range [0.0, 0.3).<br><br><br>* Optional configuration when indexType is set to IndexType.DISKANN. |


<span id="response-parameters"></span>
# Response Parameters


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|message |String |success |Operation result information |


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

public class CreateVikingdbIndexWithScalarIndex {
    public static void main(String[] args) {
        String ak = System.getenv("AK"); // ak
        String sk = System.getenv("SK"); // sk
        String endpoint = "vikingdb.ap-southeast-1.byteplusapi.com"; // Fill in the v2 domain name of the vector database control plane https://www.volcengine.com/docs/84313/1792715
        String region = "ap-southeast-1"; // Service region

        ApiClient apiClient = new ApiClient()
                .setEndpoint(endpoint)
                .setCredentials(Credentials.getCredentials(ak, sk))
                .setRegion(region);

        VikingdbApi api = new VikingdbApi(apiClient);

        CreateVikingdbIndexRequest request = new CreateVikingdbIndexRequest()
                .collectionName("test_collection_for_product")
                .indexName("idx_with_scalar_index")
                .vectorIndex(new VectorIndexForCreateVikingdbIndexInput()
                        .indexType(VectorIndexForCreateVikingdbIndexInput.IndexTypeEnum.HNSW_HYBRID)
                        .distance(VectorIndexForCreateVikingdbIndexInput.DistanceEnum.IP)
                        .quant(VectorIndexForCreateVikingdbIndexInput.QuantEnum.INT8)
                )
                .scalarIndex(Arrays.asList("product_type", "brand_name", "price", "sales")
                );

        try {
            CreateVikingdbIndexResponse response = api.createVikingdbIndex(request);
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
