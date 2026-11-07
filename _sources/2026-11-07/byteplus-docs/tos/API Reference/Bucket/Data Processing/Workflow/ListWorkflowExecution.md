---
title: "ListWorkflowExecution"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/ListWorkflowExecution"
---

<span id="d22d774f"></span>
## Description

This interface lists all workflow execution records under the current account.

<span id="c55d3cd1"></span>
## Notes

None.

<span id="6928c308"></span>
## Request syntax

```Plain
GET /?workflow_execution&states=success&order_by_time=asc HTTP/1.1
Host: bucketname.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="ce23426a"></span>
## Request parameters and headers 


|**Field name** |**Location** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|---|
|workflow_execution |Query |String |Yes |\- |Represents a special identifier for the ListWorkflowExecution request. |
|workflow_id |Query |String |No |1840df030b38571c52470001b393c48b\*\*\*\* |Workflow execution record ID. |
|start_time |Query |String |No |2025\-05\-19T16:31:29+08:00 |Workflow execution start time. |
|end_time |Query |String |No |2025\-05\-19T16:31:30+08:00 |Workflow execution end time. |
|state |Query |String |No |All |Status of workflow execution, with the following possible values:<br><br><br>* `all`: all execution records.<br><br>* `success`: records that executed successfully.<br><br>* `failed`: records that failed to execute.<br><br>* `running`: records currently executing.<br><br>* `cancel`: records that have been canceled. |
|order_by_time |Query |String |No |desc |Workflow execution record display order is explained as follows:<br><br><br>* `desc`: in descending order of time.<br><br>* `asc`: in ascending order of time. |
|page_size |Query |String |No |3 |Page size. |
|page_token |Query |String |No |1840df030b38571c52470001b393c48b\*\*\*\* |Query start position. |


<span id="6527ddbc"></span>
## Request body elements

No elements are used.

<span id="985e1893"></span>
## Response headers

The response contains common headers. For more information, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="06f8c026"></span>
## Response body elements


|**Field name** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Items |Content |\- |Execution record information. |
|ExecutionID |String |1840df030b38571c52470001b393c48b\*\*\*\* |Execution record ID.<br><br>Parent node: Items |
|RequestID |String |\- |The request ID.<br><br>Parent node: Items |
|Object |String |bbb/sample.wav |Workflow source file name.<br><br>Parent node: Items |
|Workflow |Content |\- |Workflow information.<br><br>Parent node: Items |
|ID |String |my\-wf\-rule\-1 |Name of the workflow.<br><br>Parent node: Workflow |
|Enabled |String |true |Workflow status. The options are as follows:<br><br><br>* `true`: Enable the workflow. Once an object is uploaded to the specified path, the workflow executes automatically.<br><br>* `false`: Disable the workflow.<br><br><br>Parent node: Workflow |
|Prefix |String |bbb/ |Path bound to the workflow.<br><br>Uploading files to this path triggers the workflow execution. If unspecified, the entire bucket is bound, and uploading files to the bucket triggers the workflow execution.<br><br>Parent node: Workflow |
|ExtFilter |Content |\- |media type.<br><br>parent node: Workflow |
|AudioExts |String |wav |Media type.<br><br>Only this media type can trigger workflow execution. Currently, only the value `wav` is supported.<br><br>Parent node: ExtFilter |
|Topology |String |1 |Template names included in the workflow.<br><br>Parent node: Workflow |
|Operations |Content |\- |Template information.<br><br>Parent node: Workflow |
|AudioTranscode |Content |\- |Audio transcoding template information.<br><br>Parent node: Operations |
|OperationID |String |my\-op\-1 |Name of the workflow template.<br><br>Parent node: AudioTranscode |
|Format |String |mp3 |Transcoding output format, currently only supports `mp3`.<br><br>Parent node: AudioTranscode |
|Bitrate |Number |128000 |Transcode bitrate, currently only supports the value `128000`.<br><br>Parent node: AudioTranscode |
|Output |Content |\- |File storage location.<br><br>Parent node: AudioTranscode |
|Region |String |cn\-beijing |Region where the transcoded audio file is stored.<br><br>Parent node: Output |
|Bucket |String |test |The storage bucket for transcoded audio files.<br><br>Parent node: Output |
|Object |String |data.mp3 |Name of the transcoded audio file.<br><br>Parent node: Output |
|State |String |Success |The status of the workflow execution.<br><br>Parent node: Items |
|CreateTime |String |2025\-05\-19T16:31:29+08:00 |Workflow creation time.<br><br>Parent node: Items |
|StartTime |String |2025\-05\-19T16:31:29+08:00 |Workflow execution start time.<br><br>Parent node: Items |
|EndTime |String |2025\-05\-19T16:31:30+08:00 |Workflow execution end time.<br><br>Parent node: Items |
|Tasks |Content |\- |Workflow template execution information.<br><br>Parent node: Items |
|Type |String |AudioTranscode |Workflow template type.<br><br>Parent node: Tasks |
|JobID |String |1840e07ea084b82408820001f48e6010\*\*\*\*\-0 |workflow task ID.<br><br>parent node: Tasks |
|OperationID |String |my\-op\-1 |Workflow template name.<br><br>Parent node: Tasks |
|State |String |Success |Workflow template execution status.<br><br>Parent node: Tasks |
|CreateTime |String |2025\-05\-19T16:31:29+08:00 |Workflow template creation time.<br><br>Parent node: Tasks |
|StartTime |String |2025\-05\-19T16:31:29+08:00 |Workflow template execution start time.<br><br>Parent node: Tasks |
|EndTime |String |2025\-05\-19T16:31:30+08:00 |workflow template execution end time.<br><br>parent node: Tasks |
|Code |String |0 |Error code.<br><br>Parent node: Tasks |
|Message |String |\- |Error message.<br><br>Parent node: Tasks |
|NextPageToken |String |\- |Position of the next page data. |


<span id="4839aaba"></span>
## Sample request

```Plain
GET /?workflow_execution&states=success&order_by_time=asc HTTP/1.1
Host: bucketname.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="b1ab2911"></span>
## Sample response

```Plain
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: 643
{
    "Items": [
        {
            "ExecutionID": "1840df030b38571c52470001b393c48b****",
            "RequestID": "",
            "Object": "bbb/sample.wav",
            "Workflow": {
                "ID": "my-wf-rule-1",
                "Enabled": true,
                "Prefix": "bbb/",
                "ExtFilter": {
                    "AudioExts": [
                        "wav"
                    ]
                },
                "Topology": [
                    [
                        "my-op-1"
                    ]
                ],
                "Operations": {
                    "AudioTranscode": [
                        {
                            "OperationID": "my-op-1",
                            "Format": "mp3",
                            "Bitrate": 128000,
                            "Output": {
                                "Region": "cn-beijing",
                                "Bucket": "bbb",
                                "Object": "123.mp3"
                            }
                        }
                    ]
                }
            },
            "State": "Success",
            "CreateTime": "2025-05-19T16:04:19+08:00",
            "StartTime": "2025-05-19T16:04:19+08:00",
            "EndTime": "2025-05-19T16:04:19+08:00",
            "Tasks": [
                {
                    "Type": "AudioTranscode",
                    "JobID": "1840df030b38571c52470001b393c48b****-0",
                    "OperationID": "my-op-1",
                    "State": "Success",
                    "CreateTime": "2025-05-19T16:04:19+08:00",
                    "StartTime": "2025-05-19T16:04:19+08:00",
                    "EndTime": "2025-05-19T16:04:19+08:00",
                    "Error": "",
                    "Code": 0,
                    "Message": ""
                }
            ]
        },
        {
            "ExecutionID": "1840e07ea084b82408820001f48e6010****",
            "RequestID": "",
            "Object": "bbb/aaa/sample.wav",
            "Workflow": {
                "ID": "my-wf-rule-1",
                "Enabled": true,
                "Prefix": "bbb/",
                "ExtFilter": {
                    "AudioExts": [
                        "wav"
                    ]
                },
                "Topology": [
                    [
                        "my-op-1"
                    ]
                ],
                "Operations": {
                    "AudioTranscode": [
                        {
                            "OperationID": "my-op-1",
                            "Format": "mp3",
                            "Bitrate": 128000,
                            "Output": {
                                "Region": "cn-beijing",
                                "Bucket": "bbb",
                                "Object": "123.mp3"
                            }
                        }
                    ]
                }
            },
            "State": "Success",
            "CreateTime": "2025-05-19T16:31:29+08:00",
            "StartTime": "2025-05-19T16:31:29+08:00",
            "EndTime": "2025-05-19T16:31:30+08:00",
            "Tasks": [
                {
                    "Type": "AudioTranscode",
                    "JobID": "1840e07ea084b82408820001f48e6010****-0",
                    "OperationID": "my-op-1",
                    "State": "Success",
                    "CreateTime": "2025-05-19T16:31:29+08:00",
                    "StartTime": "2025-05-19T16:31:29+08:00",
                    "EndTime": "2025-05-19T16:31:30+08:00",
                    "Error": "",
                    "Code": 0,
                    "Message": ""
                }
            ]
        }
    ],
    "NextPageToken": ""
}
```
