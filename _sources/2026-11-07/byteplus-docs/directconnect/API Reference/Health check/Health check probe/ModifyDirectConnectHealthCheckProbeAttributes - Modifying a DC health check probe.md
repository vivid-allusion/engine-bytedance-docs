---
title: "ModifyDirectConnectHealthCheckProbeAttributes - Modifying a DC health check probe"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/ModifyDirectConnectHealthCheckProbeAttributes"
---

Call the modifyDirectConnectHealthCheckProbeAttributes API to modify the name of a specified health check probe.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDirectConnectHealthCheckProbeAttributes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|DpVLHS">必选</span>`Example: ModifyDirectConnectHealthCheckProbeAttributes`

The interface name. The current API name is `ModifyDirectConnectHealthCheckProbeAttributes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|fBo434">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectHealthCheckProbeId ** <span data-label="purple">String </span><span data-api-tag="require|J4HP1Z">必选</span> `Example: dhp-2752hz4****`

The ID of the health check probe to be modified.

You can call [DescribeDirectConnectHealthCheckProbes](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectHealthCheckProbes) to query the health check probe ID.



**DirectConnectHealthCheckProbeName ** <span data-label="purple">String </span>`optional` `Example: CheckProbes-01`

The name of the health check probe.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If you keep the original configurations, it indicates no modifications to the name of the health check probe.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyDirectConnectHealthCheckProbeAttributes&Version=2020-04-01&DirectConnectHealthCheckProbeId=dhp-2752hz4****&DirectConnectHealthCheckName=CheckProbes-01 HTTP/1.1
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
        "Action": "ModifyDirectConnectHealthCheckProbeAttributes",
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


|Status code |Error codes |Error message |Explain |
|---|---|---|---|
|400 |InvalidDirectConnectHealthCheck.InvalidStatus |The specified direct connect health check is not in the correct status for the request. |The specified health check cannot respond to this request due to its status. |
|400 |InvalidDirectConnectHealthCheckProbe.InvalidStatus |The specified direct connect direct connect health check is not in the correct status for the request. |The specified health check probe cannot respond to this request due to its status. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|404 |InvalidDirectConnectHealthCheckProbe.NotFound |The specified direct connect health check probe does not exist. |The specified health check probe does not exist. |
