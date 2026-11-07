---
title: "FilterUpdate"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/filterupdate"
---

<span id="overview"></span>
# Overview

Batch update data by specific conditions. Does not support updating fields of vector, sparse_vector, or text types.

<span id="method-definition"></span>
# Method Definition

```Java
public CreateVikingdbTaskResponse createVikingdbTask(CreateVikingdbTaskRequest body) throws ApiException
```


<span id="request-parameters"></span>
# Request Parameters


|Parameter |Sub\-parameter |Type |Required |Description |
|---|---|---|---|---|
|projectName | |String |No |Project name |
|collectionName | |String |Either one is required |Collection name |
|resourceId | |String | |Collection resource ID. The request must specify either resourceId or collectionName. |
|**taskType** | |String |Yes |filter_update |
|taskConfig | |TaskConfigForCreateVikingdbTaskInput |Yes |Task specific configuration |
| |filterConds |List[Object] |Yes |Filter conditions. Usage reference: https://www.volcengine.com/docs/84313/1791133 |
| |updateFields |Object |Yes |Field values to be updated, must be scalar fields. Does not support updating fields of vector, sparse_vector, or text types. |


<span id="response-parameters"></span>
# Response Parameters


|Parameter |Type |Description |
|---|---|---|
|taskId |String |Task ID |
|message |String |Operation result message |


<span id="example"></span>
# Example

<span id="request-parameters"></span>
## Request Parameters

```Java
package org.example.newsubproduct.console.task;

import com.volcengine.ApiClient;
import com.volcengine.ApiException;
import com.volcengine.sign.Credentials;
import com.volcengine.vikingdb.VikingdbApi;
import com.volcengine.vikingdb.model.*;

import java.util.Collections;
import java.util.HashMap;
import java.util.Map;

public class CreateVikingdbTaskFilterUpdate {
    public static void main(String[] args) {
        String ak = System.getenv("AK"); // ak
        String sk = System.getenv("SK"); // sk
        String endpoint = "vikingdb.ap-southeast-1.byteplusapi.com"; // Enter the vector database control plane v2 domain name https://www.volcengine.com/docs/84313/1792715
        String region = "ap-southeast-1"; // Service region

        ApiClient apiClient = new ApiClient()
                .setEndpoint(endpoint)
                .setCredentials(Credentials.getCredentials(ak, sk))
                .setRegion(region);

        VikingdbApi api = new VikingdbApi(apiClient);

        Map<String, Object> filter = new HashMap<>();
        filter.put("op", "must");
        filter.put("field", "city");
        filter.put("conds", Collections.singletonList("beijing"));
        Map<String, Object> updateData = new HashMap<>();
        updateData.put("city", "shanghai");

        CreateVikingdbTaskRequest request = new CreateVikingdbTaskRequest()
                .collectionName("test_collection_for_sdk_with_vector")
                .taskType(CreateVikingdbTaskRequest.TaskTypeEnum.FILTER_UPDATE)
                .taskConfig(
                        new TaskConfigForCreateVikingdbTaskInput()
                                .filterConds(Collections.singletonList(filter))
                                .updateFields(updateData)
                );

        try {
            CreateVikingdbTaskResponse response = api.createVikingdbTask(request);
            System.out.println("response body: " + response);
            System.out.println();
            System.out.println("response meta RequestId: " + response.getResponseMetadata().getRequestId());
            System.out.println("response meta Service: " + response.getResponseMetadata().getService());
            System.out.println("response meta Region: " + response.getResponseMetadata().getRegion());
            System.out.println("response meta Action: " + response.getResponseMetadata().getAction());
            System.out.println("response meta Version: " + response.getResponseMetadata().getVersion());
        } catch (ApiException e) {
            System.out.println("exception http code: " + e.getCode());
            System.out.println("exception response body: " + e.getResponseBody());
            System.out.println();
            System.out.println("exception RequestId: " + e.getResponseMetadata().getRequestId());
            System.out.println("exception Action: " + e.getResponseMetadata().getAction());
            System.out.println("exception Region: " + e.getResponseMetadata().getRegion());
            System.out.println("exception Service: " + e.getResponseMetadata().getService());
            System.out.println("exception Error.Code: " + e.getResponseMetadata().getError().getCode());
            System.out.println("exception Error.Message: " + e.getResponseMetadata().getError().getMessage());
        }
    }
}
```


 &nbsp;
