---
title: "GetWorkflow"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetWorkflow"
---

## Description

This API retrieves workflow configuration information.

## Notes

None.

## Request syntax

```JSON
GET /?workflow HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```

## Request parameters and headers

|**Field name** |**Location** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|---|
|workflow |Query |String |Yes |\- |Special identifier representing the GetWorkflow request. |

## Request body elements

No elements are used.

## Response headers

The response contains common headers. For more information, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

## Response body elements

|**Field name** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Rules |Content |\- |Workflow configuration information. |
|ID |String |my\-wf\-rule\-1 |Name of the workflow.<br><br>Parent node: Rules |
|Enabled |String |true |Enable this workflow. The value explanations are as follows:<br><br><br>* `true`: Enable the workflow; after uploading the object to the specified path, the workflow will execute automatically.<br><br>* `false`: Stop the workflow.<br><br><br>Parent node: Rules |
|Prefix |String |my\-audio\-dir/ |Path bound to the workflow.<br><br>The workflow triggers only when files upload to this path. If not specified, the binding applies to the entire bucket, triggering the workflow whenever files upload to the bucket.<br><br>Parent node: Rules |
|ExtFilter |Content |\- |Media type.<br><br>Parent node: Rules |
|AudioExts |String |wav |Media type.<br><br>Only media of this type can trigger the workflow; currently, only the value `wav` is supported.<br><br>Parent node: ExtFilter |
|Topology |String |my\-op\-1 |Template names included in the workflow. |
|Operations |Content |\- |Template information.<br><br>Parent node: Rules |
|AudioTranscode |Content |\- |Audio transcoding template information.<br><br>Parent node: Operations |
|OperationID |String |my\-op\-1 |Workflow template name.<br><br>Parent node: AudioTranscode |
|Format |String |mp3 |Transcoding output format currently only supports the value `mp3`.<br><br>Parent node: AudioTranscode |
|Bitrate |Number |128000 |Transcoding bitrate, currently only supports the value `128000`.<br><br>Parent node: AudioTranscode |
|Output |Content |\- |File storage location.<br><br>Parent node: AudioTranscode |
|Region |String |cn\-beijing |Region where the transcoded audio files are stored.<br><br>Parent node: Output |
|Bucket |String |my\-bucket |Bucket for storing transcoded audio files.<br><br>Parent node: Output |
|Object |String |test.mp3 |Name of the transcoded audio file.<br><br>Parent node: Output |

## Sample request

```JSON
GET /?workflow HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```

## Sample response

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: 643

{
  "Rules": [
    {
      "ID": "my-wf-rule-1",
      "Status": "Enabled",
      "Prefix": "my-audio-dir/",
      "ExtFilter": {
        "AudioExts": [ "wav" ]
      },
      "Topology": [
        [ "my-op-1" ]
      ],
      "Operations": {
        "AudioTranscode": [
          {
            "OperationID": "my-op-1",
            "Format": "mp3",
            "Bitrate": 128000,
            "Output": {
              "Region": "cn-beijing",
              "Bucket": "my-bucket",
              "Object": "${InputPath}/${InputName}-${RunID}.mp3"
            }
          }
        ]
      }
    }
  ]
}
```
