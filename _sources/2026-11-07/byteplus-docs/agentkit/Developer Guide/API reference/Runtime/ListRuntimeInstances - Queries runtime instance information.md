---
title: "ListRuntimeInstances - Queries runtime instance information"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ListRuntimeInstances_-_Queries_runtime_instance_information"
---

Query the runtime instance information.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|cdAt6a">必选</span> `Sample value: ListRuntimeInstances`

The action that you want to perform. Value: ListRuntimeInstances.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|idGaCk">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**RuntimeId ** <span data-label="purple">string </span><span data-api-tag="require|cP1Faq">必选</span> `Sample value: r-ye7agye1a8cr38iu****`

ID of the runtime.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstanceItems ** <span data-label="purple">object[] </span>`Sample value: --`

The instance details.


**AliasName ** <span data-label="purple">string </span>`Sample value: name1`

The alias of the instance.



**RuntimeId ** <span data-label="purple">string </span>`Sample value: r-ye7agye1a8cr38iu****`

ID of the runtime.



**CreateTime ** <span data-label="purple">string </span>`Sample value: 2024-06-25 11:17:11.492301904 +0800 CST`

The time when the instance is created.



**InstanceName ** <span data-label="purple">string </span>`Sample value: 1jsq6bcn-630g8l8****`

The instance name.



**InstanceStatus ** <span data-label="purple">string </span>`Sample value: Ready`

The instance status. Value:


* Starting: Starting.

* Ready: Ready.

* Failed: Failed.

* Terminating: Terminating.

* Unknown: Unknown status.



**RevisionNumber ** <span data-label="purple">integer </span>`Sample value: 1`

The version number of the instance.




**RunningInstance ** <span data-label="purple">integer </span>`Sample value: 10`

The number of running instances.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=ListRuntimeInstances&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "RuntimeId": "r-ye7agye1a8cr38iu****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202601131535214BBED****",
    "Action": "ListRuntimeInstances",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "InstanceItems": [
      {
        "RuntimeId": "r-ye7agye1a8cr38iu****",
        "InstanceName": "xxxxx",
        "RevisionNumber": 1,
        "InstanceStatus": "Ready",
        "CreateTime": "2026-01-13 02:26:51.5812395 +0000 UTC"
      }
    ],
    "RunningInstance": 1,
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.RuntimeId |The required parameter RuntimeId is not supplied. |The parameter RuntimeId cannot be empty. |
