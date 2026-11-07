---
title: "deleteVikingdbCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/deleteVikingdbCollection"
---

<span id="overview"></span>
# Overview

DeleteVikingdbCollection is used to delete an existing dataset Collection.


* Executing Collection deletion will permanently delete all data under the specified Collection, please proceed with caution.

* Before deleting a Collection, you must first delete all Indexes associated with the Collection to successfully delete the Collection.


<span id="method-definition"></span>
# Method Definition

```Java
 public DeleteVikingdbCollectionResponse deleteVikingdbCollection(DeleteVikingdbCollectionRequest body) throws ApiException
```


<span id="request-parameters"></span>
# **Request Parameters**


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|projectName |String |No |Project name |
|collectionName |String |One of two required |Specifies the name of the Collection to delete.<br><br><br>* Can only use English letters, numbers, underscores _, and must start with an English letter, cannot be empty.<br><br>* Length requirement: [1, 128].<br><br>* Collection name cannot be duplicated. |
|resourceId |String | |Dataset resource ID. The request must specify either resourceId or collectionName. |


<span id="response-parameters"></span>
# Response Parameters


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|message |String |success |Operation result message |


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

public class DeleteVikingdbCollection {
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


        DeleteVikingdbCollectionRequest request = new DeleteVikingdbCollectionRequest()
                .collectionName("test_collection_for_sdk_with_vector");

        try {
            DeleteVikingdbCollectionResponse response = api.deleteVikingdbCollection(request);
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
