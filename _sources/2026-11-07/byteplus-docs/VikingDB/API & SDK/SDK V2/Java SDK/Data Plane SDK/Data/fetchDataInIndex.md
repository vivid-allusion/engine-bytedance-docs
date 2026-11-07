---
title: "fetchDataInIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/fetchdatainindex"
---

<span id="overview"></span>
# Overview

fetchData is used for Index data queries. Based on primary key IDs, it queries single or multiple data entries in a specified Index, with a maximum of 100 data entries per query.

After Collection data is written/deleted, there is a synchronization delay in Index data updates, generally around 10s, so it cannot be queried immediately in the Index.

<span id="method-definition"></span>
# Method Definition

```Java
    public DataApiResponse<FetchDataInIndexResult> fetchDataInIndex(FetchDataInIndexRequest request)
            throws ApiClientException, VectorApiException
```


<span id="request-parameters"></span>
# **Request Parameters**


|Parameter Name |Type |Required |Remarks |
|---|---|---|---|
|resourceId |String |2选1 |Resource ID |
|collectionName |String | |Collection name |
|indexName |String |Yes |Index name |
|ids |List[Object] |Yes |* List of primary keys for point lookup. Maximum 100 entries |
| | | | |
|outputFields |List[String] |No |List of scalar fields to return.<br><br><br>1. When outputFields is not specified, all scalar fields are returned<br><br>2. If an empty list is passed, no scalar fields are returned<br><br>3. If outputFields format is incorrect or filter fields are not in the collection, the interface returns an error |


<span id="response-parameters"></span>
# Response Parameters


|Name |Type |Description |
|---|---|---|
|fetch |List[FetchInCollectionItem] |List of queried data, see FetchInCollectionItem structure below. |
|idsNotExist |List[Object] |List of non\-existent primary keys |



* List[FetchInCollectionItem]



|Parameter Name |Type |Remarks |
|---|---|---|
|id |Object |Primary key value |
|fields |Map[String, Object] |key is field name, value is field value |
|denseVector |List[Float] |Dense vector |
|denseDim |Integer |Dense vector dimension |


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

public class FetchDataInIndex {

    public static void main(String[] args) {
        VectorService vectorService = null;
        try {
            vectorService = new VectorService(
                    Scheme.HTTPS,
                    "api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com", // Enter the vector database data plane v2 domain  https://www.volcengine.com/docs/84313/1792715
                    "cn-beijing",
                    new AuthWithAkSk(System.getenv("AK"), System.getenv("SK")),
                    ClientConfig.builder().build()
            );
        } catch (Exception e) {
            System.err.println("Client initialization failed: " + e.getMessage());
            e.printStackTrace();
            return;
        }

        FetchDataInIndexRequest request = FetchDataInIndexRequest.builder()
                .collectionName("your_collection_name") // Replace with your collection name
                .indexName("your_index_name") // Replace with your index name
                .ids(Arrays.asList(1, 2, 3))
                .build();

        try {
            DataApiResponse<FetchDataInIndexResult> response = vectorService.fetchDataInIndex(request);
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


 &nbsp;
