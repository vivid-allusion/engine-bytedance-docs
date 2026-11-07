---
title: "CreateWorkflow"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/CreateWorkflow"
---

<span id="bf222414"></span>
## Description

This interface creates a workflow for audio transcoding.

<span id="151f75fb"></span>
## Notes


* Currently, only workflows for audio transcoding are supported.

* A single bucket workflow can have up to 1000 rules. The total size of all rules serialized in JSON cannot exceed 20KB.


<span id="1c706cfb"></span>
## Request syntax

```Plain
PUT /?workflow HTTP/1.1
Host: bucketname.tos-cn-beijing.volces.com
Date: Mon, 19 May 2025 08:02:50 GMT
Authorization: authorization string

{
  "Rules": [
    {
      "ID": "my-wf-rule-1",
      "Enabled": true,
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
              "Object": "test.mp3"
            }
          }
        ]
      }
    }
  ]
}
```


<span id="88456bc0"></span>
## Request parameters and headers 

For common request headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Field name** |**Location** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|---|
|workflow |Query |String |Yes |\- |Represents the special identifier for the CreateWorkflow request. |


<span id="09efc429"></span>
## Request body elements


|**Field name** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Rules |Content |Yes |\- |Workflow configuration information. |
|ID |String |Yes |my\-wf\-rule\-1 |Name of the workflow, described as follows:<br><br><br>* Length must not exceed 255.<br><br>* Name must be unique.<br><br><br>Parent node: Rules |
|Enabled |String |Yes |true |Enable this workflow. The value descriptions are as follows:<br><br><br>* `true`: enable the workflow. Once the object is uploaded to the specified path, the workflow will run automatically.<br><br>* `false`: stop the workflow.<br><br><br>parent node: Rules |
|Prefix |String |Yes |my\-audio\-dir/ |Path bound to the workflow.<br><br>Uploading files to this path triggers the workflow execution. If not specified, the entire bucket is bound, and uploading files to the bucket triggers the workflow execution.<br><br>Parent node: Rules |
|ExtFilter |Content |Yes |\- |Media type.<br><br>Parent node: Rules |
|AudioExts |Content |Yes |wav |media type,<br><br>only this media type can trigger workflow execution; currently only supports the value `wav`.<br><br>Parent node: ExtFilter |
|Topology |String |Yes |my\-op\-1 |Template names included in the workflow. |
|Operations |Content |Yes |\- |Template information.<br><br>Parent node: Rules |
|AudioTranscode |Content |Yes |\- |Audio transcode template information.<br><br>Parent node: Operations |
|OperationID |String |Yes |my\-op\-1 |Name of the workflow template.<br><br>Parent node: AudioTranscode |
|Format |String |Yes |mp3 |Transcode output format, currently only supports `mp3`.<br><br>Parent node: AudioTranscode |
|Bitrate |Number |Yes |128000 |Transcoding bitrate, currently only supports the value `128000`.<br><br>Parent node: AudioTranscode |
|Output |Content |Yes |\- |Location where files are stored.<br><br>Parent node: AudioTranscode |
|Region |String |Yes |cn\-beijing |Region where the transcoded audio file is stored<br><br>Parent node: Output |
|Bucket |String |Yes |my\-bucket |Bucket for storing transcoded audio files.<br><br>Parent node: Output |
|Object |String |Yes |test.mp3 |Name of the transcoded audio file.<br><br>Parent node: Output |


<span id="a59a5447"></span>
## Response headers

The response contains common headers. For more information, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="b58fc0dd"></span>
## Response body elements

Sample response

<span id="0e2e4eaf"></span>
## Sample request

```Plain
PUT /?workflow HTTP/1.1
Host: bucketname.tos-cn-beijing.volces.com
Date: Mon, 19 May 2025 08:02:50 GMT
Authorization: authorization string
{
  "Rules": [
    {
      "ID": "my-wf-rule-1",
      "Enabled": true,
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
              "Object": "test.mp3"
            }
          }
        ]
      }
    }
  ]
}
```


<span id="18bf4250"></span>
## Sample response

```Plain
HTTP/1.1 200 OK
x-tos-id-2: f91b0c03a01300c1-a444cd0        
x-tos-request-id: f91b0c03a01300c1-a444cd0            
Date: Mon, 19 May 2025 08:02:50 GMT
server: TosServer
Content-Length: 0
```
