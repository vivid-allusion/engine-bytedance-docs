---
title: "GetRuntimeWebshellEndpoint - Obtains Webshell URL of a runtime instance"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetRuntimeWebshellEndpoint_-_Obtains_Webshell_URL_of_a_runtime_instance"
---

Obtain the Webshell URL of a runtime instance.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=GetRuntimeWebshellEndpoint&groupName=Runtime&serviceCode=agentkit&version=2025-10-30)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|VD5dzI">必选</span> `Sample value: GetRuntimeWebshellEndpoint`

The action that you want to perform. Value: GetRuntimeWebshellEndpoint.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|qlA3aq">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**RuntimeId ** <span data-label="purple">string </span><span data-api-tag="require|zEjSQG">必选</span> `Sample value: r-ye7agye1a8cr38iu****`

ID of the runtime.



**InstanceName ** <span data-label="purple">string </span><span data-api-tag="require|tNwQGh">必选</span> `Sample value: 1jsq6bcn-630g8l8****`

The instance name.

It can be obtained via [ListRuntimeInstances](https://docs.byteplus.com/en/docs/agentkit/ListRuntimeInstances_-_Queries_runtime_instance_information), and the instance must be in Ready status.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Endpoint ** <span data-label="purple">string </span>`Sample value: https://sf6u1gofl140096v5****.apigateway-ap-southeast-1.volceapi.com/terminal?faasInstanceName=vefaas-ano****-sandbox\u0026Authorization=kOh_BLxJ5IfRi572QL6GlliEeL4bX_9****`

The Webshell endpoint URL of the runtime instance.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com?Action=GetRuntimeWebshellEndpoint&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
  "RuntimeId": "r-ye7agye1a8cr38iu****",
  "InstanceName": "1jsq6bcn-630g8l8****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20260722101146160192149018500291",
    "Action": "GetRuntimeWebshellEndpoint",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Endpoint": "https://sf6u1gofl140096v5****.apigateway-ap-southeast-1.volceapi.com/terminal?faasInstanceName=vefaas-ano****-sandbox\\u0026Authorization=kOh_BLxJ5IfRi572QL6GlliEeL4bX_9****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.InstanceName |The required parameter InstanceName is not supplied. |The instance name cannot be empty. |
|400 |MissingParameter.RuntimeId |The required parameter RuntimeId is not supplied. |The parameter RuntimeId cannot be empty. |
|404 |InvalidAgentKitRuntime.NotFound |The specified AgentKitRuntime does not exist. |The corresponding runtime instance cannot be found. |
