---
title: "Terminate asynchronous tasks"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-terminate-asynchronous-tasks"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/terminate`

This API endpoint is used to actively cancel specified asynchronous tasks. After submitting an asynchronous task, if you no longer need the result or want to save computing resources, you can use this API to terminate tasks that are in the queue (Pending) or in Preparing stages.

## Usage limits

* Only supports canceling tasks in the `Pending` (queued) state or Preparing stages. Tasks that have reached a final state (`Completed` or `Failed`) cannot have their results changed through this API.

* Supports canceling most asynchronous tasks under AI MediaKit such as Video Tools, Editing Tools, and Audio Tools. It does not support Intelligent Editing (VCreative), Script Restoration, Video Explanation Generation, Chat API tasks, etc.

* Cancellation is performed on a "best\-effort" basis. If the underlying computing task has already started execution and cannot be physically interrupted, the AI MediaKit will mark it as canceled at the service layer, but momentary resource consumption may still occur.

* A single account supports up to 10 task cancellation requests per second by default.

* A single account has a default daily quota of 1,000 task cancellations.

## Request parameters

### Header

|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Please refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |

### Body

|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`task_ids` |String[] |Yes |`["amk-tool-enhance-video-36603392", "amk-tool-enhance-video-fast-987654"]` |A list of task IDs to be processed. A single request supports up to 10 task IDs. |

## Request example

```Bash
curl -X POST "https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/terminate" \
-H "Authorization: Bearer {YOUR_API_KEY}" \
-H "Content-Type: application/json" \
-d '{
    "task_ids": ["amk-tool-enhance-video-36603392", "amk-tool-enhance-video-fast-987654"]
}'
```

## Response parameters

The response body is a JSON object. The request identifier (`request_id`) is available in the HTTP response headers and can be used for troubleshooting.

|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the API request was successful:<br><br><br>* `true`: Request successful.<br><br>* `false`: Request failed; see the `error` field for the specific reason. |
|`result` |Object |The result object returned when the API request is successful (i.e., `success` is `true`). See [Result object](https://docs.byteplus.com/en/docs/25/125256#Result). |
|`error` |Object |The error details object returned when the API request fails (i.e., `success` is `false`). See [Error object](https://docs.byteplus.com/en/docs/25/125256#Error). |

### Result object

|Parameter |Type |Description |
|---|---|---|
|`terminated_tasks` |Object[] |A list of tasks that were successfully canceled. This includes tasks that were already in the canceled state. See [TerminatedTask object](https://docs.byteplus.com/en/docs/25/125256#TerminatedTask) for details. |
|`terminate_failed_tasks` |Object[] |A list of tasks that failed to be canceled. This includes cases where the task does not exist, there are no permissions, or the task status does not support cancellation. See [TerminateFailedTask object](https://docs.byteplus.com/en/docs/25/125256#TerminateFailedTask) for details. |

### TerminatedTask object

|Parameter |Type |Description |
|---|---|---|
|`task_id` |String |The unique identifier of the task. |

### TerminateFailedTask object

|Parameter |Type |Description |
|---|---|---|
|`task_id` |String |The unique identifier of the task. |
|`error` |Object |Details of the specific failure reason. See [Error object](https://docs.byteplus.com/en/docs/25/125256#Error). |

### Error object

|Parameter |Type |Description |
|---|---|---|
|`code` |String |The error code. For details, see [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`message` |String |A descriptive message of the error, useful for display or logging. |
|`type` |String |The type of error, such as `TaskError` for task execution errors or `ApiError` for API call errors. |

## Response examples

### Example 1: Batch cancellation success

```JSON
{
    "success": true,
    "result": {
        "terminated_tasks": [
            {
                "task_id": "amk-tool-video-highlights-llm-1782574345218"
            },
            {
                "task_id": "amk-tool-video-highlights-llm-1619113030146"
            }
        ],
        "terminate_failed_tasks": []
    }
}
```

### Example 2: Partial success and partial failure

```JSON
{
    "success": true,
    "result": {
        "terminated_tasks": [
            {
                "task_id": "amk-tool-video-highlights-llm-1782574345218"
            }
        ],
        "terminate_failed_tasks": [
            {
                "task_id": "amk-tool-enhance-video-1982171749890",
                "error": {
                    "code": "TaskOperationConflict",
                    "type": "Conflict",
                    "message": "task termination conflicts with its current state"
                }
            }
        ]
    }
}
```
