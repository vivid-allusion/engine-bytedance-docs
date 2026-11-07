---
title: "FilterDelete"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/filterdelete"
---

<span id="overview"></span>
# Overview

Batch delete data in a Collection based on specific conditions.

<span id="method-definition"></span>
# Method Definition

```Java
public CreateVikingdbTaskResponse createVikingdbTask(CreateVikingdbTaskRequest body) throws ApiException
```


<span id="request-parameters"></span>
# Request Parameters

To back up data to TOS, first authorize VikingDB for cross\-service access to TOS [Authorize Now](https://console.volcengine.com/iam/service/attach_role/?ServiceName=vikingdb)


|Parameter |Sub\-parameter |Type |Required |Description |
|---|---|---|---|---|
|ProjectName | |String |No |Project name |
|CollectionName | |String |2 out of 1 required |Dataset name |
|ResourceId | |String | |Dataset resource ID. The request must specify either ResourceId or CollectionName. |
|**TaskType** | |String |Yes |filter_delete |
|TaskConfig | |TaskConfigForCreateVikingdbTaskInput |Yes |Task specific configuration |
| |FileType |String |Yes |File type, json or parquet, required |
| |NeedConfirm |Boolean |No |Whether manual confirmation is required, default is true |
| |FilterConds |List[Object] |Yes |Filter conditions. Reference: https://www.volcengine.com/docs/84313/1791133 |
| |TosPath |String |Yes |TOS path, format: {bucket name}/{path}, note this is not a domain name. Required |


<span id="response-parameters"></span>
# Response Parameters


|Parameter |Type |Description |
|---|---|---|
|TaskId |String |Task ID |
|Message |String |Operation result information |


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
import com.volcengine.vikingdb.model.CreateVikingdbTaskRequest;
import com.volcengine.vikingdb.model.CreateVikingdbTaskResponse;
import com.volcengine.vikingdb.model.TaskConfigForCreateVikingdbTaskInput;

import java.util.Collections;
import java.util.HashMap;
import java.util.Map;

public class CreateVikingdbTaskFilterDelete {
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

        CreateVikingdbTaskRequest request = new CreateVikingdbTaskRequest()
                .collectionName("test_collection_for_sdk_with_vector")
                .taskType(CreateVikingdbTaskRequest.TaskTypeEnum.FILTER_DELETE)
                .taskConfig(
                        new TaskConfigForCreateVikingdbTaskInput()
                                .filterConds(Collections.singletonList(filter))
                                .needConfirm(true)
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


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|TaskId |String | |Task ID |
|Message |String |success |Operation result information |


<span id="follow-up-processing"></span>
## Follow\-up Processing

If manual confirmation is required, perform the **Update Task** operation.
