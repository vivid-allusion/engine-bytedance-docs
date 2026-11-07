---
title: "DisablePrivateEgressDns - Disabling private egress DNS resolution"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/DisablePrivateEgressDns"
---

Call the DisablePrivateEgressDns API to disable DNS resolution for the private network egress.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

After DNS resolution is disabled for the private network egress, ArkClaw forwards DNS queries that were previously resolved through the external DNS server to the BytePlus DNS servers (100.96.0.2 and 100.96.0.3).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DisablePrivateEgressDns&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|cuadJG">必选</span> `Example: DisablePrivateEgressDns`

The action to perform. Value: **DisablePrivateEgressDns**.



**Version ** <span data-label="purple"> String </span><span data-api-tag="require|6jW5iQ">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**PrivateEgressId ** <span data-label="purple"> String </span><span data-api-tag="require|UQdWcu">必选</span> `Example: pre-p6q7r8s9t0****`

The ID of the private network egress.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**AsyncTaskId ** <span data-label="purple"> String </span>`Example: asynctask-13f0odozfrdvk3n6nu41l****`

The ID of the asynchronous task.



**RequestId ** <span data-label="purple"> String </span>`Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

The request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
GET /?Action=DisablePrivateEgressDns&Version=2020-04-01&PrivateEgressId=pre-p6q7r8s9t0****
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DisablePrivateEgressDns",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "AsyncTaskId": "asynctask-13f0odozfrdvk3n6nu41l****",
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API has no service\-specific error codes. For more details, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).
