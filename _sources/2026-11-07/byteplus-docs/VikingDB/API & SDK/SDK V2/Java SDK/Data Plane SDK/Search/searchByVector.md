---
title: "searchByVector"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/searchbyvector"
---

<span id="overview"></span>
# Overview

searchByVector is used for vector search: based on the query vector, it searches for the limit number of vectors closest to it.


* After data is written/deleted from the Collection, Index data update takes approximately 20 seconds, so it cannot be immediately retrieved from the Index.

* When the request parameter filter is configured, it indicates hybrid search; when the request parameter filter is not configured, it indicates pure vector search.


<span id="prerequisites"></span>
# Prerequisites


* When creating a collection via the createCollection interface, the defined fields have already added vector fields.

* When writing data via the upsertData interface, the field names and field values of vector type have been written.

* When creating an index via createIndex, the vectorIndex vector index has been created.


Applicable when selecting "Existing vector data" when creating a vector database: when the imported data is vectors, you can input vectors through this interface for retrieval.

<span id="method-definition"></span>
# Method Definition

```Java
    public DataApiResponse<SearchResult> searchByVector(SearchByVectorRequest request)
            throws ApiClientException, VectorApiException
```


<span id="request-parameters"></span>
# **Request Parameters**

The request parameter is SearchByVectorRequest. The parameters included in the SearchByVectorRequest instance are shown in the table below.


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|denseVector |List[Float] |Yes |Dense vector for retrieval. |
|sparseVector |Map[String, Float] |No |Sparse vector for retrieval. |
|filter |Map[String, Object] |No |Filter conditions, see **Scalar Filtering**<br><br><br>* Default is empty, no filtering applied.<br><br>* Filter conditions include four query operators: must, must_not, range, range_out, and support and / or combinations of these operators. |
|outputFields |List[String] |No |List of scalar fields to return.<br><br><br>1. When user does not pass outputFields, all scalar fields are returned.<br><br>2. When user passes an empty list, no scalar fields are returned.<br><br>3. If outputFields format is incorrect, or the fields do not exist in the collection, the interface returns an error |
|limit |Integer |No |Number of retrieval results, maximum 5000. |
|offset |Integer |No |Offset. Only used in pagination scenarios. Not recommended to set too large a value, otherwise deep pagination may be affected. Default value is 0. The value must be at least 0, with the same semantics as MySQL's offset. |
|advance |SearchAdvance |No |Advanced parameters, see [Retrieval Common Parameters](https://docs.byteplus.com/docs/84313/1927082) |


<span id="response-parameters"></span>
# Response Parameters


|**Attribute** |Type |**Description** |
|---|---|---|
|data |List[SearchItem] |See below |
|filterMatchedCount |Integer |Number of filter matches |
|totalReturnCount |Integer |Number of results returned |
|realTextQuery |String | |
|tokenUsage |Object |Token usage |



* List[SearchItem]



|**Attribute** |Type |**Description** |
|---|---|---|
|id |Object |Primary key id. |
|fields |Map[String, Object] |The fields in the response |
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

import java.util.ArrayList;
import java.util.List;
import java.util.Random;

public class SearchByVector {

    public static void main(String[] args) {
        VectorService vectorService = null;
        try {
            vectorService = new VectorService(
                    Scheme.HTTPS,
                    "api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com", // Fill in the domain name for vector database Data Plane V2 https://www.volcengine.com/docs/84313/1792715
                    "cn-beijing",
                    new AuthWithAkSk(System.getenv("AK"), System.getenv("SK")),
                    ClientConfig.builder().build()
            );
        } catch (Exception e) {
            System.err.println("Client initialization failed: " + e.getMessage());
            e.printStackTrace();
            return;
        }

        SearchByVectorRequest request = SearchByVectorRequest.builder()
                .collectionName("your_collection_name") // Replace with your collection name
                .indexName("your_index_name") // Replace with your index name
                .denseVector(generateRandomVector(128)) // Provide the vector for query
                .limit(5) // Return the top 5 most similar results
                .build();

        try {
            DataApiResponse<SearchResult> response = vectorService.searchByVector(request);
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


    private static List<Float> generateRandomVector(int n) {
        List<Float> randomList = new ArrayList();
        Random random = new Random();

        for(int i = 0; i < n; ++i) {
            float randomFloat = random.nextFloat() * 2.0F - 1.0F;
            randomList.add(randomFloat);
        }

        return randomList;
    }
}

```
