---
title: "RestartNode"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/RestartNode"
---

Call RestartNode to restart a specified member node in an instance.

<span id="484dae45"></span>
## Precautions

When you restart a member node of an instance, the entire instance enters the **Restarting** state. During this process, some services become unavailable. We recommend that you restart member nodes of your instance during off\-peak hours.

<span id="09ddd8fc"></span>
## Request Description


* Request method: POST

* Request URL: /?Action=RestartNode&Version=2023\-01\-01 HTTP/1.1


<span id="831f7c40"></span>
## Request parameters

<span id="32d25b17"></span>
### Query


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`RestartNode` |The action that you want to perform. Value: `RestartNode`. |
|Version |String |Yes |`2023-01-01` |The version of the API. Value: `2023-01-01`. |


<span id="8b8b4bb8"></span>
### Body


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |o\-00k\*\*\*o718 |The ID of the instance whose node you want to restart. |
|NodeName |String |Yes |es\-master\-00\*\*\*\*o718\-0 |The ID of the member node that you want to restart.<br><br>To get the member node ID, call [DescribeInstanceNodes](https://docs.byteplus.com/docs/cloudsearch/DescribeInstanceNodes). |
|Force |Boolen |No |false |Whether it is a force restart. Default value: `false`. Valid values:<br><br><br>* true: It is a force restart.<br><br>* false: It is not a force restart.<br><br><br>A forced restart may lead to the loss of some transmitted data or make the instance unavailable. Proceed with caution. |


<span id="ce8f9cfc"></span>
## Response parameters


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|NodeName |String |es\-master\-00\*\*\*\*o718\-0 |The name of the restarted node. |
|InstanceId |String |o\-00k\*\*\*o718 |The ID of the instance to which the restarted node belongs. |
|TaskId |String |2e132b847\*\*\*\*7cd1451e49a |The returned task ID. |


<span id="7ff1b2f2"></span>
## Sample request

```HTTP
POST https://open.ap-southeast-1.byteplusapi.com/?Action=RestartNode&Version=2023-01-01
Content-Type: application/json
X-Date: 20231003T104027Z
Authorization: HMAC-SHA256 
Credential=AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZ****/20231003/ap-southeast-1/ESCloud/request, SignedHeaders=content-type;host;x-date, Signature=88dd0a9ea555d8609ec83eb46054b52f6cd4f79b8d5094fa784c66fa3f2b****
{
    "InstanceId": "o-00k***o718",
    "NodeName": "es-master-00****o718-0",
    "Force": false
}
```


<span id="39297b8a"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2023102016374***BA71470AA7B7",
        "Action": "RestartNode",
        "Version": "2023-01-01",
        "Service": "ESCloud",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "NodeName": "es-master-00k***718-0",
        "InstanceId": "o-00k****718",
        "TaskId": "2e132b847****7cd1451e49a"
    }
}
```
