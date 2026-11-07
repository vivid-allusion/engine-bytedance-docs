---
title: "GetAIGCMetadata"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetAIGCMetadata"
---

<span id="a180eac4"></span>
## Description

This interface extracts AIGC metadata from audio and video.

<span id="4fa4202b"></span>
## Notes

Extracting AIGC metadata from audio and video only supports synchronous processing (x\-tos\-process mode).

<span id="ab3b6e8f"></span>
## Request syntax

```HTTP
GET /sample.mp4?x-tos-process=video/aigcmetadata HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: <authorization_string>
```


<span id="0f91f283"></span>
## Request parameters and headers 

For common request headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Field name** |**Location** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|---|
|x\-tos\-process |Query |String |Yes |video/aigcmetadata |Special identifier representing the request to extract AIGC meta\-information from audio and video. |


<span id="2a64f58c"></span>
## Request body elements

No elements are used.

<span id="45de9113"></span>
## Response headers

The response contains common headers. For more information, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="ef4545b2"></span>
## Response body elements


|**Field name** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|AIGC |String |\- |AIGC metadata identification content. |
|Label |String |test_label |Generate composite label elements to indicate that the video is, may be, or is suspected to be artificially generated with AI\-based synthesis attributes.<br><br>Parent node: AIGC |
|ContentProducer |String |test_content_producer |Generate composite service provider element containing the name or code of the video generation service provider.<br><br>Parent node: AIGC |
|ProduceID |String |test_produce_id |The content production ID element is the unique ID assigned by the video generation and synthesis service provider to the content.<br><br>Parent node: AIGC |
|ContentPropagator |String |test_content_propagator |The content distribution service provider element is the name or code of the video distribution service provider.<br><br>Parent node: AIGC |
|PropagateID |String |test_propagate_id |The content distribution ID element is the unique ID assigned by the video distribution service provider to the video.<br><br>Parent node: AIGC |
|ReservedCode1 |String |dGVzdF9yZXNlcn\*\*\*\*9jb2RlXzE= |Reserved field 1 contains user\-initiated security protection information to safeguard content and identify integrity. Must be passed in after base64 encoding.<br><br>Parent node: AIGC |
|ReservedCode2 |String |dGVzdF9yZXNlcn\*\*9jb2RlXzI= |Reserved field 2, containing user\-initiated security protection information to safeguard content and identity integrity. The data must be encoded in base64 before being passed in.<br><br>Parent node: AIGC |


<span id="dce26f64"></span>
## Sample request

```HTTP
GET /sample.mp4?x-tos-process=video/aigcmetadata HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: <authorization_string>
```


<span id="7a0748ba"></span>
## Sample response

```HTTP
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 666
Connection: keep-alive
Date: Fri, 10 Mar 2025 09:45:46 GMT

{
    "AIGC": {
        "Label": "test_label",
        "ContentProducer": "test_content_producer",
        "ProduceID": "test_produce_id",
        "ReservedCode1": "dGVzdF9yZXNlcn****9jb2RlXzE=",
        "ContentPropagator": "test_content_propagator",
        "PropagateID": "test_propagate_id",
        "ReservedCode2": "dGVzdF9yZXNlcn****9jb2RlXzI="
    }
}
```
