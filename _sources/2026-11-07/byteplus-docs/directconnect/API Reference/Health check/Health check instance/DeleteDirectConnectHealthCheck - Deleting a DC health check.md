---
title: "DeleteDirectConnectHealthCheck - Deleting a DC health check"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectHealthCheck"
---

Call DeleteDirectConnectHealthCheck to delete a specified health check instance.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteDirectConnectHealthCheck&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|ZfQ4ni">必选</span> `Example: DeleteDirectConnectHealthCheck`

The interface name. The current API name is `DeleteDirectConnectHealthCheck`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|mdFMTL">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectHealthCheckId ** <span data-label="purple">String </span><span data-api-tag="require|FyGglX">必选</span> `Example: dhc-2752hz4tek****`

The ID of the health check instance to be deleted.

You can call the [DescribeDirectConnectHealthChecks](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectHealthChecks) API to query the ID of the health check instance.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteDirectConnectHealthCheck&Version=2020-04-01&DirectConnectHealthCheckId=dhc-2752hz4tek**** HTTP/1.1
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
        "Action": "DeleteDirectConnectHealthCheck",
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

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidDirectConnectHealthCheck.InvalidStatus |The specified direct connect health check is not in the correct status for the request. |The specified health check cannot respond to this request due to its status. |
|400 |InvalidDirectConnectHealthCheck.ProbeExist |The specified direct connect health check has probe. |The specified health check contains probes. |
|400 |QuotaExceeded.DirectConnectHealthCheck |You've reached the limit on the number of direct connect health check that you can create. |You have reached the maximum number of health checks that can be created. |
|404 |InvalidDirectConnectHealthCheck.NotFound |The specified direct connect health check does not exist. |The specified health check does not exist. |
