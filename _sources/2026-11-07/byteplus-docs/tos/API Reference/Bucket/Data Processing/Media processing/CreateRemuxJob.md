---
title: "CreateRemuxJob"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/CreateRemuxJob"
---

<span id="a180eac4"></span>
## Description

This interface processes audio and video files through remuxing.

<span id="4fa4202b"></span>
## Notes


* Audio and video remux tasks only support asynchronous processing (x\-tos\-async\-process mode).

* You must have `CreateMediaProcessJobs` permissions required for data processing.


<span id="ab3b6e8f"></span>
## Request syntax

```HTTP
POST /?job_type=Remux&media_jobs= HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Content-Type: application/json
Content-Length: <length>
Authorization: authorization string

{
    "Input": {
        "Object": "sample.mp4"
    },
    "RemuxConfig": {
        "Format": "mp4",
        "TranscodeIndex": 0,
        "AIGCMetadata": {
            "Label": "",
            "ContentProducer": "",
            "ProduceID": "",
            "ContentPropagator": "",
            "PropagateID": "",
            "ReservedCode1": "",
            "ReservedCode2": ""
        }
    },
    "Output": {
        "Region": "ap-southeast-1",
        "Bucket": "testbkt",
        "Object": "output.mp4"
    }
}  
```


<span id="0f91f283"></span>
## Request parameters and headers 

For common request headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Field name** |**Location** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|---|
|job_type |Query |String |Yes |Remux |Task type, the value is `Remux` only in remux scenarios. |
|media_jobs |Query |String |Yes |\- |Represents a unique identifier for media task requests. |


<span id="2a64f58c"></span>
## Request body elements


|**Field name** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|RemuxConfig |Container |Yes |\- |Specific configuration for the transmuxing task. |
|Format |String |Yes |mp4 |Audio and video container formats.<br><br>Supported:<br><br><br>* `mp4`<br><br>* `mkv`<br><br>* `avi`<br><br>* `mkv`<br><br>* `ts`<br><br>* `mp3`<br><br>* `aac`<br><br>* `flac`<br><br><br>Parent node: RemuxConfig |
|TranscodeIndex |String |No |0 |Stream number to process. Once specified, the output file will only retain the designated audio and video streams.<br><br>Process all streams by default.<br><br>Parent node: RemuxConfig |
|AIGCMetadata |Container |No |\- |AIGC metadata identifier content.<br><br><br>* Encoding format supports only `mp4` when not `nil`;<br><br>* All field lengths under AIGCMetadata are limited to 22,048 UTF\-8 characters, with character restrictions set to GB18030—2022 (ASCII) code points from 0x21 to 0x7E.<br><br><br>Parent node: RemuxConfig |
|Label |String |Yes |test_label |Generate synthetic label elements to indicate if the video is, may be, or is suspected to be AI\-generated synthetic content.<br><br>Parent node: AIGCMetadata |
|ContentProducer |String |Yes |test_content_producer |Generates an element for the synthesis service provider, containing the name or code of the video generation synthesis service provider.<br><br>Parent node: AIGCMetadata |
|ProduceID |String |Yes |test_produce_id |Content production identification element, representing the unique identifier assigned to the content by the video generation and synthesis service provider.<br><br>Parent node: AIGCMetadata |
|ContentPropagator |String |No |test_content_propagator |Content distribution provider element, representing the name or code of the video distribution service provider.<br><br>Parent node: AIGCMetadata |
|PropagateID |String |No |test_propagate_id |Content distribution ID element; the value is the unique ID assigned by the video service provider to this video.<br><br>Parent node: AIGCMetadata |
|ReservedCode1 |String |No |dGVzdF9yZXNlcnZlZF9jb2RlXzE= |Reserved field 1 contains user\-initiated security protection information to safeguard content and identify integrity. Must be base64 encoded before transmission.<br><br>Parent node: AIGCMetadata |
|ReservedCode2 |String |No |dGVzdF9yZXNlcnZlZF9jb2RlXzI= |Reserved field 2, containing information for user\-initiated security protection to safeguard content and identify integrity. The data must be transmitted after base64 encoding.<br><br>Parent node: AIGCMetadata |


<span id="45de9113"></span>
## Response headers

The response contains common headers. For more information, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="ef4545b2"></span>
## Response body elements


|**Field name** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Code |String |OK |Status code. |
|Message |String |Success |Request status information. |
|JobId |String |187919df106a49aa402300013e6ba5bf0593 |Audio and video transmuxing task ID. |


<span id="dce26f64"></span>
## Sample request

```HTTP
POST /?job_type=Remux&media_jobs= HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Content-Type: application/json
Content-Length: <length>
Authorization: authorization string

{
    "Input": {
        "Object": "sample.mp4"
    },
    "RemuxConfig": {
        "Format": "mp4",
        "TranscodeIndex": 0,
        "AIGCMetadata": {
            "Label": "test_label",
            "ContentProducer": "test_content_producer",
            "ProduceID": "test_produce_id",
            "ContentPropagator": "test_content_propagator",
            "PropagateID": "test_propagate_id",
            "ReservedCode1": "dGVzdF9yZXNlcnZlZF9jb2RlXzE=",
            "ReservedCode2": "dGVzdF9yZXNlcnZlZF9jb2RlXzI="
        }
    },
    "Output": {
        "Region": "ap-southeast-1",
        "Bucket": "testbkt",
        "Object": "output.mp4"
    }
}  
```


<span id="7a0748ba"></span>
## Sample response

```HTTP
HTTP/1.1 200 OK
x-tos-id-2: f91b0c03a01300c1-a444ed0        
x-tos-request-id: f91b0c03a01300c1-a444ed0            
Date: Fri, 30 Jul 2021 06:45:39 GMT
server: TosServer
Content-Length: 80

{
    "Code": "OK",
    "Message": "Success",
    "JobId": "187919df106a49aa402300013e6ba5bf0593"
}
```
