---
title: "deleteData"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/deletedata"
---

<span id="overview"></span>
# Overview

deleteData is used to delete data in the specified Collection. It deletes single or multiple data entries based on primary keys, with a maximum of 100 data entries per deletion.

<span id="method-definition"></span>
# Method Definition

```Java
    public DataApiResponse<DeleteDataResult> deleteData(DeleteDataRequest request)
            throws ApiClientException, VectorApiException
```


<span id="request-parameters"></span>
# **Request Parameters**


|Parameter Name |Type |Required |Remarks |
|---|---|---|---|
|resourceId |String |2 out of 1 |Resource ID |
|collectionName |String | |Collection name |
|ids |List[Object] |2 out of 1 |List of primary keys for the data to be deleted (primary key is int64 or string). Maximum 100 entries.<br><br>Note:<br><br><br>* If the request parameters are invalid (4xx type), all deletions will fail. |
| | | | |
|delAll |Boolean | |When set to true, deletes all data; default is false.<br><br>When this interface deletes all data, it is not immediately synced to the index. Therefore, the data can still be retrieved from the index for a period of time (approximately 5 minutes). |


<span id="return-parameters"></span>
# Return Parameters

When Java calls execute the above task, no return information is provided on successful execution.

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


public class DeleteData {

    public static void main(String[] args) {
        VectorService vectorService = null;
        try {
            vectorService = new VectorService(
                    Scheme.HTTPS,
                    "api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com", // Fill in the domain name for vector database data plane v2  https://www.volcengine.com/docs/84313/1792715
                    "cn-beijing",
                    new AuthWithAkSk(System.getenv("AK"), System.getenv("SK")),
                    ClientConfig.builder().build()
            );
        } catch (Exception e) {
            System.err.println("Client initialization failed: " + e.getMessage());
            e.printStackTrace();
            return;
        }

        DeleteDataRequest request = DeleteDataRequest.builder()
                .collectionName("your_collection_name") // Replace with your collection name
                .ids(Arrays.asList(1, 2, 3))
                .build();

        try {
            DataApiResponse<DeleteDataResult> response = vectorService.deleteData(request);
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
