---
title: "searchByKeywords"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/searchbykeywords"
---

<span id="overview"></span>
# Overview

SearchByKeywords is used for keyword search, applicable to indexes with text field vectorization configuration (vectorize parameter), and supports searching with multiple keywords.

<span id="method-definition"></span>
# Method Definition

```Java
    public DataApiResponse<SearchResult> searchByKeywords(SearchByKeywordsRequest request)
            throws ApiClientException, VectorApiException
```


<span id="request-parameters"></span>
# **Request Parameters**

The request parameter is SearchByKeywordsRequest. The parameters contained in the SearchByKeywordsRequest instance are shown in the following table.


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|keywords |List[String] |Yes |Keyword list, 1\-10 elements in the list, empty strings are not allowed for elements |
|caseSensitive |Boolean |No |Case\-sensitive or not. Default is false. |
|filter |Map[String, Object] |No |Filter conditions, see **Scalar Filtering** for details<br><br><br>* Default is empty, no filtering is performed.<br><br>* Filter conditions include four query operators: must, must_not, range, range_out, and two combinations of query operators: and and or. |
|outputFields |List[String] |No |List of scalar fields to return.<br><br><br>1. When the user does not pass outputFields, all scalar fields are returned<br><br>2. When the user passes an empty list, no scalar fields are returned<br><br>3. When the outputFields format is incorrect or the filter field is not a field in the collection, the interface returns an error |
|limit |Integer |No |Number of search results, maximum 5000. |
|offset |Integer |No |Offset. Only used in pagination scenarios. Setting too large a value is not recommended, as it may affect deep pagination performance. Default value is 0. The set value must be at least 0, and the semantics are the same as MySQL's offset. |
|advance |SearchAdvance |No |Advanced parameters, see [Common Search Parameters](https://docs.byteplus.com/docs/84313/1927082) |


<span id="response-parameters"></span>
# Response Parameters


|**Attribute** |Type |**Description** |
|---|---|---|
|data |List[SearchItem] |See below |
|filterMatchedCount |Integer |Number of filter matches |
|totalReturnCount |Integer |Number of returned results |
|realTextQuery |String |The actual text query involved in the search |
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

import java.util.Arrays;

public class SearchByKeywords {

    public static void main(String[] args) {
        VectorService vectorService = null;
        try {
            vectorService = new VectorService(
                    Scheme.HTTPS,
                    "api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com", // Fill in the domain name of the vector database data plane v2 https://www.volcengine.com/docs/84313/1792715
                    "cn-beijing",
                    new AuthWithAkSk(System.getenv("AK"), System.getenv("SK")),
                    ClientConfig.builder().build()
            );
        } catch (Exception e) {
            System.err.println("Client initialization failed: " + e.getMessage());
            e.printStackTrace();
            return;
        }

        SearchByKeywordsRequest request = SearchByKeywordsRequest.builder()
                .collectionName("your_collection_name") // Replace with your collection name
                .indexName("your_index_name") // Replace with your index name
                .keywords(Arrays.asList("keyword1", "keyword2"))
                .limit(10)
                .build();

        try {
            DataApiResponse<SearchResult> response = vectorService.searchByKeywords(request);
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


<span id="response-example"></span>
## Response Example
