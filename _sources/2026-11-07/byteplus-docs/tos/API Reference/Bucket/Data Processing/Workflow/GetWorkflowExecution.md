---
title: "GetWorkflowExecution"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetWorkflowExecution"
---

<span id="c6a76c6c"></span>
## Description

This interface queries the execution records of the specified workflow.

<span id="05d9c105"></span>
## Notes

None.

<span id="26054d0f"></span>
## Request syntax

```Plain
GET /?workflow_execution=1840df030b38571c52470001b393c48b**** HTTP/1.1
Host: bucketname.tos-cn-beijing.volces.com
Date: Mon, 19 May 2025 09:53:34 GMT
Authorization: authorization string
```


<span id="63d22373"></span>
## Request parameters and headers 


|**Field name** |**Location** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|---|
|workflow_execution |Query |String |Yes |1840df030b38571c52470001b393c48b\*\*\*\* |Workflow execution record ID. |


<span id="b6b94ccd"></span>
## Request body elements

No elements are used.

<span id="3b5bd613"></span>
## Response headers

The response contains common headers. For more information, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="b271ffcb"></span>
## Response body elements


|**Field name** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Items |Content |\- |Execution record information. |
|ExecutionID |String |1840df030b38571c52470001b393c48b\*\*\*\* |execution record ID.<br><br>parent node: Items |
|RequestID |String |\- |The request ID.<br><br>Parent node: Items |
|Object |String |bbb/sample.wav |Name of the workflow source file.<br><br>Parent node: Items |
|Workflow |Content |\- |Workflow information.<br><br>Parent node: Items |
|ID |String |my\-wf\-rule\-1 |The name of the workflow.<br><br>Parent node: Workflow |
|Enabled |String |true |Workflow status. The options are as follows:<br><br><br>* `true`: enables the workflow; after uploading an object to the specified path, the workflow will execute automatically.<br><br>* `false`: stops the workflow.<br><br><br>Parent node: Workflow |
|Prefix |String |bbb/ |Path bound to the workflow.<br><br>The workflow triggers only when files upload to this path. If unspecified, the entire bucket is bound, so uploading files to the bucket triggers the workflow.<br><br>Parent node: Workflow |
|ExtFilter |Content |\- |Media type.<br><br>Parent node: Workflow |
|AudioExts |String |wav |Media type.<br><br>Only media of this type can trigger the workflow execution. Currently, only the value `wav` is supported.<br><br>Parent node: ExtFilter |
|Topology |String |my\-op\-1 |Template names included in the workflow.<br><br>Parent node: Workflow |
|Operations |Content |\- |Template information.<br><br>Parent node: Workflow |
|AudioTranscode |Content |\- |Audio transcoding template information.<br><br>Parent node: Operations |
|OperationID |String |my\-op\-1 |Workflow template name.<br><br>Parent node: AudioTranscode |
|Format |String |mp3 |Transcode output format, currently only supports the value `mp3`.<br><br>Parent node: AudioTranscode |
|Bitrate |Number |128000 |Transcoding bitrate, currently only supports the value `128000`.<br><br>Parent node: AudioTranscode |
|Output |Content |\- |File storage location.<br><br>Parent node: AudioTranscode |
|Region |String |cn\-beijing |Region where the transcoded audio file is stored.<br><br>Parent node: Output |
|Bucket |String |test |bucket storing the transcoded audio file.<br><br>parent node: Output |
|Object |String |data.mp3 |Name of the transcoded audio file.<br><br>Parent node: Output |
|State |String |Success |Status of the workflow execution.<br><br>Parent node: Items |
|CreateTime |String |2025\-05\-19T16:31:29+08:00 |Workflow creation time.<br><br>Parent node: Items |
|StartTime |String |2025\-05\-19T16:31:29+08:00 |Workflow execution start time.<br><br>Parent node: Items |
|EndTime |String |2025\-05\-19T16:31:30+08:00 |Workflow execution end time.<br><br>Parent node: Items |
|Tasks |Content |\- |Workflow template execution information.<br><br>Parent node: Items |
|Type |String |AudioTranscode |Workflow template type.<br><br>Parent node: Tasks |
|JobID |String |1840e07ea084b82408820001f48e6010\*\*\*\*\-0 |Workflow task ID.<br><br>Parent node: Tasks |
|OperationID |String |my\-op\-1 |workflow template name.<br><br>parent node: Tasks |
|State |String |Success |Workflow template execution status.<br><br>Parent node: Tasks |
|CreateTime |String |2025\-05\-19T16:31:29+08:00 |Workflow template creation time.<br><br>Parent node: Tasks |
|StartTime |String |2025\-05\-19T16:31:29+08:00 |Workflow template execution start time.<br><br>Parent node: Tasks |
|EndTime |String |2025\-05\-19T16:31:30+08:00 |Workflow template execution end time.<br><br>Parent node: Tasks |
|Code |String |0 |Error code.<br><br>Parent node: Tasks |
|Message |String |\- |Error message.<br><br>Parent node: Tasks |
|NextPageToken |String |1840df030b38571c52470001b393c48b\*\*\*\* |Position of the next page data. |


<span id="5b63d334"></span>
## Sample request

```Plain
GET /?workflow_execution=1840df030b38571c52470001b393c48b**** HTTP/1.1
Host: bucketname.tos-cn-beijing.volces.com
Date: Mon, 19 May 2025 09:53:34 GMT
Authorization: authorization string
```


<span id="a954a471"></span>
## Sample response

```Plain
HTTP/1.1 200 OK
Date: Mon, 19 May 2025 09:53:34 GMT
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
                    "Code": 0,
                    "Message": ""
                }
            ]
        }
    ],
    "NextPageToken": ""
}
```
