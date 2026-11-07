---
title: "searchById"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/searchbyid"
---

<span id="overview"></span>
# Overview

searchById is used for searching based on primary key id. Retrieves the limit number of vectors closest to it based on the primary key id.


* For hybrid indexes using the hnsw\-hybrid algorithm, id\-based searching is temporarily not supported.

* After writing/deleting Collection data, Index data update time is expected to be about 20 seconds, so it cannot be retrieved in the Index immediately.

* When the request parameter filter is configured, it indicates hybrid search; when the request parameter filter is not configured, it indicates pure vector search.


<span id="prerequisites"></span>
# Prerequisites


* When creating a dataset through the createCollection interface, the defined fields have added the vector field.

* When writing data through the upsertData interface, the field names and field values of vector type have been written.

* When creating an index through the createIndex interface, the vectorIndex vector index has been created.


<span id="method-definition"></span>
# Method Definition

```Java
    public DataApiResponse<SearchResult> searchById(SearchByIdRequest request)
            throws ApiClientException, VectorApiException
```


<span id="request-parameters"></span>
# **Request Parameters**


|**Parameter** |**Type** |**Required** |**Parameter Description** |
|---|---|---|---|
|id |Object |Yes |Primary key id. |
|filter |Map[String, Object] |No |Filter conditions, see **Scalar Filtering**<br><br><br>* Default is empty, no filtering.<br><br>* Filter conditions include four query operators: must, must_not, range, range_out, and support and and or combinations of query operators. |
|outputFields |List[String] |No |List of scalar fields to return.<br><br><br>1. When user does not pass outputFields, all scalar fields are returned.<br><br>2. When user passes an empty list, no scalar fields are returned.<br><br>3. When outputFields format is incorrect, or the filter field is not a field in the collection, the interface returns an error. |
|limit |Integer |No |Number of search results, maximum 5000. |
|offset |Integer |No |Offset. Only used in pagination scenarios. It is not recommended to set too large a value, otherwise there will be deep pagination impact. Default value is 0. Set value must be at least 0, semantics are the same as MySQL's offset. |
|advance |SearchAdvance |No |Advanced parameters, see [Common Search Parameters](https://docs.byteplus.com/docs/84313/1927082) |


<span id="response-parameters"></span>
# Response Parameters


|**Attribute** |Type |**Description** |
|---|---|---|
|data |List[SearchItem] |See below |
|filterMatchedCount |Integer |Number of filtered matches |
|totalReturnCount |Integer |Number of returns |
|realTextQuery |String | |
|tokenUsage |Object |Token usage |



* List[SearchItem]



|**Attribute** |Type |**Description** |
|---|---|---|
|id |Object |Primary key id. |
|fields |Map[String, Object] |fields in the returned results. |
|score |Float |Similarity |
|annScore |Float |ANN score. |


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


public class SearchById {

    public static void main(String[] args) {
        VectorService vectorService = null;
        try {
            vectorService = new VectorService(
                    Scheme.HTTPS,
                    "api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com", // Fill in the domain name of vector database data plane v2  https://www.volcengine.com/docs/84313/1792715
                    "cn-beijing",
                    new AuthWithAkSk(System.getenv("AK"), System.getenv("SK")),
                    ClientConfig.builder().build()
            );
        } catch (Exception e) {
            System.err.println("Client initialization failed: " + e.getMessage());
            e.printStackTrace();
            return;
        }

        SearchByIdRequest request = SearchByIdRequest.builder()
                .collectionName("your_collection_name") // Replace with your collection name
                .indexName("your_index_name") // Replace with your index name
                .id("uuid_001")
                .limit(5) // Return top 5 most similar results
                .build();

        try {
            DataApiResponse<SearchResult> response = vectorService.searchById(request);
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
