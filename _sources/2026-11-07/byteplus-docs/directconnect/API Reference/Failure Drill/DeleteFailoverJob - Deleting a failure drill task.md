---
title: "DeleteFailoverJob - Deleting a failure drill task"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DeleteFailoverJob"
---

Call DeleteFailoverJob to delete a specified failure drill task.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteFailoverJob&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|nIUBxf">必选</span> `Example: DeleteFailoverJob`

The interface name. The current API name is `DeleteFailoverJob`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|tCrpKN">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**JobId ** <span data-label="purple">String </span><span data-api-tag="require|WVVI6Y">必选</span> `Example: foj-1234***`

The ID of the failure drill task.

You can call the [DescribeFailoverJobs](https://docs.byteplus.com/en/docs/directconnect/DescribeFailoverJobs) API to query the failure drill task ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteFailoverJob&Version=2020-04-01&JobID=foj-1234*** HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202111161611080102121461940900****",
        "Action": "DeleteFailoverJob",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "RequestId": "202111161611080102121461940900****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidFailoverJob.InvalidStatus |The specified failover job is not in the correct status for the request. |The specified failover drill task cannot respond to this request due to its status. |
|400 |InvalidFailoverJob.IsNull |The failover job does not exist. |The failure drill task does not exist. |
|400 |InvalidFailoverJob.StatusIsRunning |The status of the object is running, so no operations are permitted. |The failure drill task is running and cannot be operated on. |
|403 |Forbidden |You are not authorized to perform operations on the specified shared connection. |No permission to perform actions on the specified Shared Line. |
|403 |InvalidFailoverJob.Forbidden |You are not authorized to perform failover job operations on the specified account. |No permission to perform failure drill task actions on the specified account. |
