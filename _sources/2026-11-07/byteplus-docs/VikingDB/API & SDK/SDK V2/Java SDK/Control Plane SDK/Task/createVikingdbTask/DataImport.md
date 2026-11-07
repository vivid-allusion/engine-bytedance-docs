---
title: "DataImport"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/dataimport"
---

<span id="overview"></span>
# Overview

Import data into the Collection. The column names in the file must match the Collection fields, otherwise parsing will fail.

Please authorize VikingDB to access TOS across services before use: [Authorize](https://console.volcengine.com/iam/service/attach_role/?ServiceName=vikingdb)

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
|collectionName | |String |One of two required |Collection name |
|resourceId | |String | |Collection resource ID. The request must specify either resourceId or collectionName. |
|**taskType** | |String |Yes |data_import |
|taskConfig | |TaskConfigForCreateVikingdbTaskInput |Yes |Specific task configuration |
| |fileType |String |Yes |File type, json or parquet. Required |
| |tosPath |String |Yes |TOS path, format: {bucket name}/{path}, note that this is not a domain name. Required |
| |ignoreError |Boolean |No |When set to true, file parsing continues when errors are encountered. Default is false |


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

public class CreateVikingdbTaskDataImport {
    public static void main(String[] args) {
        String ak = System.getenv("AK"); // ak
        String sk = System.getenv("SK"); // sk
        String endpoint = "vikingdb.ap-southeast-1.byteplusapi.com"; // Fill in the vector database control plane v2 domain name https://www.volcengine.com/docs/84313/1792715
        String region = "ap-southeast-1"; // Service region

        ApiClient apiClient = new ApiClient()
                .setEndpoint(endpoint)
                .setCredentials(Credentials.getCredentials(ak, sk))
                .setRegion(region);

        VikingdbApi api = new VikingdbApi(apiClient);

        CreateVikingdbTaskRequest request = new CreateVikingdbTaskRequest()
                .collectionName("test_collection_for_sdk_with_vector")
                .taskType(CreateVikingdbTaskRequest.TaskTypeEnum.DATA_IMPORT)
                .taskConfig(
                        new TaskConfigForCreateVikingdbTaskInput()
                                .fileType(TaskConfigForCreateVikingdbTaskInput.FileTypeEnum.JSON)
                                .tosPath("test-doc1-tos/pic_search_1000_images.json")
                                .ignoreError(true)
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
