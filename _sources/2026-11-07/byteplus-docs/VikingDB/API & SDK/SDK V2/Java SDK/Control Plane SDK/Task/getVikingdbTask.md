---
title: "getVikingdbTask"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/getVikingdbTask"
---

<span id="overview"></span>
# Overview

Query the detailed information and execution progress of a specified task.

<span id="method-definition"></span>
# Method Definition

```Java
public GetVikingdbTaskResponse getVikingdbTask(GetVikingdbTaskRequest body) throws ApiException
```


<span id="request-parameters"></span>
# Request Parameters


|Field Name |Type |Required |Description |
|---|---|---|---|
|taskId |string |Yes |Task ID, returned when creating the task |


<span id="response-parameters"></span>
# Response Parameters


|**Attribute** |**Type** |**Description** |
|---|---|---|
|taskId |string |Task ID |
|taskType |string |Task type |
|taskStatus |string |Task status |
|updatePerson |string |Task updater |
|updateTime |string |Task information update time |
|createTime |string |Task information creation time |
|taskProcessInfo |TaskProcessInfoForGetVikingdbTaskOutput |Task processing information, see below |



* taskType types include:



|taskType<br><br>data_import |Description<br><br>Data import task |
|---|---|
|data_export |Data export task |
|filter_update |Data filter update task |
|filter_delete |Data filter delete task |



* taskStatus includes:



|init |queued |confirm |confirmed |running |done |fail |
|---|---|---|---|---|---|---|
|Initializing |Queued |Requires manual confirmation |Confirmed |Running |Completed |Failed |



* TaskProcessInfoForGetVikingdbTaskOutput



|**Field** |**Type** |**Description** |
|---|---|---|
|taskProgress |string |Task progress, e.g., 50% |
|errorMessage |string |Task error message |
|sampleData |List[SampleDataForGetVikingdbTaskOutput] |Sample 5 data entries for display |
|sampleTimestamp |Integer |Sampling timestamp, data written after this timestamp will not be processed |
|scanDataCount |Integer |Current scanned data volume |
|totalDataCount |Integer |Total number of Collection data entries (estimated) |
|totalFilterCount |Integer |Number of filtered data entries |


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

public class GetVikingdbTask {
    public static void main(String[] args) {
        String ak = System.getenv("AK"); // ak
        String sk = System.getenv("SK"); // sk
        String endpoint = "vikingdb.ap-southeast-1.byteplusapi.com"; // Fill in the domain name of the vector database control plane V2  https://www.volcengine.com/docs/84313/1792715
        String region = "ap-southeast-1"; // Service region

        ApiClient apiClient = new ApiClient()
                .setEndpoint(endpoint)
                .setCredentials(Credentials.getCredentials(ak, sk))
                .setRegion(region);

        VikingdbApi api = new VikingdbApi(apiClient);

        GetVikingdbTaskRequest request = new GetVikingdbTaskRequest()
                .taskId("ff39477b-a7f4-5f63-abd5-1592aaf6dc0c");

        try {
            GetVikingdbTaskResponse response = api.getVikingdbTask(request);
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
