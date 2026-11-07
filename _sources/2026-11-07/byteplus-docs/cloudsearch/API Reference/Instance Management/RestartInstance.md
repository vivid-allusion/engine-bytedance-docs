---
title: "RestartInstance"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/RestartInstance"
---

Call RestartInstance to restart all nodes in an instance.

<span id="b6788e9b"></span>
## Precautions

During the instance restart process, some services become unavailable. We recommend that you restart your instance during off\-peak hours.

A normal restart requires the instance to be in a healthy state. If an index within the instance is in an unhealthy state, the restart cannot proceed. If you still want to restart the instance under this circumstance, a forced restart is required. However, performing a forced restart when the instance is in an unhealthy state may lead to the loss of some transmitted data or make the instance unavailable. Proceed with caution.

<span id="eddbaa76"></span>
## Request Description


* Request method: POST

* Request URL: /?Action=RestartInstance&Version=2023\-01\-01 HTTP/1.1


<span id="ed6acec7"></span>
## Request parameters

<span id="8e11177d"></span>
### Query


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`RestartInstance` |The action that you want to perform. Value: `RestartInstance`. |
|Version |String |Yes |`2023-01-01` |The version of the API. Value: `2023-01-01`. |


<span id="cad2d6fa"></span>
### Body


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |o\-00k\*\*\*o718 |The ID of the instance that you want to restart. |
|Force |Boolen |No |false |Whether it is a force restart. Default value: `false`. Valid values:<br><br><br>* true: It is a force restart.<br><br>* false: It is not a force restart. |


<span id="01e0eb45"></span>
## Response parameters


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |o\-00k\*\*\*o718 |The ID of the restarted instance. |
|TaskId |String |edc9bbcf802\*\*\*\*\*9a3abac9edde |The returned task ID. |


<span id="544851cd"></span>
## Sample request

```HTTP
POST https://open.ap-southeast-1.byteplusapi.com/?Action=RestartInstance&Version=2023-01-01
Content-Type: application/json
X-Date: 20231003T104027Z
Authorization: HMAC-SHA256 
Credential=AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZ****/20231003/ap-southeast-1/ESCloud/request, SignedHeaders=content-type;host;x-date, Signature=88dd0a9ea555d8609ec83eb46054b52f6cd4f79b8d5094fa784c66fa3f2b****
{
    "InstanceId": "o-00k***o718",
    "Force": false
}
```


<span id="8f31aca9"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2023102016********591F1A3437",
        "Action": "RestartInstance",
        "Version": "2023-01-01",
        "Service": "ESCloud",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "InstanceId": "o-00k****718",
        "TaskId": "edc9bbcf802*****9a3abac9edde"
    }
}
```
