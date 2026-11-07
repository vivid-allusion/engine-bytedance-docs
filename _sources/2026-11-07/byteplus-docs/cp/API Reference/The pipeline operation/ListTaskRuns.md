---
title: "ListTaskRuns"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/ListTaskRuns"
---

Query execution records for a task in a pipeline

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, see [Service address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.cn\-beijing.byteplusapi.com.cn?Action=ListTaskRuns&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListTaskRuns |The API name. The name of the current API is `ListTaskRuns`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|WorkspaceId |String |Yes |7815d4783edc47c5bbd7df024ab9\*\*\*\* |Workspace ID. |
|PipelineId |String |Yes |c3afa3f27d754ac8b6052bf3dc0b\*\*\*\* |Pipeline ID. |
|PipelineRunId |String |Yes |c9020f1a904c41e4bc25afc96316\*\*\*\* |Pipeline run ID. |
|TaskId |String |Yes |7c9d82311f9246ccb24eae5457bd\*\*\*\* |Task ID. |
|Filter |Object of [TaskRunFilter](https://docs.byteplus.com/en/docs/292/73431#taskrunfilter) |no |\- |Filter for the list of task execution records to be queried. |
|PageSize |Long |no |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |
|PageNumber |Long |no |1 |The starting page number when querying. The default number is 1. |


<span id="taskrunfilter"></span>
### TaskRunFilter


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Ids |Array of String |no |["230643959e41493d9baf6012b785\*\*\*\*"] |Filter by task run record ID for a precise query. |
|Statuses |Array of String |no |["Succeeded"] |Filter by task status. The available values are:<br><br><br>* Queued: Pending execution.<br><br>* Running: In progress.<br><br>* Timeout: Timeout.<br><br>* Failed: Failed.<br><br>* Success: Success.<br><br>* Canceled: Canceled. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.cn-beijing.byteplusapi.com.cn?Action=ListTaskRuns&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "WorkspaceId": "7815d4783edc47c5bbd7df024ab9****",
    "PipelineId": "c3afa3f27d754ac8b6052bf3dc0b****",
    "PipelineRunId": "c9020f1a904c41e4bc25afc96316****",
    "TaskId": "7c9d82311f9246ccb24eae5457bd****",
    "Filter": {
        "Statuses": [
            "Succeeded"
        ]
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|TotalCount |Long |10 |Total number of task execution records. |
|Items |Array of [TaskRun](https://docs.byteplus.com/en/docs/292/73431#taskrun) |\- |Task run records. |
|PageSize |Long |10 |Page size. |
|PageNumber |Long |10 |The current page number. |


<span id="taskrun"></span>
### TaskRun


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Id |String |230643959e41493d9baf6012b785\*\*\*\* |Task run ID. |
|TaskId |String |7c9d82311f9246ccb24eae5457bd\*\*\*\* |The task ID. |
|Name |String |exec\-cmd |The task name. |
|Status |String |Succeeded |Task status. The tasks here do not include Agentless tasks.<br><br><br>* Queued: Pending execution.<br><br>* Running：Running.<br><br>* Timeout: Exceeding the time limit.<br><br>* Failed: Failed.<br><br>* Succeeded:  Success.<br><br>* Canceled: Canceled. |
|CreateTime |String |2024\-04\-07T11:59:08+08:00 |Task creation time. |
|UpdateTime |String |2024\-04\-07T11:59:08+08:00 |Task last updated time. |
|StartTime |String |2024\-04\-07T11:59:08+08:00 |The task start time. |
|FinishTime |String |2024\-04\-07T11:59:08+08:00 |The task end time. |
|Steps |Array of [TaskRunStep](https://docs.byteplus.com/en/docs/292/73431#taskrunstep) |\- |The details of the execution steps in the task |
|CustomPhase |String |Waiting |Execution status of agentless tasks, which currently include manual checkpoint, application deployment, Kubernetes image upgrade, and Kubernetes batch release. Optional values are:<br><br><br>* Waiting: Pending.<br><br>* Failed: Failed.<br><br>* Succeeded: Success.<br><br>* Running：In progress.<br><br>* Approved: Agree.<br><br>* Rejected: Rejected.<br><br>* Canceled: Canceled. |
|CustomContent |String | |Custom content for Agentless tasks provided by the user. |


<span id="taskrunstep"></span>
### TaskRunStep


|**Parameter** |**Type** |**Sample Value** |**Description** | |
|---|---|---|---|---|
|Name |String |git\-clone\-0 |Step name. | |
|Status |String |Succeeded |Step status：<br><br><br>* NotStart：Not started.<br><br>* Running：In progress.<br><br>* Succeeded：Success.<br><br>* Failed：Failed. | |
|LogUri |String |https://cp\-v2.tos\-cn\-beijing.volces.com/v2/log/7815d4783edc47c5bbd7df024ab\*\*\*\* |The step log download link. | |
|Version |String |v2 |Step log version (default: v2). | |
|LogStatus |String |Finished |Step log status<br><br><br>* Running: Collecting logs.<br><br>* Finished: Log collection completed.<br><br>* Synced: Log synchronization completed. | |
|StartTime |String |2023\-05\-01T12:00:00+08:00 |The step start time. | |
|FinishTime |String |2023\-05\-01T12:01:00+08:00 |The step end time. | |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "202404071710430739950998FB2847****",
        "Action": "ListTaskRuns",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Items": [
            {
                "Id": "230643959e41493d9baf6012b785****",
                "TaskId": "7c9d82311f9246ccb24eae5457bd****",
                "Name": "exec-cmd",
                "Status": "Succeeded",
                "CreateTime": "2024-04-07T11:59:08+08:00",
                "UpdateTime": "2024-04-07T11:59:17+08:00",
                "Steps": [
                    {
                        "Name": "git-clone-0",
                        "Status": "Succeeded",
                        "LogUri": "",
                        "StartTime": "2024-04-07T11:59:12+08:00",
                        "FinishTime": "2024-04-07T11:59:17+08:00",
                        "Version": "v2",
                        "LogStatus": "Synced"
                    },
                    {
                        "Name": "exec-cmd",
                        "Status": "Succeeded",
                        "LogUri": "",
                        "StartTime": "2024-04-07T11:59:17+08:00",
                        "FinishTime": "2024-04-07T11:59:17+08:00",
                        "Version": "v2",
                        "LogStatus": "Synced"
                    }
                ],
                "StartTime": "2024-04-07T11:59:08+08:00",
                "FinishTime": "2024-04-07T11:59:17+08:00",
                "CustomPhase": "",
                "CustomContent": ""
            }
        ],
        "PageSize": 10,
        "PageNumber": 1,
        "TotalCount": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API does not currently have dedicated error codes. If an exception is returned when calling the API, refer to [Public error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
