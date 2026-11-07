---
title: "listVikingdbTask"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/listVikingdbTask"
---

<span id="overview"></span>
# Overview

Gets information for multiple Tasks, displaying up to 20 records at a time.

<span id="method-definition"></span>
# Method Definition

```Java
public ListVikingdbTaskResponse listVikingdbTask(ListVikingdbTaskRequest body) throws ApiException
```


<span id="request-parameters"></span>
# Request Parameters


|Parameter |Type |Required |Description |
|---|---|---|---|
|projectName |String |No |Project name |
|collectionName |String |One of two required |Collection name |
|resourceId |String | |Collection resource ID. The request must specify either resourceId or collectionName. |
|taskStatus |String |Yes |Task status, see below |
|taskType |String |Yes |Task type, see below |
|pageNumber |Integer |No |Page number for pagination. Starts at 1. |
|pageSize |Integer |No |Page size for pagination. |


<span id="response-parameters"></span>
# Response Parameters


|Field |Type |Sub\-field Description |
|---|---|---|
|tasks |List[TaskForListVikingdbTaskOutput] |Task list |
|pageSize |Integer | |
|pageNumber |Integer | |
|totalCount |Integer | |



* List[TaskForListVikingdbTaskOutput]



|**Attribute** | |**Type** |**Description** |
|---|---|---|---|
|taskId | |string |Task ID |
|taskConfig | |TaskConfigForListVikingdbTaskOutput |Task configuration, see below |
| |collectionName |String |Collection name |
| |exportAll |Boolean |Whether to export full data |
|taskType | |string |Task type |
|taskStatus | |string |Task status |
|updatePerson | |string |Task updater |
|updateTime | |string |Task info update time |
|createTime | |string |Task info creation time |
|taskProcessInfo | |TaskProcessInfoForListVikingdbTaskOutput |Task processing information, see below |



* taskType includes



|taskType<br><br>data_import |Description<br><br>Data import task |
|---|---|
|data_export |Data export task |
|filter_update |Data filter update task |
|filter_delete |Data filter delete task |



* taskStatus includes



|init |queued |running |done |fail |
|---|---|---|---|---|
|Initializing |Queued |Running |Done |Failed |



* TaskProcessInfoForListVikingdbTaskOutput includes



|**Field** |**Type** |**Description** |
|---|---|---|
|taskProgress |string |Task progress, e.g., 50% |
|errorMessage |string |Task error message |
|sampleData |List[SampleDataForGetVikingdbTaskOutput] |5 sampled data records for display |
|sampleTimestamp |Integer |Sampling timestamp; data written after this timestamp will not be processed |
|scanDataCount |Integer |Current scanned data volume |
|totalDataCount |Integer |Total number of data records in Collection (estimated) |
|totalFilterCount |Integer |Number of filtered data records |


<span id="example"></span>
# Example

```Java
package org.example.newsubproduct.console.task;

import com.volcengine.ApiClient;
import com.volcengine.ApiException;
import com.volcengine.sign.Credentials;
import com.volcengine.vikingdb.VikingdbApi;
import com.volcengine.vikingdb.model.*;

public class ListVikingdbTask {
    public static void main(String[] args) {
        String ak = System.getenv("AK"); // ak
        String sk = System.getenv("SK"); // sk
        String endpoint = "vikingdb.ap-southeast-1.byteplusapi.com"; // Enter the vector database control plane v2 domain  https://www.volcengine.com/docs/84313/1792715
        String region = "ap-southeast-1"; // Service region

        ApiClient apiClient = new ApiClient()
                .setEndpoint(endpoint)
                .setCredentials(Credentials.getCredentials(ak, sk))
                .setRegion(region);

        VikingdbApi api = new VikingdbApi(apiClient);

        ListVikingdbTaskRequest request = new ListVikingdbTaskRequest()
                .collectionName("test_collection_for_sdk_with_vector")
                .taskStatus(ListVikingdbTaskRequest.TaskStatusEnum.RUNNING)
                .taskType(ListVikingdbTaskRequest.TaskTypeEnum.DATA_IMPORT);

        try {
            ListVikingdbTaskResponse response = api.listVikingdbTask(request);
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
