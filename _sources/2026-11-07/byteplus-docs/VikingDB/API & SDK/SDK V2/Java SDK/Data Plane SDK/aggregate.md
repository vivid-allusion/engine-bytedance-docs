---
title: "aggregate"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/aggregate_v2"
---

<span id="overview"></span>
# Overview

Aggregate statistics can perform group aggregation on specified fields and support filtering operations to obtain corresponding aggregated statistics, helping to understand data distribution and other scenarios.

The index must contain at least one scalar index field of enumeration type (string, int64, or bool type).

<span id="method-definition"></span>
# Method Definition

```Java
    public DataApiResponse<AggregateResult> aggregate(AggregateRequest request)
            throws ApiClientException, VectorApiException
```


<span id="request-parameters"></span>
# Request Parameters


|Parameter Name |Type |Required |Description |
|---|---|---|---|
|resourceId |String |2 out of 1 |Resource ID |
|collectionName |String | |Collection name |
|indexName |String |Yes |Index name |
|filter |Map[String, Object] |No |Filter condition, see below for format. Default is empty, no filtering is applied. |
|op |string |Yes |Currently only supports count. When using the count operator, the index must have at least one scalar index field of type string, int64, or bool. |
|field |string |No |Aggregate on the specified field name. Supported field types are string, int64, bool and must be scalar index fields. |
|cond |Map[String, Object] |No |Similar to the HAVING clause in SQL GROUP BY. Only takes effect when the field parameter is specified. For the count operator, "gt" is supported, which means only result items greater than the threshold will be returned. |


<span id="return-parameters"></span>
## Return Parameters

Java calls execute the above task and return AggregateResult. The properties contained in the AggregateResult instance are shown in the table below.


|**Attribute** | |**Description** |
|---|---|---|
|agg |Map[String, Object] |Aggregation result (key is the field value, value is the count; only the total is returned when field is not specified) |
|op |String |Operator name (currently only supports count) |
|field |String |Aggregation field name |


<span id="example"></span>
# Example

<span id="request-parameters"></span>
## Request Parameters

```Java
package org.example.newsubproduct.data;

import com.volcengine.vikingdb.runtime.core.ClientConfig;
import com.volcengine.vikingdb.runtime.core.auth.AuthWithAkSk;
import com.volcengine.vikingdb.runtime.enums.Scheme;
import com.volcengine.vikingdb.runtime.exception.VectorApiException;
import com.volcengine.vikingdb.runtime.vector.model.request.*;
import com.volcengine.vikingdb.runtime.vector.model.response.*;
import com.volcengine.vikingdb.runtime.vector.service.VectorService;

public class Aggregate {

    public static void main(String[] args) {
        VectorService vectorService = null;
        try {
            vectorService = new VectorService(
                    Scheme.HTTPS,
                    "api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com", // Fill in the v2 data plane domain name of the vector database  https://www.volcengine.com/docs/84313/1792715
                    "cn-beijing",
                    new AuthWithAkSk(System.getenv("AK"), System.getenv("SK")),
                    ClientConfig.builder().build()
            );
        } catch (Exception e) {
            System.err.println("Client initialization failed: " + e.getMessage());
            e.printStackTrace();
            return;
        }

        AggregateRequest request = AggregateRequest.builder()
                .collectionName("your_collection_name") // Replace with your collection name
                .indexName("your_index_name") // Replace with your index name
                .op("count")
                .field("id")
                .build();

        try {
            DataApiResponse<AggregateResult> response = vectorService.aggregate(request);
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
