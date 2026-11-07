---
title: "updateVikingdbIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/updateVikingdbIndex"
---

<span id="overview"></span>
# Overview

The updateVikingdbIndex interface is used to update the description, cpuQuota, and scalarIndex of a specified Index.

<span id="method-definition"></span>
# Method Definition

```Java
public UpdateVikingdbIndexResponse updateVikingdbIndex(UpdateVikingdbIndexRequest body) throws ApiException 
```


<span id="request-parameters"></span>
# **Request Parameters**

The request parameter is UpdateVikingdbIndexRequest. The parameters included in the UpdateVikingdbIndexRequest class are shown in the table below.


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|projectName |String |No |Project name |
|collectionName |String |One of two required |Specifies the name of the Collection to which the index to be updated belongs.<br><br><br>* Can only use English letters, numbers, and underscores _, must start with an English letter, and cannot be empty.<br><br>* Length requirement: [1, 128].<br><br>* Collection name must already exist. |
|resourceId |String | |Dataset resource ID. The request must specify either resourceId or collectionName. |
|indexName |String |Yes |Specifies the name of the Index to be updated.<br><br><br>* Can only use English letters, numbers, and underscores _, must start with an English letter, and cannot be empty.<br><br>* Length requirement: [1, 128].<br><br>* Index name must already exist. |
|cpuQuota |Integer |No |CPU quota consumed by index retrieval, formatted as a positive integer.<br><br><br>* Related to throughput, not latency. 1 CPU core is approximately 100 QPS.<br><br>* N shards result in N times CPU consumption; if the CPU consumed by retrieval exceeds the quota, the index will be throttled.<br><br>* Value range: [2, 10240]. |
|description |String |No |Custom description of the index. |
|scalarIndex |List[String] |No |List of scalar fields.<br><br><br>* scalarIndex defaults to None, indicating all fields are built into the scalar index.<br><br>* When scalarIndex is [], it means no scalar index.<br><br>* When scalarIndex is a non\-empty list, it means the fields in the list are built into the scalar index.<br><br><br>If scalar fields are included in the scalar index, they are mainly used for range filtering and enumeration filtering, and will consume additional resources:<br><br><br>* Range filtering: float32, int64<br><br>* Enumeration filtering: int64, string, list[int64], list[string], bool<br><br><br>If scalar fields are not included in the scalar index, they are still supported for selection as forward index fields and for partial forward index calculations. |
|shardCount |Integer |No |Number of shards. Index sharding means that in large\-scale data scenarios, index data can be divided into multiple small index blocks and distributed to different nodes in the same cluster for management. Each node is responsible for storing and processing a portion of the data, which can distribute query load to different nodes for concurrent processing. When a node fails, the system can automatically migrate the shard data on it to other normal nodes to ensure stability, enabling horizontal data scaling and high\-performance read/write operations.<br><br><br>* Value range: [1, 256].<br><br>* Default is 1. Shard count estimation reference: estimated data volume / 30 million. |


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

public class UpdateVikingdbIndex {
    public static void main(String[] args) {
        String ak = System.getenv("AK"); // ak
        String sk = System.getenv("SK"); // sk
        String endpoint = "vikingdb.ap-southeast-1.byteplusapi.com"; // Fill in the domain name of the vector database control plane V2 https://www.volcengine.com/docs/84313/1792715
        String region = "ap-southeast-1"; // Service region

        ApiClient apiClient = new ApiClient()
                .setEndpoint(endpoint)
                .setCredentials(Credentials.getCredentials(ak, sk))
                .setRegion(region);

        VikingdbApi api = new VikingdbApi(apiClient);

        UpdateVikingdbIndexRequest request = new UpdateVikingdbIndexRequest()
                .collectionName("test_collection_for_sdk_with_vector")
                .indexName("idx_simple")
                .cpuQuota(2);

        try {
            UpdateVikingdbIndexResponse response = api.updateVikingdbIndex(request);
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
