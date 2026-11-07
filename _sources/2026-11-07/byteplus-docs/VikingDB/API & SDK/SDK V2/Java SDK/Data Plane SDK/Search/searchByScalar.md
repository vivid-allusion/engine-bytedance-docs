---
title: "searchByScalar"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/searchbyscalar"
---

<span id="overview"></span>
# Overview

This interface applies to indexes that contain scalar index fields of int64/float32 types. Scalar retrieval in a vector database refers to the retrieval method based on scalar values. In a vector database, each vector has one or more scalar values, and scalar retrieval can search based on these scalar values to find query\-related data. For example, author feature retrieval in document retrieval.

<span id="method-definition"></span>
# Method Definition

```Java
    public DataApiResponse<SearchResult> searchByScalar(SearchByScalarRequest request)
            throws ApiClientException, VectorApiException
```


<span id="request-parameters"></span>
# Request Parameters


|Parameter Name |Type |Required |Remarks |
|---|---|---|---|
|field |String |Yes |Field name. Prerequisites: 1. The field must be int64 or float32. 2. A scalar index must be established for this field. |
|order |Order |No |asc/desc. The default is desc for descending order, and asc is for ascending order. |
|filter |Map[String, Object] |No |Filter conditions, see **Scalar Filtering**<br><br><br>* Default is empty, no filtering is performed.<br><br>* Filter conditions include four query operators: must, must_not, range, range_out, and two combinations of query operators: and and or. |
|outputFields |List[String] |No |List of scalar fields to return.<br><br><br>1. When the user does not pass outputFields, all scalar fields are returned<br><br>2. When the user passes an empty list, no scalar fields are returned<br><br>3. When the outputFields format is incorrect or the returned fields are not fields in the collection, the interface returns an error |
|limit |Integer |No |Number of retrieval results, maximum 5000. |
|offset |Integer |No |Offset. Only used in pagination scenarios. It is not recommended to set an excessively large value, otherwise there will be deep pagination impact. The default value is 0. The setting value must be at least 0, and the semantics are the same as MySQL's offset. |
|advance |SearchAdvance |No |Advanced parameters, not commonly used |


<span id="return-parameters"></span>
# Return Parameters


|**Attribute** |Type |**Description** |
|---|---|---|
|data |List[SearchItem] |See below |
|filterMatchedCount |Integer |Number of filter matches |
|totalReturnCount |Integer |Number of returns |
|realTextQuery |String | |
|tokenUsage |Object |Token usage |



* List[SearchItem]



|**Attribute** |Type |**Description** |
|---|---|---|
|id |Object |Primary key id. |
|fields |Map[String, Object] |The fields field in the request response |
|score |Float |Similarity |
|annScore |Float |ANN score |


<span id="example"></span>
# Example

```Java
package org.example.newsubproduct.data.search;

import com.volcengine.vikingdb.runtime.core.ClientConfig;
import com.volcengine.vikingdb.runtime.core.auth.AuthWithAkSk;
import com.volcengine.vikingdb.runtime.enums.Scheme;
import com.volcengine.vikingdb.runtime.exception.VectorApiException;
import com.volcengine.vikingdb.runtime.vector.model.request.*;
import com.volcengine.vikingdb.runtime.vector.model.response.*;
import com.volcengine.vikingdb.runtime.vector.service.VectorService;

import static com.volcengine.vikingdb.runtime.vector.model.request.Order.ASC;

public class SearchByScalar {

    public static void main(String[] args) {
        VectorService vectorService = null;
        try {
            vectorService = new VectorService(
                    Scheme.HTTPS,
                    "api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com", // Fill in the domain name of vector database data plane v2 https://www.volcengine.com/docs/84313/1792715
                    "cn-beijing",
                    new AuthWithAkSk(System.getenv("AK"), System.getenv("SK")),
                    ClientConfig.builder().build()
            );
        } catch (Exception e) {
            System.err.println("Client initialization failed: " + e.getMessage());
            e.printStackTrace();
            return;
        }

        SearchByScalarRequest request = SearchByScalarRequest.builder()
                .collectionName("your_collection_name") // Replace with your collection name
                .indexName("your_index_name") // Replace with your index name
                .field("your_scalar_field") // Replace with your scalar field
                .order(ASC) // or Order.DESC
                .limit(10)
                .build();

        try {
            DataApiResponse<SearchResult> response = vectorService.searchByScalar(request);
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
