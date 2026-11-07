---
title: "searchByRandom"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/searchbyrandom"
---

<span id="overview"></span>
# Overview

Random search is a retrieval method that returns several random records from a dataset without specifying query content. Random search also supports filtering and post\-processing of search results, and can be used for scenarios such as comparing recall effects and data filtering.

<span id="method-definition"></span>
# Method Definition

```Java
    public DataApiResponse<SearchResult> searchByRandom(SearchByRandomRequest request)
            throws ApiClientException, VectorApiException
```


<span id="request-parameters"></span>
# **Request Parameters**


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|filter |Map[String, Object] |No |Filter conditions, see **Scalar Filtering**<br><br><br>* Default is empty, no filtering.<br><br>* Filter conditions include four query operators: must, must_not, range, and range_out, and support AND and OR combinations of query operators. |
|outputFields |List[String] |No |List of scalar fields to return.<br><br><br>1. If user does not pass outputFields, returns all scalar fields<br><br>2. If user passes an empty list, returns no scalar fields<br><br>3. If outputFields format is incorrect or filter fields are not fields in the collection, the interface returns an error |
|limit |Integer |No |Number of search results, maximum 5000. |
|offset |Integer |No |Offset. Only used in pagination scenarios. It is not recommended to set an excessively large value, otherwise it may affect deep pagination performance. Default value is 0. The value must be at least 0, with the same semantics as MySQL offset. |
|advance |SearchAdvance |No |Advanced parameters, not commonly used |


<span id="response-parameters"></span>
# Response Parameters


|**Attribute** |Type |**Description** |
|---|---|---|
|data |List[SearchItem] |See below |
|filterMatchedCount |Integer |Number of matched filters |
|totalReturnCount |Integer |Number of returned results |
|realTextQuery |String | |
|tokenUsage |Object |Token usage |



* List[SearchItem]



|**Attribute** |Type |**Description** |
|---|---|---|
|id |Object |Primary key id. |
|fields |Map[String, Object] |fields field in the response |
|score |Float |Similarity |
|annScore |Float |ANN score |


<span id="example"></span>
# Example

<span id="request-parameters"></span>
## Request Parameters

```Java
package org.example.newsubproduct.data.search;

import com.volcengine.vikingdb.runtime.core.ClientConfig;
import com.volcengine.vikingdb.runtime.core.auth.AuthWithAkSk;
import com.volcengine.vikingdb.runtime.enums.Scheme;
import com.volcengine.vikingdb.runtime.exception.VectorApiException;
import com.volcengine.vikingdb.runtime.vector.model.request.*;
import com.volcengine.vikingdb.runtime.vector.model.response.*;
import com.volcengine.vikingdb.runtime.vector.service.VectorService;

import java.util.*;

public class SearchByRandom {

    public static void main(String[] args) {
        VectorService vectorService = null;
        try {
            vectorService = new VectorService(
                    Scheme.HTTPS,
                    "api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com", // Fill in the vector database data plane v2 domain https://www.volcengine.com/docs/84313/1792715
                    "cn-beijing",
                    new AuthWithAkSk(System.getenv("AK"), System.getenv("SK")),
                    ClientConfig.builder().build()
            );
        } catch (Exception e) {
            System.err.println("Client initialization failed: " + e.getMessage());
            e.printStackTrace();
            return;
        }

        SearchByRandomRequest request = SearchByRandomRequest.builder()
                .collectionName("your_collection_name") // Replace with your collection name
                .indexName("your_index_name") // Replace with your index name
                .limit(5)
                .filter(new HashMap<String, Object>(){{
                    put("op", "must_not");
                    put("field", "f_int64_2");
                    put("conds", Arrays.asList(3, 33));
                }})
                .advance(SearchAdvance.builder()
                        .idsIn(Arrays.asList(1, 2, 3, 4, 5)).build())
                .build();

        try {
            DataApiResponse<SearchResult> response = vectorService.searchByRandom(request);
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
