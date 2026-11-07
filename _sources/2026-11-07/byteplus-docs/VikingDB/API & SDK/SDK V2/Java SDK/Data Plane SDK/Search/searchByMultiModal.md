---
title: "searchByMultiModal"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/searchbymultimodal"
---

<span id="overview"></span>
# Overview

searchByMultiModal is used for multimodal data retrieval. Multimodal data retrieval means the vector database supports direct retrieval using multimodal data types such as text and images, and supports combinations of modalities, such as text\-to\-image, image\-to\-image, image\-to\-text+image, etc.


* Currently supports unstructured data of text, image, and video types.

* After writing/deleting Collection data, Index data update time is approximately 20 seconds, so it cannot be immediately retrieved in the Index.


<span id="prerequisites"></span>
# Prerequisites


* You have selected a database type starting from vectorization in the console and configured vectorization fields when creating the dataset; or when creating a dataset through the create_collection interface, you have configured the Collection's vectorization function by setting the vectorize parameter.

* When writing data through the upsert_data interface, you have written the field names and field values of text or image types.

* When creating an index through create_index, you have created a vector_index vector index.


Applicable when "vectorization required" is selected when creating the vector database: When the imported data is raw data, you can input text, images, etc. through this interface for retrieval.

<span id="method-definition"></span>
# Method Definition

```Java
    public DataApiResponse<SearchResult> searchByMultiModal(SearchByMultiModalRequest request, RequestAddition addition)
            throws ApiClientException, VectorApiException
```


<span id="request-parameters"></span>
# **Request Parameters**

The request parameter is SearchByMultiModalRequest. The parameters contained in the SearchByMultiModalRequest instance are shown in the table below.


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|text |string |At least 1 required |The input text for retrieval. |
|image |Object | |The input image for retrieval, currently supports 2 methods:<br><br><br>* Image TOS link. `tos://{bucket}/{object_key}`.<br><br>* Base64 string. `base64://{Base64 encoding}`. |
|video |Object | |{<br><br>"value": TOS link, http/https format link (this field is required)<br><br>"fps": 2.0 (0.2\-5, this field is optional)<br><br>} |
|filter |Map[String, Object] |No |Filter conditions, see **Scalar Filtering** for details.<br><br><br>* Default is empty, no filtering.<br><br>* Filter conditions include four query operators: must, must_not, range, range_out, and include two combinations of query operators: and and or. |
|outputFields |List[String] |No |List of scalar fields to return.<br><br><br>1. When user does not pass outputFields, all scalar fields are returned<br><br>2. When user passes an empty list, no scalar fields are returned<br><br>3. When outputFields format is incorrect or the filter field is not a field in the collection, the interface returns an error |
|limit |Integer |No |Number of retrieval results, maximum 5000. |
|offset |Integer |No |Offset. Only used in pagination scenarios. It is not recommended to set too large a value, otherwise it will affect deep pagination. Default value is 0. The set value must be at least 0, and the semantics are the same as MySQL's offset. |
|advance |SearchAdvance |No |Advanced parameters, see [Common Retrieval Parameters](https://docs.byteplus.com/docs/84313/1927082) |
|needInstruction |Boolean |No |Determined by the model default value, Doubao series models default to true, other models default to false |


<span id="response-parameters"></span>
# Response Parameters


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


public class SearchByMultiModal {

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

        SearchByMultiModalRequest request = SearchByMultiModalRequest.builder()
                .collectionName("your_collection_name") // Replace with your collection name
                .indexName("your_index_name") // Replace with your index name
                .text("你好。")
                .limit(5) // Return the top 5 most similar results
                .build();

        try {
            DataApiResponse<SearchResult> response = vectorService.searchByMultiModal(request);
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
