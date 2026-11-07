---
title: "updateVikingdbTask"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/updateVikingdbTask"
---

<span id="overview"></span>
# Overview

Update the specified task. Currently, task updates are only used to **remove** the manual confirmation step of a task.

<span id="method-definition"></span>
# Method Definition

```Java
public UpdateVikingdbTaskResponse updateVikingdbTask(UpdateVikingdbTaskRequest body) throws ApiException 
```


<span id="request-parameters"></span>
# Request Parameters


|Field Name |Type |Required |Description |
|---|---|---|---|
|taskId |String |Yes |Task ID, returned when creating the task |
|taskStatus |String |Only tasks with confirm status can be updated, and can only be updated to confirmed. Required. | |
| | | | |
| | | | |
| | | | |
| | | | |


<span id="response-parameters"></span>
# Response Parameters


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|message |String |success |Operation result information |


<span id="example"></span>
# Example

```Java
package org.example.newsubproduct.console.task;

import com.volcengine.ApiClient;
import com.volcengine.ApiException;
import com.volcengine.sign.Credentials;
import com.volcengine.vikingdb.VikingdbApi;
import com.volcengine.vikingdb.model.*;

public class UpdateVikingdbTask {
    public static void main(String[] args) {
        String ak = System.getenv("AK"); // ak
        String sk = System.getenv("SK"); // sk
        String endpoint = "vikingdb.ap-southeast-1.byteplusapi.com"; // Fill in the domain name of the vector database control plane v2 https://www.volcengine.com/docs/84313/1792715
        String region = "ap-southeast-1"; // Service region

        ApiClient apiClient = new ApiClient()
                .setEndpoint(endpoint)
                .setCredentials(Credentials.getCredentials(ak, sk))
                .setRegion(region);

        VikingdbApi api = new VikingdbApi(apiClient);

        UpdateVikingdbTaskRequest request = new UpdateVikingdbTaskRequest()
                .taskId("ff39477b-a7f4-5f63-abd5-1592aaf6dc0c")
                .taskStatus(UpdateVikingdbTaskRequest.TaskStatusEnum.CONFIRMED);

        try {
            UpdateVikingdbTaskResponse response = api.updateVikingdbTask(request);
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
