---
title: "updateData"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/updatedata"
---

<span id="overview"></span>
# Overview

updateData is used to update partial fields of existing data, supporting updates to text, scalar fields, and vector fields.

<span id="method-definition"></span>
# Method Definition

```Java
    public DataApiResponse<UpdateDataResult> updateData(UpdateDataRequest request)
            throws ApiClientException, VectorApiException
```


<span id="request-parameters"></span>
# **Request Parameters**


|Name |Type |Description |Required |
|---|---|---|---|
|collectionName |String |The name of the collection. |Either one is required |
|resourceId |String |The ID of the collection. | |
|data |List[Map[String, Object]] |List of data to update. Each Map in the list represents one data entry and must include the primary key field. |Yes |
|ttl |Integer |Time\-To\-Live (TTL) of the data in seconds. Data will be automatically deleted after this time expires. |No |


<span id="response-parameters"></span>
# Response Parameters


|Name |Type |Description |
|---|---|---|
|tokenUsage |Object |Token usage for this request. |


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
import java.util.HashMap;

public class UpdateData {

    public static void main(String[] args) {
        VectorService vectorService = null;
        try {
            vectorService = new VectorService(
                    Scheme.HTTPS,
                    "api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com", // Fill in the data plane V2 domain of the vector database https://www.volcengine.com/docs/84313/1792715
                    "cn-beijing",
                    new AuthWithAkSk(System.getenv("AK"), System.getenv("SK")),
                    ClientConfig.builder().build()
            );
        } catch (Exception e) {
            System.err.println("Client initialization failed: " + e.getMessage());
            e.printStackTrace();
            return;
        }

        UpdateDataRequest request = UpdateDataRequest.builder()
                .collectionName("your_collection_name") // Replace with your collection name
                .data(Arrays.asList(
                        new HashMap<String, Object>() {{ put("id", 1); put("field1", "new_value1"); }},
                        new HashMap<String, Object>() {{ put("id", 2); put("field1", "new_value2"); }}
                ))
                .build();

        try {
            DataApiResponse<UpdateDataResult> response = vectorService.updateData(request);
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
