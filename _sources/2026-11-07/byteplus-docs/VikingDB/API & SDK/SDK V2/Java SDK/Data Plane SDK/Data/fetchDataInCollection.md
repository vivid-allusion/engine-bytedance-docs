---
title: "fetchDataInCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/fetchdataincollection"
---

<span id="overview"></span>
# Overview

Query single or multiple data records in a specified Collection by primary key. You can query up to 100 records at a time.

Data can be queried in real\-time after being written to or deleted from the Collection.

<span id="method-definition"></span>
# Method Definition

```Java
    public DataApiResponse<FetchDataInCollectionResult> fetchDataInCollection(FetchDataInCollectionRequest request)
            throws ApiClientException, VectorApiException
```


<span id="request-parameters"></span>
# **Request Parameters**


|Parameter Name |Type |Required |Remarks |
|---|---|---|---|
|resourceId |String |Either this or collectionName is required |Resource ID |
|collectionName |String | |Collection name |
|ids |List[Object] |Yes |* Primary key list for point query. Maximum 100 records |
| | | | |


<span id="response-parameters"></span>
# Response Parameters


|Name |Type |Description |
|---|---|---|
|fetch |List[FetchInCollectionItem] |List of queried data records, see FetchResult structure below. |
|idsNotExist |List[Object] |List of non\-existent primary keys |



* List[FetchInCollectionItem]



|Name |Type |
|---|---|
|id |Object |
|fields |Map[String, Object] |


<span id="example"></span>
# Example

<span id="request-parameters"></span>
## Request Parameters

```Java
package org.example.newsubproduct.data.data;


import com.volcengine.vikingdb.runtime.core.ClientConfig;
import com.volcengine.vikingdb.runtime.core.auth.AuthWithAkSk;
import com.volcengine.vikingdb.runtime.enums.Scheme;
import com.volcengine.vikingdb.runtime.exception.VectorApiException;
import com.volcengine.vikingdb.runtime.vector.model.request.*;
import com.volcengine.vikingdb.runtime.vector.model.response.*;
import com.volcengine.vikingdb.runtime.vector.service.VectorService;

import java.util.Arrays;

public class FetchDataInCollection {

    public static void main(String[] args) {
        VectorService vectorService = null;
        try {
            vectorService = new VectorService(
                    Scheme.HTTPS,
                    "api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com", // Fill in the domain name for vector database data plane v2 https://www.volcengine.com/docs/84313/1792715
                    "cn-beijing",
                    new AuthWithAkSk(System.getenv("AK"), System.getenv("SK")),
                    ClientConfig.builder().build()
            );
        } catch (Exception e) {
            System.err.println("Client initialization failed: " + e.getMessage());
            e.printStackTrace();
            return;
        }

        FetchDataInCollectionRequest request = FetchDataInCollectionRequest.builder()
                .collectionName("your_collection_name") // Replace with your collection name
                .ids(Arrays.asList(1, 2, 3, -99))
                .build();

        try {
            DataApiResponse<FetchDataInCollectionResult> response = vectorService.fetchDataInCollection(request);
            System.out.println("request success:");
            System.out.println(response);
        } catch (VectorApiException vectorApiException) {
            System.err.println("request vectorApiException:");
            System.out.println("apiName: " + vectorApiException.getApiName());
            System.out.println("httpStatusCode: " + vectorApiException.getHttpStatusCode());
            System.out.println("code: " + vectorApiException.getCode());
            System.out.println("message: " + vectorApiException.getMessage());
            System.out.println("requestId: " + vectorApiException.getRequestId());
            System.out.println("responseContext: " + vectorApiException.getResponseContext().getBody());
        } catch (Exception e) {
            System.err.println("request exception, message : " + e.getMessage());
            e.printStackTrace();
        }
    }
}

```
