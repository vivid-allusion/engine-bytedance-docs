---
title: "ReleaseRuntime - Updates runtime version"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ReleaseRuntime_-_Updates_runtime_version"
---

You can call this operation to update the version of a runtime.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action**<span data-label="purple"> string</span> <span data-api-tag="require|ZqZJMs">必选</span> `Sample value: ReleaseRuntime`

The action that you want to perform. Value: ReleaseRuntime.



**Version** <span data-label="purple">string </span><span data-api-tag="require|9Xht0M">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**Description ** <span data-label="purple">string </span>`Optional` `Sample value: version-new`

Version description.



**RollingStep ** <span data-label="purple">integer </span>`Optional` `Sample value: 10`

Grey release step size.


* Value range: 0–100.

* Unit: %.



**RuntimeId ** <span data-label="purple">string </span><span data-api-tag="require|24Zo7T">必选</span> `Sample value: r-ye7agye1a8cr38iu****`

ID of the runtime.



**TargetTrafficWeight ** <span data-label="purple">integer </span>`Optional` `Sample value: 10`

Grey release ratio. This indicates the proportion of total traffic allocated to the new version.


* Value range: 0–100

* Unit: %



**VersionNumber ** <span data-label="purple">integer </span>`Optional` `Sample value: 1`

Release version number. 0: Indicates the latest version.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RuntimeId ** <span data-label="purple">string </span>`Example value: r-ye7agye1a8cr38iu****`

ID of the runtime.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=ReleaseRuntime&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "RuntimeId": "r-ye6xzwchkwoaroxxxxxx"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "ReleaseRuntime",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "RuntimeId": " r-3thhlu***"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.RuntimeId |The required parameter RuntimeId is not supplied. |The parameter RuntimeId cannot be empty. |
|400 |MissingParameter.VersionNumber |The required parameter VersionNumber is not supplied. |The parameter VersionNumber cannot be empty. |
